i recently rewrote my C http server in Rust btw, and this blog post i will be sharing how i did it.
when building the C  version i was following the codecrafters http server challenge, that's what motivated me to give it a try in C. My goal was to have a working prototype that passes tests
the post was getting too long so this will be the first and the other parts will follow
# Part 1
## Bind to a port
first step was to bind to a port and listen for incoming connections. Rust has tcp lib in standard library so let's use that:
```rust
	// bind to port
    let listener = TcpListener::bind("127.0.0.1:4221").unwrap();

	// listen for connections
    for stream in listener.incoming() {
        match stream {
			// if connection received
            Ok(_stream) => {
                println!("accepted new connection");
            }
			// if not print error and keep listening
            Err(e) => {
                println!("error: {}", e);
            }
        }
    }

```
we listen to incoming connection by continuously sending `recv` syscall under the hood to check if a connection is received, and it can return either error or the received connection.

now that we have operational TCP connections, it's time to get to the meat. implementing http.
but before adding any functionality, i think the best approach is to start with the important components of it, which are the http request and response. out server needs to handle http requests and then responds to them accordingly that's what http servers do.
Let's start with parsing http messages. if you are not familiar with http messages, requests and response have similar format and they are both considered http messages the only difference is their first part called `start-line` in requests it's called `request-line` and in responses `status-line` yes NOT `response-line` as you may have guessed. anyways 
### http message format
```
start-line CRLF
*( field-line CRLF )
CRLF
[ message-body ]
```
this `*( field-line CRLF )` means multiple headers each one ended by `CRLF`

exemple http request:
```
GET / HTTP/1.1
Host: localhost:8080
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:135.0) Gecko/20100101 Firefox/135.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br, zstd
Sec-GPC: 1
Connection: keep-alive
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: cross-site
Priority: u=0, i

```
this request doesn't have a body (most GET requests don't)

the http RFC suggest some steps to correctly parse a message :

> [The normal procedure for parsing an HTTP message is to read the start-line into a structure, read each header field line into a hash table by field name until the empty line, and then use the parsed data to determine if a message body is expected. If a message body has been indicated, then it is read as a stream until an amount of octets equal to the message body length is read or the connection is closed. ](https://datatracker.ietf.org/doc/html/rfc9112#name-message-parsing)

that's exactly what we will be doing, so we'll start by parsing requests:
```rust
// request-line looks like this
// "{method} {target} {version}"
// ex: "GET / HTTP/1.1"
pub struct RequestLine {
    pub method: String,
    pub target: String,
    pub version: String,
}
```
and the actual request:
```rust
pub struct Request {
    pub request_line: RequestLine,
    pub headers: HashMap<String, Vec<String>>,
    pub body: Vec<u8>,
}
```
notice that headers hashmap has values of type vector, meaning that a header can have multiple values separated by a comma, that's something i wasn't aware of before
the body is optional so you may inclined to wrap it inside an Option type but i didn't find it necessary since a vector can be empty. but an option type would be a better representation, especially for library interface. that's an enhancement for another time. let's get going.
now that we layed our request structure let's do the actual parsing.

```rust
impl Request {
    pub fn new(stream: &TcpStream) -> anyhow::Result<Self> {

```
this is our Request constructor signature , it takes a tcp stream parse it and return a Request struct here's it is wrapped in a result because the function can error.

first we initialize a buffered reader that will read from the tcp stream:
```rust
use std::io::{BufRead, BufReader, Read};
let mut buf_reader = BufReader::new(stream);
```
here we parse the request-line:
```rust
//read start-line into struct
let mut start_line = String::new();
buf_reader.read_line(&mut start_line)?;
let start_line = start_line.trim();
let parts: Vec<&str> = start_line.split_whitespace().collect();
if parts.len() != 3 {
	bail!("Invalid request line");
}
let request_line = RequestLine {
	method: parts[0].to_string(),
	target: parts[1].to_string(),
	version: parts[2].to_string(),
};

let mut request = Request {
	request_line,
	headers: HashMap::new(),
	body: Vec::new(),
};
```
next, we should parse the headers:
```rust
// read each header field line into hash table by field name until empty line
let mut line = String::new();
loop {
	line.clear();
	buf_reader.read_line(&mut line)?;
	let line = line.trim();
	if line.is_empty() {
		break;
	}
	let header = line.split_once(":").unwrap();
	let (header, values) = (header.0.trim(), header.1.trim());
	request
		.headers
		.entry(header.to_string())
		.or_insert(
			values
				.split(",")
				.map(|value| value.trim().to_string())
				.collect(),
		);
}
```
finally we parse the body if content-length header is present:
```rust
// use parsed data to determine if body is expected
if let Some(content_length) = request.headers.get("Content-Length") {
	// if message expected
	println!("content-length: {:#?}", content_length);
	if let Ok(content_length) = content_length[0].parse::<usize>() {
		// read body until amounts of octets equal to content-length header or connection is
		// closed
		let mut buffer: Vec<u8> = vec![0; content_length];
		buf_reader.read_exact(&mut buffer)?;
		request.body = buffer;
	}
}
```
if we reached thus far in the function then the response  is parsed with no errors, at the end of the function we return the request struct as an `Ok` value
```rust
Ok(request)
```

let's move to crafting responses
```rust
/// HTTP Response struct
pub struct Response {
    pub status_line: StatusLine,
    pub headers: HashMap<String, Vec<String>>,
    pub body: Vec<u8>,
}

/// HTTP Response Status Line struct
pub struct StatusLine {
    pub version: String,
    pub status_code: u16,
    pub reason_phrase: Option<String>,
}
```

to transform the struct into a byte vector, we use a method we called here `to_bytes`, first let's implement it for StatusLine:
```rust
impl StatusLine {
    pub fn to_bytes(&self) -> Vec<u8> {
		// if reason phrase is None it will become an empty string
        let reason_phrase = self.reason_phrase.clone().unwrap_or("".to_string());
        format!("{} {} {}", self.version, self.status_code, reason_phrase)
            .as_bytes()
            .to_vec()
    }
}
```
i'm using a vector `Vec<u8>` rather than an array `[u8]` because we're gonna passing the buffer around so it should be heap allocated.

let's make a function that initializes the 
```rust
impl Response {
    pub fn new() -> Self {
        let mut headers = HashMap::new();
        // headers.insert("Server".to_string(), vec!["faras".to_string()]);
        headers.insert("Content-Type".to_string(), vec!["text/plain".to_string()]);
        Response {
            status_line: StatusLine {
                version: "HTTP/1.1".to_string(),
                status_code: 200,
                reason_phrase: Some("OK".to_string()),
            },
            body: Vec::new(),
            headers,
        }
    }
```


# Part 1
## Respond with 200
now we will be using the `send` syscall to send data over our current tcp connection, and of course syscalls are abstracted away by rust's standard library.
## extract url path from request
## Respond with req url params
## Respond with req user-agent
## support concurrent connections
## respond with requested file
## create file from req body
## support compression