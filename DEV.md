# Rust
## Rust Installation and First Program

First, download Rust using `rustup`, a command-line tool for managing Rust versions and associated tools. [See the official guide for installing Rust](https://www.rust-lang.org/tools/install).

To install Rust, run:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

The installation script automatically adds Rust to your system PATH after the next login. If you want to start using Rust right away, run:
```bash
source $HOME/.cargo/env
```

Create a sample "Hello World" program in a file named `main.rs`:
```rust
fn main() {
    println!("Hello, world!");
}
```

To compile and run the program, use:
```bash
rustc main.rs
```

This step requires a linker, such as `gcc`, which is included in the `build-essential` package on Linux. After compilation, an executable file named `main` (or `main.exe` on Windows) will be created. Run the executable with:
```bash
./main
```

This will output:
```
Hello, world!
```

## Cargo

Cargo is the build system and package manager for Rust. It simplifies the management of Rust projects by automating tasks such as building code, downloading dependencies, and compiling those dependencies. **Cargo** is included with the Rust installation.

To check the version of Cargo, use:
```bash
cargo --version
```

### Creating a Project Using Cargo
To create a new project with Cargo:
```bash
cargo new hello_world
cd hello_world
```
The first command creates a new directory and project named *hello_world*. This project includes a `Cargo.toml` file and a `src` directory containing a `main.rs` file.

### Building and Running a Cargo Project
To build the project, run:
```bash
cargo build
```
This command generates an executable in *target/debug/hello_world*, rather than the current directory. The default build is a debug build, so Cargo places the binary in the debug directory:
```bash
./target/debug/hello_world
```
Running `cargo build` for the first time also creates a *Cargo.lock* file at the top level, which keeps track of the exact versions of dependencies in the project. There's no need to manually edit this file; Cargo manages it automatically.

To compile the code and run the executable in one step, use:
```bash
cargo run
```
Cargo will track changes in the source files, rebuild the project if changes are detected, and then run the binary.

Cargo also provides a command to quickly check your code for compilation without producing an executable:
```bash
cargo check
```

### Building for Release
When the project is ready for release, compile it with optimizations using:
```bash
cargo build --release
```
This will create the executable in *target/release* instead of *target/debug*.

### Understanding a Basic Rust Program
```rust
use std::io;

fn main() {
    println!("Please input your name");

    let mut name = String::new();

    io::stdin()
        .read_line(&mut name)
        .expect("Failed to read line");

    println!("Hello World {name}")
}
```

To obtain user input and print the result as output, we need to bring the `io` (input/output) library into scope. Rust includes a set of items in the standard library called the **prelude**, which is automatically brought into the scope of every program. More details can be found in the [standard library documentation](https://doc.rust-lang.org/std/prelude/index.html).

If a type we need is not in the prelude, we must explicitly bring it into scope with a `use` statement.

#### Storing Values with Variables
We create a variable to store user input with:
```rust
let mut name = String::new();
```

Using `let`, we create a variable, like `let num = 5;`, which creates a variable named `num` and assigns it the value of 5. By default, variables in Rust are immutable (their values cannot change once set). To make a variable mutable, we add `mut` before the variable name. Learn more about [variables and mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#variables-and-mutability).

```rust
let num = 43;  // immutable
let mut num_mutable = 32; // mutable
```

In the basic program, `let mut name` creates a mutable variable bound to a new instance of a `String`. The `new` function is an associated function of the `String` type that creates a new, empty `String`. `String` is a data type provided by the standard library, representing a growable, UTF-8 encoded bit of text.

#### Receiving User Input and Handling Exceptions
We include the input/output functionality from the standard library with `use std::io` at the top of the program. The code:
```rust
io::stdin()
    .read_line(&mut name)
    .expect("Failed to read line");
```
Here, `.read_line(&mut name)` calls the `read_line` method on the standard input handle to get input from the user. `read_line` takes whatever the user types into standard input and appends it to a string, so we pass that string as an argument. The string argument must be mutable so the method can change its content.

The `&` indicates that this argument is a *reference*, allowing multiple parts of the code to access one piece of data without needing to copy it into memory multiple times. We use `&mut name` to make the reference mutable.

`read_line` places the user's input into the string we pass to it and also returns a `Result` value. `Result` is an enumeration (enum), a type that can be one of multiple possible states. `Result` has two variants: `Ok` and `Err`.

- `Ok` indicates the operation was successful, containing the successfully generated value.
- `Err` means the operation failed, containing information about the failure.

Values of the `Result` type have methods defined on them. One such method is `expect`. If the `Result` is an `Err` value, `expect` will cause the program to crash and display the message passed to it. If it is an `Ok` value, the program will continue running.


#### Ensuring Reproducible Builds with the *Cargo.lock* File

Cargo ensures that you can consistently rebuild the same artifact. It will use only the versions of the dependencies you specified until you indicate otherwise. For example, if version `0.8.6` of the `rand` crate is released next week with an important bug fix but also a regression that breaks your code, your project will not automatically update to `0.8.6`.

When you build a project for the first time, Cargo determines the versions of dependencies that meet your criteria and writes them to the `Cargo.lock` file. On future builds, Cargo will use the versions specified in the `Cargo.lock` file, ensuring reproducible builds. This means your project will remain at `0.8.5` until you explicitly upgrade it, thanks to the `Cargo.lock` file.

### Variables
By default, variables are immutable. This is one of many nudges Rust guves us to write our code in a way that takes advantage of the safety and easy concurrency that Rust offers. Howevee, Rust also have option to make variables mutable.

```rust
let x = 5; //immutable variable x
let mut y = 5; //mutable variable y(value can be changed)
```
### Constants
Constants are like immutable variable, that are bound to a name and are not allowed to change. Constants are not just immutable by default, they are always immutable. We declare constants using the `const` keyword instead of `let` keyword, and type of the value *must* be annotated.

Constaant may be set only to constant expression, not the result of a value that could be computed at runtime.
```rust
const HOURS_IN_SECONDS: u32 = 60*60;
```

#### Shadowing
Although we cannot change the immutable variable, we can declare a new variable with same name as a previous variable. Rustaceans say that the first variable is shadowed by the second, which means that the second variable is what the compiler will see when you use the name of the variable. In effect, the second variable overshadows the first, taking any uses of the variable name to itself until either it itself is shadowed or the scope ends.


```rust
let a = 5;
let a = a+5; //valid since we are not changing value of variable, we are creating a new variable with same name

let spaces = "   ";
let spaces = spaces.len(); // store the lenght of spaces

/*
* In mutable variable, we acan update the value of variable, but its value should be same as that as when we defined it.
let mut spaces = "    ";
spaces = spaces.len(); // This will throw an error
*/
```

### Data Types

Rust is a **statically typed** language, which means it requires knowing the types of all variables at compile time.

**Scalar types** represent single values. Rust offers four primary scalar types: integers, floating-point numbers, booleans, and characters. Integer types are categorized as either signed (`i`) or unsigned (`u`), and their size can vary. Here’s a breakdown:

**Integer Types:**

| Length   | Signed | Unsigned |
|----------|--------|----------|
| 8-bit    | `i8`   | `u8`     |
| 16-bit   | `i16`  | `u16`    |
| 32-bit   | `i32`  | `u32`    |
| 64-bit   | `i64`  | `u64`    |
| 128-bit  | `i128` | `u128`   |
| Arch     | `isize`| `usize`  |

For signed integers, the range is from \(-2^{n-1}\) to \(2^{n-1}-1\), where \(n\) is the number of bits. Unsigned integers range from \(0\) to \(2^n - 1\). The `isize` and `usize` types adapt to the architecture of your computer: they are 64-bit on a 64-bit architecture and 32-bit on a 32-bit architecture.

**Integer Literals** can be written in various formats:

- **Decimal**: `98_222`
- **Hexadecimal**: `0xff`
- **Octal**: `0o77`
- **Binary**: `0b1111_0000`
- **Byte (u8 only)**: `b'A'`

Be cautious of integer overflow, which occurs when a value exceeds the variable's range. For details on handling overflow and panic modes, refer to the [Rust documentation](https://doc.rust-lang.org/book/ch03-02-data-types.html).

Rust has two floating point `f64`(double precision) which is default in rust and `f32` which is single precision.

### FAQ
1. Where NOT to use Semicolins?
Ans: If we are not returning a value a value from function or closure, we dibit need a semicolon in end of the return expression
```rust
fn calculate() -> i32 {
    let x = 5;
    let y = 10;
    x+y
}
```

##### References:
**From Rust Documentation**
- [Rust Book](https://doc.rust-lang.org/book/): The official Rust programming language book, offering comprehensive guidance on learning Rust.
- [Module fmt](https://doc.rust-lang.org/std/fmt/): Provides formatting functionality for strings, including printing and formatting with placeholders.
- [Module str](https://doc.rust-lang.org/stable/std/str/): Defines the `str` type and provides string manipulation functions in Rust.
- [Module io](https://doc.rust-lang.org/stable/std/io/): Contains types and functions for reading and writing input/output in Rust.
- [Module result](https://doc.rust-lang.org/stable/std/result/): Defines the `Result` type, used for error handling in Rust.
- [Module thread](https://doc.rust-lang.org/stable/std/thread/): Provides functionality for spawning and managing threads for concurrent execution.
- [Module collections](https://doc.rust-lang.org/stable/std/collections/): Defines common collection types like vectors, hash maps, and hash sets.
- [Module time](https://doc.rust-lang.org/stable/std/time/): Provides types and functions for working with time, including durations and timestamps.
- [Module sync Struct Arc](https://doc.rust-lang.org/stable/std/sync/struct.Arc.html): A thread-safe reference-counting pointer, allowing shared ownership across threads.
- [Module mpsc](https://doc.rust-lang.org/stable/std/sync/mpsc/index.html): Provides multi-producer, single-consumer channels for message passing between threads.
- [Module net](https://doc.rust-lang.org/stable/std/net/index.html): Defines networking primitives for TCP and UDP communication.