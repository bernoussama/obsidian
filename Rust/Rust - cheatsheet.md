## Structs
--- 
### Definition
```rust
// Classic struct with named fields
struct Student { name: String, level: u8, remote: bool }

// Tuple struct with data types only
struct Grades(char, char, char, char, f32);

// Unit struct
struct Unit;
```

### Instantiation
```rust
// Instantiate classic struct, specify fields in random order, or in specified order
let user_1 = Student { name: String::from("Constance Sharma"), remote: true, level: 2 };
let user_2 = Student { name: String::from("Dyson Tan"), level: 5, remote: false };

// Instantiate tuple structs, pass values in same order as types defined
let mark_1 = Grades('A', 'A', 'B', 'A', 3.75);
let mark_2 = Grades('B', 'A', 'A', 'C', 3.25);

println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}", 
         user_1.name, user_1.level, user_1.remote, mark_1.0, mark_1.1, mark_1.2, mark_1.3, mark_1.4);
println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}", 
         user_2.name, user_2.level, user_2.remote, mark_2.0, mark_2.1, mark_2.2, mark_2.3, mark_2.4);
```

### Define enum
```rust
enum WebEvent {
    // An enum variant can be like a unit struct without fields or data types
    WELoad,
    // An enum variant can be like a tuple struct with data types but no named fields
    WEKeys(String, char),
    // An enum variant can be like a classic struct with named fields and their data types
    WEClick { x: i64, y: i64 }
}
```

### Define enum with structs
```rust
// Define a tuple struct
struct KeyPress(String, char);

// Define a classic struct
struct MouseClick { x: i64, y: i64 }

// Redefine the enum variants to use the data from the new structs
// Update the page Load variant to have the boolean type
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }
```

### Instantiate enum
 For each variant, we use the `let` keyword to make the assignment. To access the specific variant in the enum definition, we use the syntax `<enum>::<variant>` with double colons `::`.
 
```rust
let we_load = WebEvent::WELoad(true);


// Instantiate a MouseClick struct and bind the coordinate values
let click = MouseClick { x: 100, y: 250 };

// Set the WEClick variant to use the data in the click struct
let we_click = WebEvent::WEClick(click);


// Instantiate a KeyPress tuple and bind the key values
let keys = KeyPress(String::from("Ctrl+"), 'N');
    
// Set the WEKeys variant to use the data in the keys tuple
let we_key = WebEvent::WEKeys(keys);
```

#### Example
```rust
// Define a tuple struct
#[derive(Debug)]
struct KeyPress(String, char);

// Define a classic struct
#[derive(Debug)]
struct MouseClick { x: i64, y: i64 }

// Define the WebEvent enum variants to use the data from the structs
// and a boolean type for the page Load variant
#[derive(Debug)]
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }

fn main() {
    // Instantiate a MouseClick struct and bind the coordinate values
    let click = MouseClick { x: 100, y: 250 };
    println!("Mouse click location: {}, {}", click.x, click.y);
        
    // Instantiate a KeyPress tuple and bind the key values
    let keys = KeyPress(String::from("Ctrl+"), 'N');
    println!("\nKeys pressed: {}{}", keys.0, keys.1);
        
    // Instantiate WebEvent enum variants
    // Set the boolean page Load value to true
    let we_load = WebEvent::WELoad(true);
    // Set the WEClick variant to use the data in the click struct
    let we_click = WebEvent::WEClick(click);
    // Set the WEKeys variant to use the data in the keys tuple
    let we_key = WebEvent::WEKeys(keys);
        
    // Print the values in the WebEvent enum variants
    // Use the {:#?} syntax to display the enum structure and data in a readable form
    println!("\nWebEvent enum structure: \n\n {:#?} \n\n {:#?} \n\n {:#?}", we_load, we_click, we_key);
}
```

### Debug statements

In the previous example, look for the following code statement. This statement is used in several places in the code.
```rust
// Set the Debug flag so we can check the data in the output
#[derive(Debug)]
```

The `#[derive(Debug)]` syntax lets us see certain values during the code execution that aren't otherwise viewable in standard output. To view debug data with the `println!` macro, we use the syntax `{:#?}` to format the data in a readable manner.

1. All variants in a Rust enum are grouped together into the same type. Functions that use any variant of an enum must accept all its variants. How can you work around these enum variant requirements?

> Define a separate struct for each variant in the enum to hold the variant data.
> 
> 	- Correct! By defining a separate struct for each variant in the enum, you can directly access the data for a specific variant.

When you read code in the Rust language, you'll notice the syntax `<T>`. This syntax represents the use of a generic type `T`. ***We use a generic type declaration when we don't yet know the actual data type***.

The generic type syntax is used to declare vectors. The syntax `<vector><T>` declares a vector type composed of a generic (not yet known) data type `T`. To actually create a vector, we use a concrete type like `<vector>u32`, a vector of type `u32`, or `<vector>String`, a vector of type String.

