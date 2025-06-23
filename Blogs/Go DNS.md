# Introduction to DNS
![[Pasted image 20250622175711.png]]
![[Pasted image 20250622183945.png]]

if you want to go to let's say to `chatgpt.com` you need to send a request to their server, but to communicate with that server we need to have its ip address, now we only have its domain name so we need a way to get ip addresses from domain names since ip addresses are not meant to be used by humans. Luckily there's a protocol that takes care of translating domain names to ip addresses, it's DNS you can think of it like the yellow pages of the internet. But the real question is how does it work?
to understand how it works, i decided to make a dns server from scratch with 0 dependencies, that's what we will be going through in this blog post
## TLDR
![[Pasted image 20250622212636.png]]
so how does DNS work?

![[Pasted image 20250622191234.png]]
when type a domain name for example `chatgpt.com` in the browser and hit enter a DNS query is sent from your browser to a DNS recursive resolver.
> by default the dns server that the query will be sent to is provided by your internet provider, or the one you provided yourself like cloudflare's `1.1.1.1` or google's `8.8.8.8`

then, the recursive resolver sends a query to one of the root nameservers to get the ip address of tld in this case `.com` nameserver.
when it gets the `.com` ns (nameserver) ip, it sends a query to it to get the address of the authoritative ns for `chatgpt.com` 
and now it can query for the ip address of `chatgpt.com`  , and when the ns responds with the ip address. The DNS has concluded its job

# High level walkthrough
# Decoding DNS message
# Building DNS response

# Caching