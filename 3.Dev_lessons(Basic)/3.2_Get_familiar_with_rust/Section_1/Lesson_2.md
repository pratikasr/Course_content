# Lesson 2: Rust Syntax and Variables

In this lesson, we will dive into the fundamental aspects of Rust programming language. We will learn about the syntax, data types, variable declaration, initialization, and basic operators used in Rust programming.

## Learning Objectives

By the end of this lesson, you will be able to:

-   Understand the basic syntax and data types in Rust programming language
-   Declare and initialize variables in Rust
-   Use basic operators to manipulate values in Rust.

## Basic Syntax and Data Types in Rust

Rust is a systems programming language that is designed to be fast, efficient, and safe. The language has a simple and expressive syntax that is similar to that of other programming languages such as C++ and Python. Rust's syntax is designed to be easy to read and write, with a focus on safety and performance.

Rust has several built-in data types, including:

-   Integers: Rust supports various integer data types such as i8, i16, i32, i64, u8, u16, u32, and u64, representing signed and unsigned integers of different sizes. The size of the integer type affects the range of values it can hold.
-   Floating-point numbers: Rust supports floating-point numbers such as f32 and f64, representing single-precision and double-precision floating-point values, respectively. These types are useful for representing non-integer numbers and perform arithmetic operations involving decimal places.
-   Boolean: Rust supports boolean values (true or false) represented by the bool type. This type is used for logical operations.
-   Character: Rust supports character data type (char) representing a single Unicode scalar value. This type is used for representing a single character such as 'a' or 'ß'.
-   String: Rust supports strings (represented by the String type) as a collection of Unicode scalar values. Rust strings are mutable, resizable and UTF-8 encoded.

## Declaring and Initializing Variables

In Rust, you must declare a variable before using it. To declare a variable, you use the `let` keyword followed by the variable name and its data type (if not inferred by the compiler). Here's an example:

rustCopy code

`let x: i32 = 10;` 

This declares a variable named `x` of type `i32` and initializes it with a value of 10. The colon `:` is used to specify the type of the variable explicitly.

You can also declare a variable without explicitly specifying its data type, and the Rust compiler will infer it from the value you assign to the variable. Here's an example:

rustCopy code

`let y = 3.14;` 

This declares a variable named `y` and initializes it with a value of 3.14. The Rust compiler infers that the data type of `y` is `f64` (double-precision floating-point number) because 3.14 is a float value.

Variables are also mutable by default in Rust, meaning their values can be changed. To declare a mutable variable, use the `mut` keyword before the variable name.

rustCopy code

`let mut z: i32 = 5;
z = 10;` 

This declares a mutable variable `z` of type `i32` and initializes it with a value of 5. The `mut` keyword makes it possible to reassign the value of the variable later in the code.

## Using Basic Operators

Rust supports several basic operators such as arithmetic, comparison, logical, and bitwise operators. Here's an example:


    let a = 10;
    let b = 5;

    let sum = a + b;
    let difference = a - b;
    let product = a * b;
    let quotient = a / b;
    let remainder = a % b;

    let is_greater = a > b;
    let is_equal = a == b;
    let logical_and = is_greater && is_equal;
    let bitwise_or = a | b;

In this example, we declare two variables `a` and `b`, and use various arithmetic, comparison, logical, and bitwise operators to manipulate their values. The resulting values are stored in new variables `sum`, `difference`, `product`, `quotient`, `remainder`, `is_greater`, `is_equal`, `logical_and`, and `bitwise_or`.

## Conclusion

In this lesson, we have learned about the basic syntax and data types in Rust programming language, how to declare and initialize variables, and how to use basic operators to manipulate values in Rust. By understanding these fundamental aspects of Rust programming, you are now ready to move on to the next lesson and learn about control structures in Rust.