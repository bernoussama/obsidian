# Rust Cookbook

## Basic Syntax

### The types have widths as follows:

- iN, uN, and fN are N bits wide,
- isize and usize are the width of a pointer,
- char is 32 bits wide,
- bool is 8 bits wide.

- Raw strings allow you to create a `&str` value with escapes disabled:
  `r"\n" == "\n"`. You can embed double-quotes by using an equal amount of `#`
  on either side of the quotes:

```rust
fn main() {
    println!(r#"<a href="link.html">link</a>"#);
    println!("<a href=\"link.html\">link</a>");
}
```

- Byte strings allow you to create a &[u8] value directly:

```rust
fn main() {
    println!("{:?}", b"abc");
    println!("{:?}", &[97, 98, 99]);
}
```

- All underscores in numbers can be left out, they are for legibility only. So
  1_000 can be written as 1000 (or 10_00), and 123_i64 can be written as 123i64.

- Arrays:

A value of the array type [T; N] holds N (a compile-time constant) elements of
the same type T. Note that the length of the array is part of its type, which
means that [u8; 3] and [u8; 4] are considered two different types.

We can use literals to assign values to arrays.

In the main function, the print statement asks for the debug implementation with
the ? format parameter: {} gives the default output, {:?} gives the debug
output. We could also have used {a} and {a:?} without specifying the value after
the format string.

Adding #, eg {a:#?}, invokes a “pretty printing” format, which can be easier to
read.

- Tuples:

Like arrays, tuples have a fixed length.

Tuples group together values of different types into a compound type.

Fields of a tuple can be accessed by the period and the index of the value, e.g.
t.0, t.1.

The empty tuple () is also known as the “unit type”. It is both a type, and the
only valid value of that type - that is to say both the type and its value are
expressed as (). It is used to indicate, for example, that a function or
expression has no return value, as we’ll see in a future slide.

You can think of it as void that can be familiar to you from other programming
languages.

#### References

```rust
fn main() {
    let mut x: i32 = 10;
    let ref_x: &mut i32 = &mut x;
    *ref_x = 20;
    println!("x: {x}");
}
```

- We must dereference ref_x when assigning to it, similar to C and C++ pointers.
- Rust will auto-dereference in some cases, in particular when invoking methods
  (try ref_x.count_ones()).
- References that are declared as mut can be bound to different values over
  their lifetime.

> Be sure to note the difference between let mut ref_x: &i32 and let ref_x: &mut
> i32. The first one represents a mutable reference which can be bound to
> different values, while the second represents a reference to a mutable value.

- Rust will statically forbid dangling references:

```rust
fn main() {
    let ref_x: &i32;
    {
        let x: i32 = 10;
        ref_x = &x;
    } // x will drop
    // ref_x is a dangling pointer now
    println!("ref_x: {ref_x}");
}
```

- A reference is said to “borrow” the value it refers to.
- Rust is tracking the lifetimes of all references to ensure they live long
  enough.
- We will talk more about borrowing when we get to ownership.

### Slices

A slice gives you a view into a larger collection:

```rust
fn main() {
    let mut a: [i32; 6] = [10, 20, 30, 40, 50, 60];
    println!("a: {a:?}");

    let s: &[i32] = &a[2..4];

    println!("s: {s:?}");
}
```

- Slices borrow data from the sliced type.

> Question: What happens if you modify a[3] right before printing s?

- We create a slice by borrowing a and specifying the starting and ending
  indexes in brackets.

- If the slice starts at index 0, Rust’s range syntax allows us to drop the
  starting index, meaning that &a[0..a.len()] and &a[..a.len()] are identical.

- The same is true for the last index, so &a[2..a.len()] and &a[2..] are
  identical.

- To easily create a slice of the full array, we can therefore use &a[..].

- `s` is a reference to a slice of i32s. Notice that the type of s (&[i32]) no
  longer mentions the array length. This allows us to perform computation on
  slices of different sizes.

- Slices always borrow from another object. In this example, a has to remain
  ‘alive’ (in scope) for at least as long as our slice.

- The question about modifying a[3] can spark an interesting discussion, but the
  answer is that for memory safety reasons you cannot do it through a at this
  point in the execution, but you can read the data from both a and s safely. It
  works before you created the slice, and again after the println, when the
  slice is no longer used.

### `String` vs `str`

```rust
fn main() {
    let s1: &str = "World";
    println!("s1: {s1}");

    let mut s2: String = String::from("Hello ");
    println!("s2: {s2}");
    s2.push_str(s1);
    println!("s2: {s2}");

    let s3: &str = &s2[6..];
    println!("s3: {s3}");
}
```

