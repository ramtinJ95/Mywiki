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
