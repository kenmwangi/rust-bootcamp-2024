# Introduction
Rust is a type-safe, highly-flexible, blazingly fast high-performance language.
It doesn't have garbage collector since it enforces memory safety by pointing all references to valid memory.
It prevents data races - through borrow checker that tracks object lifetime of all references in code during compile time.

## Rust Primitives Types and Variables

Primitive types in __Rust__ has fixed size thus stored in __stack__.
Other types such arrays stored in heap memory.

## example of basic primitives

- integers, signed and unsigned (i32,u8,u32 etc.)
- floating point types f32 and f64
- Booleans (bool)
- Characters (char)


## Variables 

Variables are statically typed - requires types for variables but not necessary since Rust has __type inference__. Example code

```rust
fn main() {
    let x = 5;
    let y = 6.5;
    println!("X is {}, Y is {}", x, y);
}
```
### Casting
Rust does not have implicit type conversion for its primitive types. For instance you cannot multiply f64 and i32
let area = 3.14 * 12 // no implicit type conversion.

Explicit type conversion (casting) using as keyword can fix this problem as show
n in the code example below

```rust

const PI: f64 = 3.14;

fn main() {
    let radius = 44;
    // explicit type conversion (Casting) using as keyword
    // convert PI f64 into i32
    let area = PI as i32 * radius * radius;

    println!("The area of the circle is: {}", area);
}

```
## Tuples, Arrays and Slices

__NB__: Arrays and tuples composed of primitives types are primitives considering they have fixed size.

```rust
fn main() {
    let my_tuple: (u32, f64, bool) = (4, 3.14, true);
    let my_array: [i8; 3] = [1, 2, 3];
}

```

## Example code using fibonacci series

```rust
// Generate the nth Fibonacci number
// Fibonacci series - sequence of number in which each number is the sum of two preceding ones.
use std::io;

fn fibonacci(n: i32) -> i32 {
    if n == 0 {
        return 0;
    }
    if n == 1 {
        return 1;
    }

    fibonacci(n - 1) + fibonacci(n - 2)
}

fn main() {
    println!("Enter a number");

    let mut number = String::new();

    io::stdin()
        .read_line(&mut number)
        .expect("Failed to read line");

    let number: i32 = number.trim().parse().expect("Invalid number");

    if number < 0 {
        panic!("Invalid number for Fibonacci");
    }

    println!("Fibonacci of {} is {}", number, fibonacci(number));
}

```



# Managing Memory in Rust
=========================

Rust has more control over memory usage. In Rust we allocate memory and de-allocate memory at specific points in a our program.

Rust __DOESN'T__ have __GARBAGE COLLECTION__.

__ownership__ is main concept governing Rust's memory model.
Heap memory always has one owner and once that owner gets out of scope, the memory gets de-allocated.

Rust software is fast since memory allocation will be de-allocated once the purpose is accomplished. 

### Ownership Rules
 - Each value in Rust has an owner.
 - There can only be one owner at a time.
 - When the owner goes out of scope,the value will be dropped.

### The Stack and Heap
Both stack and heap are parts of memory but they are structured in different ways.

1. __Stack__ stores values in the order it gets them and removes values in the opposite order, *last in, first out* (LIFO).
Adding data is *pushing onto the stack*.
Removing data is *popping off the stack*.
All data stored on the stack must have fixed size.

2. __Heap__ less organized and when you put data into heap, you request amount of space. Memory allocator finds an empty spot in heap big enough and it returns a *pointer* - address of that location in a process called *allocation on the heap*. Pointer is stored in stack since pointer to the heap has fixed size.

## Giving References to Functions

Remember, in Rust a value can only have one owner.
if you want to borrow,use a reference. For example, String for owned type, &str for a borrowed string.

- `fn func_name(variable: String)` - takes String and owns it. If it doesn't return anything, then variable dies inside the function.
- `fn fun_name(variable: &String)` - borrows String and can look at it. Variable doesn't die inside the function.
- `fn func_name(variable: &mut String) - borrows String and can change it. Variable doesn't die inside the function.