Rust terminology:

- &str an immutable reference to a string slice.
- String a mutable string buffer.

- &str introduces a string slice, which is an immutable reference to UTF-8
  encoded string data stored in a block of memory. String literals (”Hello”),
  are stored in the program’s binary.

- Rust’s String type is a wrapper around a vector of bytes. As with a `Vec<T>`, it
  is owned.

- As with many other types String::from() creates a string from a string
  literal; String::new() creates a new empty string, to which string data can be
  added using the push() and push_str() methods.

- The format!() macro is a convenient way to generate an owned string from
  dynamic values. It accepts the same format specification as println!().

- You can borrow &str slices from String via & and optionally range selection.

### FizzBuzz



```rust
fn main() {
    print_fizzbuzz_to(20);
}

fn is_divisible(n: u32, divisor: u32) -> bool {
    if divisor == 0 {
        return false;
    }
    n % divisor == 0
}

fn fizzbuzz(n: u32) -> String {
    let fizz = if is_divisible(n, 3) { "fizz" } else { "" };
    let buzz = if is_divisible(n, 5) { "buzz" } else { "" };
    if fizz.is_empty() && buzz.is_empty() {
        return format!("{n}");
    }
    format!("{fizz}{buzz}")
}

fn print_fizzbuzz_to(n: u32) {
    for i in 1..=n {
        println!("{}", fizzbuzz(i));
    }
}
```

- We refer in main to a function written below. Neither forward declarations nor
  headers are necessary.
- Declaration parameters are followed by a type (the reverse of some programming
  languages), then a return type.
- The last expression in a function body (or any block) becomes the return
  value. Simply omit the ; at the end of the expression.
- Some functions have no return value, and return the ‘unit type’, (). The
  compiler will infer this if the -> () return type is omitted.
- The range expression in the for loop in print_fizzbuzz_to() contains =n, which
  causes it to include the upper bound.

## Rustdoc

````rust
/// Determine whether the first argument is divisible by the second argument.
///
/// If the second argument is zero, the result is false.
///
/// # Example
/// ```
/// assert!(is_divisible_by(42, 2));
/// ```
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    if rhs == 0 {
        return false;  // Corner case, early return
    }
    lhs % rhs == 0     // The last expression in a block is the return value
}
````

The contents are treated as Markdown. All published Rust library crates are
automatically documented at docs.rs using the rustdoc tool. It is idiomatic to
document all public items in an API using this pattern. Code snippets can
document usage and will be used as unit tests.

### Function Overloading

Overloading is not supported:

- Each function has a single implementation:
  - Always takes a fixed number of parameters.
  - Always takes a single set of parameter types.
- Default values are not supported:
  - All call sites have the same number of arguments.
  - Macros are sometimes used as an alternative. However, function parameters
    can be generic:

```rust
fn pick_one<T>(a: T, b: T) -> T {
    if std::process::id() % 2 == 0 { a } else { b }
}

fn main() {
    println!("coin toss: {}", pick_one("heads", "tails"));
    println!("cash prize: {}", pick_one(500, 1000));
}
```

- When using generics, the standard library’s `Into<T>` can provide a kind of
  limited polymorphism on argument types. We will see more details in a later
  section.

### break and continue

- If you want to exit a loop early, use break,
- If you want to immediately start the next iteration use continue.

- Both continue and break can optionally take a label argument which is used to
  break out of nested loops:

```rust
fn main() {
    let v = vec![10, 20, 30];
    let mut iter = v.into_iter();
    'outer: while let Some(x) = iter.next() {
        println!("x: {x}");
        let mut i = 0;
        while i < x {
            println!("x: {x}, i: {i}");
            i += 1;
            if i == 3 {
                break 'outer;
            }
        }
    }
}
```

### Pattern matching

The match keyword is used to match a value against one or more patterns. In that
sense, it works like a series of if let expressions:

```rust
fn main() {
    match std::env::args().next().as_deref() {
        Some("cat") => println!("Will do cat things"),
        Some("ls")  => println!("Will ls some files"),
        Some("mv")  => println!("Let's move some files"),
        Some("rm")  => println!("Uh, dangerous!"),
        None        => println!("Hmm, no program name?"),
        _           => println!("Unknown program name!"),
    }
}
```

Like if let, each match arm must have the same type. The type is the last
expression of the block, if any. In the example above, the type is ().

