## This is the index over my Rust notes divided by topic and application area

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

