## Lesson 4: Functions in Rust

Functions are one of the most important concepts in programming. In this lesson, we will learn about declaring and calling functions, passing arguments to functions, and returning values from functions.

### Declaring and Calling Functions

In Rust, you can declare a function using the `fn` keyword, followed by the function name, the function's parameters (if any), and the function's return type (if any). Here is an example:


    fn greet(name: &str) {
        println!("Hello, {}!", name);
    }

    fn main() {
        greet("Alice");
    } 

In this example, we define a function called `greet` that takes a single parameter `name` of type `&str` (a string slice) and does not return a value. We then call the `greet` function from the `main` function, passing in the argument `"Alice"`.

### Passing Arguments to Functions

In Rust, function parameters are passed by value by default. This means that when a function is called with an argument, the value of the argument is copied into the function's parameter. However, you can also pass references or mutable references to data if you want to avoid copying large data structures. Here is an example:


    fn double(x: i32) -> i32 {
        x * 2
    }

    fn main() {
        let x = 5;
        let doubled = double(x);
        println!("{} doubled is {}", x, doubled);
    } 

In this example, we define a function called `double` that takes a single parameter `x` of type `i32` (a 32-bit integer) and returns the value of `x` multiplied by 2. We then call the `double` function from the `main` function, passing in the variable `x`. The value of `x` is copied into the `double` function's parameter, and the resulting value is returned and assigned to the `doubled` variable.

### Returning Values from Functions

In Rust, the return type of a function is specified using an arrow (`->`) followed by the return type. If a function does not return a value, the return type should be `()` (the unit type). Here is an example:


    fn add(x: i32, y: i32) -> i32 {
        x + y
    }

    fn main() {
        let sum = add(2, 3);
        println!("The sum of 2 and 3 is {}", sum);
    } 

In this example, we define a function called `add` that takes two parameters `x` and `y` of type `i32` (32-bit integers) and returns their sum. We then call the `add` function from the `main` function, passing in the values `2` and `3`. The resulting sum is returned and assigned to the `sum` variable, which we then print to the console.

Here are some advanced examples of functions in Rust:

**Example 1:** A function that returns a closure.


    fn create_adder(x: i32) -> impl Fn(i32) -> i32 {
        move |y| x + y
    } 

In this example, we have defined a function called `create_adder` that takes an integer `x` as an argument and returns a closure that takes an integer `y` as an argument and returns the sum of `x` and `y`. The `move` keyword is used to transfer ownership of the captured variable `x` into the closure.

**Example 2:** A function that takes a closure as an argument.


    fn operate_on_vec<F>(vec: Vec<i32>, operation: F) -> Vec<i32>
        where F: Fn(i32) -> i32
    {
        vec.iter().map(|&x| operation(x)).collect()
    } 

In this example, we have defined a function called `operate_on_vec` that takes a vector of integers `vec` and a closure `operation` as arguments. The closure `operation` takes an integer as an argument and returns an integer. The `where` keyword is used to specify that the closure `operation` must implement the `Fn(i32) -> i32` trait. The function `operate_on_vec` applies the closure `operation` to each element of the vector `vec` using the `map` method and returns a new vector containing the results using the `collect` method.

**Example 3:** A recursive function that calculates the factorial of a number.


    fn factorial(n: u32) -> u32 {
        match n {
            0 => 1,
            _ => n * factorial(n - 1)
        }
    } 

In this example, we have defined a function called `factorial` that takes an unsigned 32-bit integer `n` as an argument and returns the factorial of `n`. The function uses a match expression to handle the base case when `n` is 0 and the recursive case when `n` is greater than 0. The function calls itself recursively with `n - 1` as the argument until the base case is reached.