- Save the match expression to a variable and print it out.
- Remove .as_deref() and explain the error.
	  - std::env::args().next() returns an `Option<String>`, but we cannot match
    against String.
  - as_deref() transforms an `Option<T>` to `Option<&T::Target>`. In our case, this
    turns `Option<String>` into `Option<&str>`.
  - We can now use pattern matching to match against the &str inside Option.

---

The match keyword let you match a value against one or more patterns. The
comparisons are done from top to bottom and the first match wins.

- The patterns can be simple values, similarly to switch in C and C++:

```rust
fn main() {
    let input = 'x';

    match input {
        'q'                   => println!("Quitting"),
        'a' | 's' | 'w' | 'd' => println!("Moving around"),
        '0'..='9'             => println!("Number input"),
        _                     => println!("Something else"),
    }
}
```

- The \_ pattern is a wildcard pattern which matches any value.

- some specific characters used when in a pattern

  - | as an or
  - .. can expand as much as it needs to be
  - 1..=5 represents an inclusive range
  - \_ is a wild card

#### Desructuring arrays

```rust
#[rustfmt::skip]
fn main() {
    let triple = [0, -2, 3];
    println!("Tell me about {triple:?}");
    match triple {
        [a@.., 3] => println!("Last is 3 and the rest were {a:?}"),
        [0, y, z] => println!("First is 0, y = {y}, and z = {z}"),
        [1, ..]   => println!("First is 1 and the rest were ignored"),
        _         => println!("All elements were ignored"),
    }
}
```

#### Match Guards

```rust
#[rustfmt::skip]
fn main() {
    let pair = (2, -2);
    println!("Tell me about {pair:?}");
    match pair {
        (x, y) if x == y     => println!("These are twins"),
        (x, y) if x + y == 0 => println!("Antimatter, kaboom!"),
        (x, _) if x % 2 == 1 => println!("The first one is odd"),
        _                    => println!("No correlation..."),
    }
}
```

- They are not the same as separate if expression inside of the match arm. An if
  expression inside of the branch block (after =>) happens after the match arm
  is selected. Failing the if condition inside of that block won’t result in
  other arms of the original match expression being considered.

### Memory management