```rust 
// Create empty vector, declare vector mutable so it can grow and shrink
let mut fruit = Vec::new();

// Push values onto end of vector, type changes from generic `T` to String
fruit.push("Apple");
fruit.push("Banana");
fruit.push("Cherry");
println!("Fruits: {:?}", fruit);

// Pop off value at end of vector
// Call pop() method from inside println! macro
println!("Pop off: {:?}", fruit.pop());
println!("Fruits: {:?}", fruit);
```

### Hash maps
```rust
use std::collections::HashMap;
let mut reviews: HashMap<String, String> = HashMap::new();

reviews.insert(String::from("Ancient Roman History"), String::from("Very accurate."));
reviews.insert(String::from("Cooking with Rhubarb"), String::from("Sweet recipes."));
reviews.insert(String::from("Programming in Rust"), String::from("Great examples."));
```
#### insert to hash map
```rust
// Look for a specific review
let book: &str = "Programming in Rust";
println!("\nReview for \'{}\': {:?}", book, reviews.get(book));
```
#### remove from hash map
```rust
// Remove book review
let obsolete: &str = "Ancient Roman History";
println!("\n'{}\' removed.", obsolete);
reviews.remove(obsolete);

// Confirm book review removed
println!("\nReview for \'{}\': {:?}", obsolete, reviews.get(obsolete));
```

### Loops
```rust
loop {
    // Keep printing, printing, printing...
    println!("We loop forever!");
    // On the other hand, maybe we should stop!
    break;                            
}
```

```rust
while counter < 5 {
    println!("We loop a while...");
    counter = counter + 1;
}
```

```rust
let big_birds = ["ostrich", "peacock", "stork"];
for bird in big_birds
```

We access the items in the collection by using the `iter()` method. The `for` expression binds the current value of the iterator to the result of the `iter()` method. In the expression body, we can work with the iterator value.
```rust
let big_birds = ["ostrich", "peacock", "stork"];
for bird in big_birds.iter() {
    println!("The {} is a big bird.", bird);
}
```

Another easy way to create an iterator is to use the range notation `a..b`. The iterator starts at the `a` value and continues through to `b` in steps of one, but it doesn't use the value `b`.
```rust
for number in 0..5 {
    println!("{}", number * 2);
}
```

### error handling
> Panicking is the simplest error handling mechanism in Rust.
	You can use the `panic!` macro to _panic_ the current thread. The macro prints an error message, frees resources, and then exits the program.
```rust
fn main() {
    panic!("Farewell!");
}
```
#### Option type
The Rust standard library provides an `Option<T>` enum to be used when the absence of a value is a possibility. `Option<T>` is widely used in Rust code. It's useful for working with values that might exist or that might be empty.

In many other languages absence of a value would be modeled using `null` or `nil`, but Rust doesn't use `null` outside of code that interoperates with other languages. Rust is explicit about when a value is optional. While in many languages, a function that takes a `String` might actually take either a `String` or `null`, in Rust, that same function can only take an actual `String`. If you want to model an optional string in Rust, you need to explicitly wrap it in an `Option` type: `Option<String>`.

```rust
enum Option<T> {
    None,     // The value doesn't exist
    Some(T),  // The value exists
}
```

```rust
fn main() {
let fruits = vec!["banana", "apple", "coconut", "orange", "strawberry"];
for &index in [0, 2, 99].iter() {
    match fruits.get(index) {
        Some(&"coconut") => println!("Coconuts are awesome!!!"),
        Some(fruit_name) => println!("It's a delicious {}!", fruit_name),
        None => println!("There is no fruit! :("),
    }
}
}
```

In the following example, the input to `match` is an `Option<u8>` value. The `match` expression should only run code if that input value is _7_.
```rust
let a_number: Option<u8> = Some(7);
match a_number {
    Some(7) => println!("That's my lucky number!"),
    _ => {},
}
```
In this case, we'd like to ignore the `None` variant and all `Some<u8>` values that don't match `Some(7)`. Wildcard patterns are useful for this type of situation. You can add the `_` (underscore) wildcard pattern after all other patterns to match _anything else_, and it's used to satisfy the compiler demands for exhausting match arms.

To condense this code, you can use an _if let_ expression:
```rust
let a_number: Option<u8> = Some(7);
if let Some(7) = a_number {
    println!("That's my lucky number!");
}
```

### Use `unwrap` and `expect`

> You can try to access the inner value of an `Option` type directly by using the `unwrap` method. Be careful, though, because this method will panic if the variant is a `None`.
```rust
let gift = Some("candy");
assert_eq!(gift.unwrap(), "candy");

let empty_gift: Option<&str> = None;
assert_eq!(empty_gift.unwrap(), "candy"); // This will panic!
```

The `expect` method does the same as `unwrap`, but it provides a custom panic message that's provided by its second argument:
```rust
let a = Some("value");
assert_eq!(a.expect("fruits are healthy"), "value");

let b: Option<&str> = None;
b.expect("fruits are healthy"); // panics with `fruits are healthy`
```

Because these functions might panic, we don't recommend using them. Instead, consider either of the following approaches:

