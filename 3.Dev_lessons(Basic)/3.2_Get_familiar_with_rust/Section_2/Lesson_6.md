# Lesson 6: Structs and Enums in Rust

Rust is not an object-oriented programming language, but it does provide features that allow you to achieve some of the same goals. Two of these features are structs and enums.

## Structs

A struct is a data structure that groups together variables of different types under a single name. It's similar to a class in an object-oriented language. Structs are defined using the `struct` keyword, followed by the name of the struct and a set of curly braces containing the variables that make up the struct.

Here's an example:


    struct Point {
        x: i32,
        y: i32,
    } 

This defines a `Point` struct with two `i32` variables: `x` and `y`. You can create a new instance of this struct like this:


`let my_point = Point { x: 3, y: 4 };` 

You can access the variables in a struct using dot notation:


    let my_x = my_point.x;
    let my_y = my_point.y; 

## Enums

An enum is a type that can have one of several values. It's similar to a class hierarchy in an object-oriented language. Enums are defined using the `enum` keyword, followed by the name of the enum and a set of curly braces containing the possible values.

Here's an example:


    enum Color {
        Red,
        Green,
        Blue,
    } 

This defines a `Color` enum with three possible values: `Red`, `Green`, and `Blue`. You can create a new instance of this enum like this:


`let my_color = Color::Red;` 

You can match on the value of an enum using a `match` expression:


    match my_color {
        Color::Red => println!("The color is red!"),
        Color::Green => println!("The color is green!"),
        Color::Blue => println!("The color is blue!"),
    } 

## Object-oriented programming in Rust

Rust doesn't have classes or inheritance like traditional object-oriented languages, but it does provide ways to achieve similar functionality. Structs can be used to group together variables and functions that operate on those variables, similar to how classes group together instance variables and methods. Enums can be used to define a set of related values, similar to how a class hierarchy defines a set of related classes.

Rust also provides traits, which are similar to interfaces in other languages. Traits define a set of methods that a type must implement in order to be considered to have that trait. This allows you to define generic functions that can operate on any type that implements a particular trait.


    trait Printable {
        fn print(&self);
    }

    struct MyStruct {
        x: i32,
    }

    impl Printable for MyStruct {
        fn print(&self) {
            println!("MyStruct {{ x: {} }}", self.x);
        }
    }

    fn print_something<T: Printable>(thing: &T) {
        thing.print();
    }

    fn main() {
        let my_struct = MyStruct { x: 42 };
        print_something(&my_struct);
    } 

This code defines a trait called `Printable`, which requires implementing a `print` method. The `MyStruct` struct implements this trait, and the `print_something` function takes a generic type that must implement the `Printable` trait. It then calls the `print` method on the passed-in object.

While Rust's approach to object-oriented programming may be different from other languages, it provides powerful features that can be used to achieve similar goals.