<div style="width:100%; height:192px;"><style type="text/css">svg { width: 100% !important; }</style><svg xmlns="http://www.w3.org/2000/svg" width="544" height="192"><style>line, path, circle, rect, polygon{stroke:var(--fg);stroke-width:2;stroke-opacity:1;fill-opacity:1;stroke-linecap:round;stroke-linejoin:miter;}text{font-family:Iosevka Fixed, monospace;font-size:14px;}rect.backdrop{stroke:none;fill:transparent;}.broken{stroke-dasharray:8;}.filled{fill:black;}.bg_filled{fill:transparent;}.nofill{fill:transparent;}.end_marked_arrow{marker-end:url(#arrow);}.start_marked_arrow{marker-start:url(#arrow);}.end_marked_diamond{marker-end:url(#diamond);}.start_marked_diamond{marker-start:url(#diamond);}.end_marked_circle{marker-end:url(#circle);}.start_marked_circle{marker-start:url(#circle);}.end_marked_open_circle{marker-end:url(#open_circle);}.start_marked_open_circle{marker-start:url(#open_circle);}.end_marked_big_open_circle{marker-end:url(#big_open_circle);}.start_marked_big_open_circle{marker-start:url(#big_open_circle);}<!--separator--></style><defs><marker id="arrow" viewBox="-2 -2 8 8" refX="4" refY="2" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><polygon points="0,0 0,4 4,2 0,0"></polygon></marker><marker id="diamond" viewBox="-2 -2 8 8" refX="4" refY="2" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><polygon points="0,2 2,0 4,2 2,4 0,2"></polygon></marker><marker id="circle" viewBox="0 0 8 8" refX="4" refY="4" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><circle cx="4" cy="4" r="2" class="filled"></circle></marker><marker id="open_circle" viewBox="0 0 8 8" refX="4" refY="4" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><circle cx="4" cy="4" r="2" class="bg_filled"></circle></marker><marker id="big_open_circle" viewBox="0 0 8 8" refX="4" refY="4" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><circle cx="4" cy="4" r="3" class="bg_filled"></circle></marker></defs><rect class="backdrop" x="0" y="0" width="544" height="192"></rect><text x="10" y="12">Stack</text><line x1="24" y1="24" x2="32" y2="24" class="solid"></line><line x1="40" y1="24" x2="48" y2="24" class="solid"></line><text x="282" y="12">Heap</text><line x1="296" y1="24" x2="304" y2="24" class="solid"></line><line x1="312" y1="24" x2="320" y2="24" class="solid"></line><text x="42" y="60">s1</text><text x="50" y="92">ptr</text><circle cx="164" cy="88" r="3" class="nofill"></circle><text x="322" y="92">H</text><text x="362" y="92">e</text><text x="402" y="92">l</text><text x="442" y="92">l</text><text x="482" y="92">o</text><text x="50" y="108">len</text><text x="178" y="108">5</text><text x="50" y="124">capacity</text><text x="178" y="124">5</text><line x1="56" y1="24" x2="64" y2="24" class="solid"></line><line x1="72" y1="24" x2="80" y2="24" class="solid"></line><line x1="88" y1="24" x2="96" y2="24" class="solid"></line><line x1="104" y1="24" x2="112" y2="24" class="solid"></line><line x1="120" y1="24" x2="128" y2="24" class="solid"></line><line x1="136" y1="24" x2="144" y2="24" class="solid"></line><line x1="152" y1="24" x2="160" y2="24" class="solid"></line><line x1="168" y1="24" x2="176" y2="24" class="solid"></line><line x1="184" y1="24" x2="192" y2="24" class="solid"></line><line x1="200" y1="24" x2="208" y2="24" class="solid"></line><line x1="328" y1="24" x2="336" y2="24" class="solid"></line><line x1="344" y1="24" x2="352" y2="24" class="solid"></line><line x1="360" y1="24" x2="368" y2="24" class="solid"></line><line x1="376" y1="24" x2="384" y2="24" class="solid"></line><line x1="392" y1="24" x2="400" y2="24" class="solid"></line><line x1="408" y1="24" x2="416" y2="24" class="solid"></line><line x1="424" y1="24" x2="432" y2="24" class="solid"></line><line x1="440" y1="24" x2="448" y2="24" class="solid"></line><line x1="456" y1="24" x2="464" y2="24" class="solid"></line><line x1="472" y1="24" x2="480" y2="24" class="solid"></line><line x1="488" y1="24" x2="496" y2="24" class="solid"></line><line x1="504" y1="24" x2="512" y2="24" class="solid"></line><line x1="296" y1="152" x2="304" y2="152" class="solid"></line><line x1="312" y1="152" x2="320" y2="152" class="solid"></line><line x1="328" y1="152" x2="336" y2="152" class="solid"></line><line x1="344" y1="152" x2="352" y2="152" class="solid"></line><line x1="360" y1="152" x2="368" y2="152" class="solid"></line><line x1="376" y1="152" x2="384" y2="152" class="solid"></line><line x1="392" y1="152" x2="400" y2="152" class="solid"></line><line x1="408" y1="152" x2="416" y2="152" class="solid"></line><line x1="424" y1="152" x2="432" y2="152" class="solid"></line><line x1="440" y1="152" x2="448" y2="152" class="solid"></line><line x1="456" y1="152" x2="464" y2="152" class="solid"></line><line x1="472" y1="152" x2="480" y2="152" class="solid"></line><line x1="488" y1="152" x2="496" y2="152" class="solid"></line><line x1="504" y1="152" x2="512" y2="152" class="solid"></line><line x1="24" y1="168" x2="32" y2="168" class="solid"></line><line x1="40" y1="168" x2="48" y2="168" class="solid"></line><line x1="56" y1="168" x2="64" y2="168" class="solid"></line><line x1="72" y1="168" x2="80" y2="168" class="solid"></line><line x1="88" y1="168" x2="96" y2="168" class="solid"></line><line x1="104" y1="168" x2="112" y2="168" class="solid"></line><line x1="120" y1="168" x2="128" y2="168" class="solid"></line><line x1="136" y1="168" x2="144" y2="168" class="solid"></line><line x1="152" y1="168" x2="160" y2="168" class="solid"></line><line x1="168" y1="168" x2="176" y2="168" class="solid"></line><line x1="184" y1="168" x2="192" y2="168" class="solid"></line><line x1="200" y1="168" x2="208" y2="168" class="solid"></line><g><path d="M 8,24 A 4,4 0,0,0 4,28" class="nofill"></path><line x1="4" y1="28" x2="4" y2="164" class="broken"></line><line x1="8" y1="24" x2="16" y2="24" class="solid"></line><path d="M 4,164 A 4,4 0,0,0 8,168" class="nofill"></path><line x1="8" y1="168" x2="16" y2="168" class="solid"></line></g><g><line x1="216" y1="24" x2="224" y2="24" class="solid"></line><path d="M 224,24 A 4,4 0,0,1 228,28" class="nofill"></path><line x1="228" y1="28" x2="228" y2="164" class="broken"></line><line x1="216" y1="168" x2="224" y2="168" class="solid"></line><path d="M 228,164 A 4,4 0,0,1 224,168" class="nofill"></path></g><g><path d="M 280,24 A 4,4 0,0,0 276,28" class="nofill"></path><line x1="276" y1="28" x2="276" y2="148" class="broken"></line><line x1="280" y1="24" x2="288" y2="24" class="solid"></line><path d="M 276,148 A 4,4 0,0,0 280,152" class="nofill"></path><line x1="280" y1="152" x2="288" y2="152" class="solid"></line></g><g><line x1="36" y1="72" x2="196" y2="72" class="solid"></line><line x1="36" y1="72" x2="36" y2="136" class="solid"></line><line x1="132" y1="72" x2="132" y2="136" class="solid"></line><line x1="196" y1="72" x2="196" y2="136" class="solid"></line><line x1="36" y1="136" x2="196" y2="136" class="solid"></line></g><g><line x1="308" y1="72" x2="508" y2="72" class="solid"></line><line x1="308" y1="72" x2="308" y2="104" class="solid"></line><line x1="348" y1="72" x2="348" y2="104" class="solid"></line><line x1="388" y1="72" x2="388" y2="104" class="solid"></line><line x1="428" y1="72" x2="428" y2="104" class="solid"></line><line x1="468" y1="72" x2="468" y2="104" class="solid"></line><line x1="508" y1="72" x2="508" y2="104" class="solid"></line><line x1="308" y1="104" x2="508" y2="104" class="solid"></line></g><g><line x1="168" y1="88" x2="296" y2="88" class="solid"></line><polygon points="296,84 304,88 296,92" class="filled"></polygon></g><g><line x1="520" y1="24" x2="528" y2="24" class="solid"></line><path d="M 528,24 A 4,4 0,0,1 532,28" class="nofill"></path><line x1="532" y1="28" x2="532" y2="148" class="broken"></line><line x1="520" y1="152" x2="528" y2="152" class="solid"></line><path d="M 532,148 A 4,4 0,0,1 528,152" class="nofill"></path></g></svg></div>

- String is backed by a Vec, so it has a capacity and length and can grow if
  mutable via reallocation on the heap.

- the underlying memory is heap allocated using the System Allocator and custom
  allocators can be implemented using the Allocator API

- We can inspect the memory layout with unsafe code. However, you should point
  out that this is rightfully unsafe!

```rust
fn main() {
    let mut s1 = String::from("Hello");
    s1.push(' ');
    s1.push_str("world");
    // DON'T DO THIS AT HOME! For educational purposes only.
    // String provides no guarantees about its layout, so this could lead to
    // undefined behavior.
    unsafe {
        let (ptr, capacity, len): (usize, usize, usize) = std::mem::transmute(s1);
        println!("ptr = {ptr:#x}, len = {len}, capacity = {capacity}");
    }
}
```

#### Scope-Based Memory Management

Constructors and destructors let you hook into the lifetime of an object.

By wrapping a pointer in an object, you can free memory when the object is
destroyed. The compiler guarantees that this happens, even if an exception is
raised.

This is often called resource acquisition is initialization (RAII) and gives you
smart pointers.

- C++ Example

```cpp
void say_hello(std::unique_ptr<Person> person) {
  std::cout << "Hello " << person->name << std::endl;
}
```

-The std::unique_ptr object is allocated on the stack, and points to memory
allocated on the heap.

- At the end of say_hello, the std::unique_ptr destructor will run.
- The destructor frees the Person object it points to. Special move constructors
  are used when passing ownership to a function:

```cpp
std::unique_ptr<Person> person = find_person("Carla");
say_hello(std::move(person));
```

- Rust achieves this by modeling ownership explicitly.

- If asked how at this point, you can mention that in Rust this is usually
  handled by RAII wrapper types such as Box, Vec, Rc, or Arc. These encapsulate
  ownership and memory allocation via various means, and prevent the potential
  errors in C.

You may be asked about destructors here, the Drop trait is the Rust equivalent.

#### Moves in Function Calls

When you pass a value to a function, the value is assigned to the function
parameter. This transfers ownership:

```rust
fn say_hello(name: String) {
    println!("Hello {name}")
}

fn main() {
    let name = String::from("Alice");
    // say_hello will receive a clone of name
    say_hello(name.clone());

    // name ownership moved to say_hello function
    say_hello(name);
    // name is freed after function execution
}
```

- With the first call to say_hello, main gives up ownership of name. Afterwards,
  name cannot be used anymore within main.
- The heap memory allocated for name will be freed at the end of the say_hello
  function.
- main can retain ownership if it passes name as a reference (&name) and if
  say_hello accepts a reference as a parameter.
- Alternatively, main can pass a clone of name in the first call (name.clone()).
- Rust makes it harder than C++ to inadvertently create copies by making move
  semantics the default, and by forcing programmers to make clones explicit.

### Copying and cloning

> Copying and cloning are not the same thing:

- Copying refers to bitwise copies of memory regions and does not work on
  arbitrary objects.
- Copying does not allow for custom logic (unlike copy constructors in C++).
- Cloning is a more general operation and also allows for custom behavior by
  implementing the `Clone` trait.
- Copying does not work on types that implement the `Drop` trait.

### Shared and Unique Borrows

Rust puts constraints on the ways you can borrow values:

- You can have one or more `&T` values at any given time, or
- You can have exactly one `&mut T `value.

```rust
fn main() {
    let mut a: i32 = 10;
    let b: &i32 = &a;
    println!("b: {b}");

    {
        let c: &mut i32 = &mut a;
        *c = 20;
    }

    println!("a: {a}");
    // will not compile because of this
    println!("b: {b}");
}
```

- The above code does not compile because a is borrowed as mutable (through c)
  and as immutable (through b) at the same time.
- Move the `println!` statement for b before the scope that introduces c to make
  the code compile.
- After that change, the compiler realizes that b is only ever used before the
  new mutable borrow of a through c. This is a feature of the borrow checker
  called “non-lexical lifetimes”.

### Structs

```rust
struct Person {
    name: String,
    age: u8,
}

fn main() {
    let mut peter = Person {
        name: String::from("Peter"),
        age: 27,
    };
    println!("{} is {} years old", peter.name, peter.age);

    peter.age = 28;
    println!("{} is {} years old", peter.name, peter.age);

    let jackie = Person {
        name: String::from("Jackie"),
        ..peter
    };
    println!("{} is {} years old", jackie.name, jackie.age);
}
```

- Structs work like in C or C++.
  - Like in C++, and unlike in C, no typedef is needed to define a type.
  - Unlike in C++, there is no inheritance between structs.
- Methods are defined in an impl block, which we will see in following slides.
- This may be a good time to let people know there are different types of
  structs.
  - Zero-sized structs e.g., `struct Foo`; might be used when implementing a
    trait on some type but don’t have any data that you want to store in the
    value itself.
- Tuple structs, used when the field names are not important.
- The syntax `..peter` allows us to copy the majority of the fields from the old
  struct without having to explicitly type it all out. It must always be the
  last element.

## standard lib

### `Vec`

```rust
fn main() {
    let mut v1 = Vec::new();
    v1.push(42);
    println!("v1: len = {}, capacity = {}", v1.len(), v1.capacity());

    let mut v2 = Vec::with_capacity(v1.len() + 1);
    v2.extend(v1.iter());
    v2.push(9999);
    println!("v2: len = {}, capacity = {}", v2.len(), v2.capacity());

    // Canonical macro to initialize a vector with elements.
    let mut v3 = vec![0, 0, 1, 2, 3, 4];

    // Retain only the even elements.
    v3.retain(|x| x % 2 == 0);
    println!("{v3:?}");

    // Remove consecutive duplicates.
    v3.dedup();
    println!("{v3:?}");
}
```

`Vec` implements `Deref<Target = [T]>`, which means that you can call slice methods on a `Vec`.

- `Vec` is a type of collection, along with `String` and `HashMap`. The data it contains is stored on the heap. This means the amount of data doesn’t need to be known at compile time. It can grow or shrink at runtime.
- Notice how `Vec<T>` is a generic type too, but you don’t have to specify `T` explicitly. As always with Rust type inference, the `T` was established during the first `push` call.
- `vec![...]` is a canonical macro to use instead of `Vec::new()` and it supports adding initial elements to the vector.
- To index the vector you use `[` `]`, but they will panic if out of bounds. Alternatively, using `get` will return an `Option`. The `pop` function will remove the last element.
- Show iterating over a vector and mutating the value: `for e in &mut v { *e += 50; }`

```rust
use std::collections::HashMap;

fn main() {
    let mut page_counts = HashMap::new();
    page_counts.insert("Adventures of Huckleberry Finn".to_string(), 207);
    page_counts.insert("Grimms' Fairy Tales".to_string(), 751);
    page_counts.insert("Pride and Prejudice".to_string(), 303);

    if !page_counts.contains_key("Les Misérables") {
        println!("We know about {} books, but not Les Misérables.",
                 page_counts.len());
    }

    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        match page_counts.get(book) {
            Some(count) => println!("{book}: {count} pages"),
            None => println!("{book} is unknown.")
        }
    }

    // Use the .entry() method to insert a value if nothing is found.
    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        let page_count: &mut i32 = page_counts.entry(book.to_string()).or_insert(0);
        *page_count += 1;
    }

    println!("{page_counts:#?}");
}
```
Try the following lines of code. The first line will see if a book is in the hashmap and if not return an alternative value. The second line will insert the alternative value in the hashmap if the book is not found.
```rust
  let pc1 = page_counts
      .get("Harry Potter and the Sorcerer's Stone ")
      .unwrap_or(&336);
  let pc2 = page_counts
      .entry("The Hunger Games".to_string())
      .or_insert(374);
```

- Unlike `vec!`, there is unfortunately no standard `hashmap!` macro.
    - Although, since Rust 1.56, HashMap implements [`From<[(K, V); N]>`](https://doc.rust-lang.org/std/collections/hash_map/struct.HashMap.html#impl-From%3C%5B(K,+V);+N%5D%3E-for-HashMap%3CK,+V,+RandomState%3E), which allows us to easily initialize a hash map from a literal array:
```rust
  let page_counts = HashMap::from([
    ("Harry Potter and the Sorcerer's Stone".to_string(), 336),
    ("The Hunger Games".to_string(), 374),
  ]);
```

- Alternatively HashMap can be built from any `Iterator` which yields key-value tuples.
    
- We are showing `HashMap<String, i32>`, and avoid using `&str` as key to make examples easier. Using references in collections can, of course, be done, but it can lead into complications with the borrow checker.
    
    - Try removing `to_string()` from the example above and see if it still compiles. Where do you think we might run into issues?
- This type has several “method-specific” return types, such as `std::collections::hash_map::Keys`. These types often appear in searches of the Rust docs. Show students the docs for this type, and the helpful link back to the `keys` method.

	```rust
	fn main() {
    let five = Box::new(5);
    println!("five: {}", *five);
}
```
![[Drawing 2023-10-16 14.42.14.excalidraw]]
`Box<T>` implements `Deref<Target = T>`, which means that you can [call methods from `T` directly on a `Box<T>`](https://doc.rust-lang.org/std/ops/trait.Deref.html#more-on-deref-coercion).

- `Box` is like `std::unique_ptr` in C++, except that it’s guaranteed to be not null.
> - **In the above example, you can even leave out the `*` in the `println!` statement thanks to `Deref`.**
- A `Box` can be useful when you:
    - have a type whose size that can’t be known at compile time, but the Rust compiler wants to know an exact size.
    - want to transfer ownership of a large amount of data. To avoid copying large amounts of data on the stack, instead store the data on the heap in a `Box` so only the pointer is moved.
```rust

#[derive(Debug)]
enum List<T> {
    Cons(T, Box<List<T>>),
    Nil,
}

fn main() {
    let list: List<i32> = List::Cons(1, Box::new(List::Cons(2, Box::new(List::Nil))));
    println!("{list:?}");
}
```

### `Rc`
```rust
use std::rc::Rc;

fn main() {
    let mut a = Rc::new(10);
    let mut b = Rc::clone(&a);

    println!("a: {a}");
    println!("b: {b}");
}
```

- See [`Arc`](https://google.github.io/comprehensive-rust/concurrency/shared_state/arc.html) and [`Mutex`](https://doc.rust-lang.org/std/sync/struct.Mutex.html) if you are in a multi-threaded context.
- You can _downgrade_ a shared pointer into a [`Weak`](https://doc.rust-lang.org/std/rc/struct.Weak.html) pointer to create cycles that will get dropped.

#### Speaker Notes

- `Rc`’s count ensures that its contained value is valid for as long as there are references.
- `Rc` in Rust is like `std::shared_ptr` in C++.
- `Rc::clone` is cheap: it creates a pointer to the same allocation and increases the reference count. Does not make a deep clone and can generally be ignored when looking for performance issues in code.
- `make_mut` actually clones the inner value if necessary (“clone-on-write”) and returns a mutable reference.
- Use `Rc::strong_count` to check the reference count.
- `Rc::downgrade` gives you a _weakly reference-counted_ object to create cycles that will be dropped properly (likely in combination with `RefCell`, on the next slide).
```rust
use std::cell::RefCell;
use std::rc::Rc;

#[derive(Debug, Default)]
struct Node {
    value: i64,
    children: Vec<Rc<RefCell<Node>>>,
}

impl Node {
    fn new(value: i64) -> Rc<RefCell<Node>> {
        Rc::new(RefCell::new(Node { value, ..Node::default() }))
    }

    fn sum(&self) -> i64 {
        self.value + self.children.iter().map(|c| c.borrow().sum()).sum::<i64>()
    }
}

fn main() {
    let root = Node::new(1);
    root.borrow_mut().children.push(Node::new(5));
    let subtree = Node::new(10);
    subtree.borrow_mut().children.push(Node::new(11));
    subtree.borrow_mut().children.push(Node::new(12));
    root.borrow_mut().children.push(subtree);

    println!("graph: {root:#?}");
    println!("graph sum: {}", root.borrow().sum());
}
```
- If we were using `Cell` instead of `RefCell` in this example, we would have to move the `Node` out of the `Rc` to push children, then move it back in. This is safe because there’s always one, un-referenced value in the cell, but it’s not ergonomic.
- To do anything with a Node, you must call a `RefCell` method, usually `borrow` or `borrow_mut`.
- Demonstrate that reference loops can be created by adding `root` to `subtree.children` (don’t try to print it!).
- To demonstrate a runtime panic, add a `fn inc(&mut self)` that increments `self.value` and calls the same method on its children. This will panic in the presence of the reference loop, with `thread 'main' panicked at 'already borrowed: BorrowMutError'`.
```rust
mod foo {
    pub fn do_something() {
        println!("In the foo module");
    }
}

mod bar {
    pub fn do_something() {
        println!("In the bar module");
    }
}

fn main() {
    foo::do_something();
    bar::do_something();
}
```
- Packages provide functionality and include a `Cargo.toml` file that describes how to build a bundle of 1+ crates.
- Crates are a tree of modules, where a binary crate creates an executable and a library crate compiles to a library.
- Modules define organization, scope, and are the focus of this section.

## [Paths](https://google.github.io/comprehensive-rust/modules/paths.html#paths)

Paths are resolved as follows:

1. As a relative path:
    
    - `foo` or `self::foo` refers to `foo` in the current module,
    - `super::foo` refers to `foo` in the parent module.
2. As an absolute path:
    
    - `crate::foo` refers to `foo` in the root of the current crate,
    - `bar::foo` refers to `foo` in the `bar` crate.

A module can bring symbols from another module into scope with `use`. You will typically see something like this at the top of each module:

```rust
use std::collections::HashSet;
use std::mem::transmute;
```

# [Filesystem Hierarchy](https://google.github.io/comprehensive-rust/modules/filesystem.html#filesystem-hierarchy)

Omitting the module content will tell Rust to look for it in another file:

`mod garden;`

This tells rust that the `garden` module content is found at `src/garden.rs`. Similarly, a `garden::vegetables` module can be found at `src/garden/vegetables.rs`.

The `crate` root is in:

- `src/lib.rs` (for a library crate)
- `src/main.rs` (for a binary crate)

Modules defined in files can be documented, too, using “inner doc comments”. These document the item that contains them – in this case, a module.
```rust
//! This module implements the garden, including a highly performant germination
//! implementation.

// Re-export types from this module.
pub use seeds::SeedPacket;
pub use garden::Garden;

/// Sow the given seed packets.
pub fn sow(seeds: Vec<SeedPacket>) { todo!() }

/// Harvest the produce in the garden that is ready.
pub fn harvest(garden: &mut Garden) { todo!() }
```

#### Speaker Notes

- Before Rust 2018, modules needed to be located at `module/mod.rs` instead of `module.rs`, and this is still a working alternative for editions after 2018.
    
- The main reason to introduce `filename.rs` as alternative to `filename/mod.rs` was because many files named `mod.rs` can be hard to distinguish in IDEs.
    
- Deeper nesting can use folders, even if the main module is a file:
    
```
src/
├── main.rs
├── top_module.rs
└── top_module/
    └── sub_module.rs

```
    
- The place rust will look for modules can be changed with a compiler directive:
    
  ```rust
#[path = "some/path.rs"]
mod some_module;
```
    This is useful, for example, if you would like to place tests for a module in a file named `some_module_test.rs`, similar to the convention in Go.
    