-   Use pattern matching and handle the `None` case explicitly.
-   Call similar non-panicking methods, such as `unwrap_or`, which returns a default value if the variant is `None` or the inner value if the variant is `Some(value)`.

#### unwrap_or()
```rust
assert_eq!(Some("dog").unwrap_or("cat"), "dog");
assert_eq!(None.unwrap_or("cat"), "cat");
```


```rust
enum Result<T, E> {
    Ok(T):  // A value T was obtained.
    Err(E): // An error of type E was encountered instead.
}
```
```rust
#[derive(Debug)]
struct DivisionByZeroError;

fn safe_division(dividend: f64, divisor: f64) -> Result<f64, DivisionByZeroError> {
    if divisor == 0.0 {
        Err(DivisionByZeroError)
    } else {
        Ok(dividend / divisor)
    }
}

fn main() {
    println!("{:?}", safe_division(9.0, 3.0));
    println!("{:?}", safe_division(4.0, 0.0));
    println!("{:?}", safe_division(0.0, 2.0));
}
```

## Ownership

### Scoping rules

In Rust, like most other programming languages, variables are valid only within a certain _scope_. In Rust, scopes are often denoted by using curly brackets `{}`. Common scopes include function bodies and `if`, `else`, and `match` branches.

> Note
	In Rust, "variables" are often called "bindings". This is because "variables" in Rust aren't very variable - they don't change that often since they're unchangeable by default. Instead, we often think about names being "bound" to data, hence the name "binding". In this module, we'll use the terms "variable" and "binding" interchangeably.

```rust
// `mascot` is not valid and cannot be used here, because it's not yet declared.
{
    let mascot = String::from("ferris");   // `mascot` is valid from this point forward.
    // do stuff with `mascot`.
}
// this scope is now over, so `mascot` is no longer valid and cannot be used.
```

### Ownership and dropping

> **Rust adds a twist to the idea of scopes. Whenever an object goes out of scope, it's "dropped." Dropping a variable releases any resources that are tied to it. For variables of files, the file ends up being closed. For variables that have allocated memory associated with them, the memory is freed.
> In Rust, bindings that have things "associated" with them that they'll free when the binding is dropped are said to "own" those things.**

```rust
{
    let mascot = String::from("ferris");
    // mascot dropped here. The string data memory will be freed here.
}
```

## Move semantics

Sometimes, though, we don't want the things associated with a variable to be dropped at the end of scope. Instead, we want to transfer ownership of an item from one binding to another.

The simplest example is when declaring a new binding:
```rust
{
    let mascot = String::from("ferris");
    // transfer ownership of mascot to the variable ferris.
    let ferris = mascot;
    // ferris dropped here. The string data memory will be freed here.
}
```

A key thing to understand is that once ownership is transferred, the old variable is no longer valid. In our previous example, after we transfer ownership of the `String` from `mascot` to `ferris`, we can no longer use the `mascot` variable.

In Rust, "transferring ownership" is known as "moving". In other words, the ownership of the `String` value has been _moved_ from `mascot` to `ferris`.

> **Important
>	 In Rust, only one thing can ever _own_ a piece of data at a time.**

> Your code must implement _either_ of the following definitions, but **not both at the same time**:
	-   One or more immutable references (`&T`)
	-   Exactly one mutable reference (`&mut T`)

## Traits

A trait is a common interface that a group of types can implement. The Rust standard library has many useful traits, such as:

-   `io::Read` for values that can read bytes from a source.
-   `io::Write` for values that can write out bytes.
-   `Debug` for values that can be printed in the console using the "{:?}" format specifier.
-   `Clone` for values that can be explicitly duplicated in memory.
-   `ToString` for values that can be converted to a `String`.
-   `Default` for types that have a sensible default value, like zero for numbers, empty for vectors, and “” for `String`.
-   `Iterator` for types that can produce a sequence of values.

In Rust, a trait is a collection of methods that define a behavior or capability that a type can have. Think of a trait as a contract that a type agrees to fulfill in order to be considered as having that behavior or capability.

For example, imagine you have a trait called Drawable that has a method called draw. Any type that implements the Drawable trait must provide an implementation of the draw method. This means that you can use the draw method on any value that implements the Drawable trait, regardless of its actual type.

Here's an example implementation of the Drawable trait for a Rectangle struct:

```rust
trait Drawable {
    fn draw(&self);
}

struct Rectangle {
    width: f64,
    height: f64,
}

impl Drawable for Rectangle {
    fn draw(&self) {
        println!("Drawing a rectangle with width {} and height {}", self.width, self.height);
    }
}
```
In this example, we define a trait called Drawable that requires an implementation of the draw method. We then define a Rectangle struct and implement the Drawable trait for it by providing an implementation of the draw method.

Now, we can create a Rectangle instance and call the draw method on it:

```rust
let rectangle = Rectangle { width: 10.0, height: 5.0 };
rectangle.draw();
```
This will output: Drawing a rectangle with width 10 and height 5.

Traits in Rust allow for code reuse and polymorphism, meaning that we can write code that can work with any type that implements a certain trait, without having to know the specific type at compile time. This makes Rust code more modular and flexible.