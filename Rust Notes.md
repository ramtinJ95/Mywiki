## This is the index over my Rust notes divided by topic and application area

## Variables and Shadowing
Shadowing is pretty much what rust calls type conversions. By reusing the same
variable name but using the 'let' keyword we can have the same name for
different data types that the variable holds:
```rust
let number = 2;
let number = "3";
```
this would not have been possible if we had used the mut key word since that
requires us to determine a type in advance and then the type of that variable is
not allowed to change. This is great for type conversions.
## Conventions and general charachteristics of Rustlang
- constants in code are in all caps seperated with underscore
  THIS_IS_WHAT_I_MEAN
- Rust uses snake case for function and variable names.
- Statments in rust are instructions that perform some action and do not return
  a value. So we cannot have x = y = 6, like we can do in C langugaes.
- Comments are started with // and for each line that we want for a block of
  comments we have add a // infron, i.e there is no block comment syntax

## Compound types
Rust has two primitive compund types: tuples and arrays

#### Tuple

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);

``` 
the variable tup binds to the entire tuple beacuse a tuple is considered a
single compound element. this means that to get the individual values out we can
use patter matching like:

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
let (x,y,z) = tup;

println!("The value of y is: {y}");

// or we can use . notation

let five_hundred = tup.0
let six_point_four = tup.1

``` 
#### Array
The array in rust has a fixed size that has to be declared on initialization and
this lives in stack memory. Then there is the vector that is more of a dynamic
array, very similar to C and C++ and Java. So an array is an array and a vector
is rust and C languages is the arraylist in java.

#### Statements & Expressions
Statments in rust are instructions that perform some action and do not return
a value. So we cannot have x = y = 6, like we can do in C langugaes.

Instead what we can do is create a new scope block and have an expressions
inside it:

```rust
let y = {
    let x = 3;
    x + 1
};

``` 
The line x + 1 does NOT have an ending semicolon because expressions do not
include ending semicolons. If we would add a semicolon it will turn the
expressions into a statement and then it wont return a value. This behaviour
means that we can have functions like this:

```rust
fn main() {
  let x = plus_one(5);
  println!("The value of x: {x}";
}

fn plus_one(x: i32) -> i32 {
  x+1
}
``` 
Because x+1 is an expression and thus it returns a i32 which we have said that
this function will return. If we where to add a semicolon to this then it would
become a statment and return nothing, or it would return the unit type (), which
is not what we promised that the funcion would return. 

#### Control flow
One special thing that Rust has when it comes to repeting code is the loop. This
is a special kind of loop that just goes on forever like a while true loop. One
cool that is possible is that if we have multiple loops that are nested and we
want to break out of a loop that is not in the scope that is currently running
we can add lables and then break out of the parent loop through the use of the
label:


```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
``` 

### Ownership
For this part there is too much to take notes on just read the documentation,
anything I write would be inferior: https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html 


### Structs and methods
We can define a struct like any other language by simply doing:


```rust
struct Rectangle {
  width: u32,
  height: u32,
}
```
or if we want to create a struct which is in princple a type of tuple that makes
sense in our domain we can do

```rust
struct Point(i32, i32, i32);
``` 
Now it is possible to also define functions within the context of these struct
types, and these are called methods. Whats special in Rust in this regard is
that we do this outside the struct block, in what is called an implementation
block, impl. Like so:


```rust
impl Rectangle {
  fn area(&self) -> u32 {
    self.width * self.height
  }
}
``` 
Methods must have a parameter named self of type Self for their first 
parameter. Note that we still need to use the & in front of the self 
shorthand to indicate that this method borrows the Self instance, just as we 
did in rectangle: &Rectangle. Methods can take ownership of self, borrow self 
immutably, as we’ve done here, or borrow self mutably, just as they can any 
other parameter.

These functions that are defined in a impl block are called associated
functions since they are assosciated with the type named after the impl. Note
that it is possible to define associated function that dont have self as their
first parameter (and thus are not methods) because they dont need an instance of
the type to work with. An example of this is:

```rust
impl Rectangle {
  fn square(size: u32) -> Self {
    Self {
      width: size,
      height: size,
    }
  }
}
```
The Self keywords in the return type and in the body of the function are aliases
for the type that apperas afer the impl keyword, which in this case is
Rectangle.

It is possible to have multiple impl blocks for the same type but rarely is that
a useful thing to do since it will just look confusing. 


### Enums and pattern matching
The problem with, or rather the major limitation of structs is that they are not
quite as flexiable as Enums. Say that we want to have a collection of primitve
shapes such as triangles, squares and rectangles. With the struct approach we
would have to create a new struct with essentially the same code for all of
these but with Enums we can express our need in a concise manner.

```rust
enum IpAddrKind {
  V4,
  V6,
}

let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
``` 

We can then create a function that takes in the enum type and works for all the
possible enum values, something that would have require a new funciton for each
new strut otherwise

```rust
fn route(ip_kind: IpAddrKind) {}
``` 

If one would like to store some data associated with a type of the enum we can
do that directly when we define the diffrent enums. Note that it is possible for
the different enum valus to be associated or "hold" data that is off diffrent
types within the same enum defintion. 

```rust
enum IpAddr {
    V4(String),
    V6(String),
}
let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
``` 
If we have different data types for each value it looks like this:

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
``` 
One more important similarity between strucs and enums is that just as we are
able to define methods on structs using impl, we can do the same with enums:


```rust
impl Message {
    fn call(&self) {
        // method body would be defined here
    }
}

let m = Message::Write(String::from("hello"));
m.call();
``` 
#### The option Enum
Rust does not have the Null type in its type system. Instead we have the Option
enum that is defind by the standard library. For example, if you request the 
first item in a non-empty list, you would get a value. If you request the first
item in an empty list, you would get nothing. Expressing this concept in terms 
of the type system means the compiler can check whether you’ve handled all the
cases you should be handling; this functionality can prevent bugs that are
extremely common in other programming languages.

The implementation of this Enum is

```rust
enum Option<T> {
  None,
  Some(T),
}
``` 
Some special things to keep in mind when using the Option enum is for example
when we have the following situation:

```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);
let sum = x + y;
``` 
This code will not compile beause i8 and option<i8> are different types and thus
rust does not know how to add these types. This means that in order for this to
compile we need to convert the Option<T> to T type and also handle the case when
this value can be missing since that is a possiblity with the Option<T> type. To
get the Type T and many more things that is possible to do, one needs to check
the documentaiton for the Option enum. This is an important enum so its good
to get familiar with it in order to become a good Rust developer. 

#### Match and pattern matching
This is very similar to the patter matching stuff that Haskell does.

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

```
The use of the match pattern goes pretty deep in Rust and one can get quite
creative with how to use it. This is really cool because this creativity is risk
free in Rust because the compiler will tell you if you have missed to account
for an edge case or if you have missed a possible outcome completely. 
