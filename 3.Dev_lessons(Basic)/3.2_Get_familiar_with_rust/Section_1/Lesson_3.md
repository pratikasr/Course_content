# Lesson 3: Control Structures in Rust

In programming, control structures are used to determine the flow of the program based on certain conditions. In this lesson, we will learn about the different types of control structures in Rust with examples.

## If statements and conditional expressions

In Rust, if statements and conditional expressions are used to execute a block of code if a certain condition is met. The basic syntax for an if statement in Rust is:


    let x = 5;
    if x == 5 {
        println!("x is equal to 5");
    } 

In this example, we first declare a variable `x` and assign it a value of 5. We then use an if statement to check if `x` is equal to 5. If the condition is true, the code within the curly braces will be executed, which in this case is to print a message to the console.

Conditional expressions in Rust are similar to if statements, but they are used to assign a value to a variable based on a condition. The syntax for a conditional expression in Rust is:

    let result = if x == 5 {
        "x is equal to 5"
    } else {
        "x is not equal to 5"
    }; 

In this example, we use a conditional expression to assign a value to the `result` variable based on the value of `x`. If `x` is equal to 5, the first value is assigned, and if it is not, the second value is assigned.

## For loops and looping structures

For loops are used to iterate over a sequence of values in Rust. The basic syntax for a for loop in Rust is:


    let numbers = [1, 2, 3, 4, 5];
    for number in numbers.iter() {
        println!("{}", number);
    } 

In this example, we create an array of numbers and use a for loop to iterate over each element in the array and print it to the console.

Rust also provides other looping structures, such as loop, while, and while let, for more specific use cases.


    let mut counter = 0;
    loop {
        counter += 1;
        println!("{}", counter);
        if counter == 10 {
            break;
        }
    }

In this example, we use a loop to repeatedly print the value of `counter` to the console until it reaches 10, at which point we use the `break` keyword to exit the loop.

## Match expressions

Match expressions in Rust are used to compare a value against a series of patterns and execute code based on the pattern that matches. The basic syntax for a match expression in Rust is:


    let x = 5;
    match x {
        1 => println!("x is equal to 1"),
        2 | 3 => println!("x is equal to 2 or 3"),
        4..=6 => println!("x is between 4 and 6"),
        _ => println!("x is something else"),
    }

In this example, we use a match expression to compare the value of `x` against several patterns. If `x` is equal to 1, we print a message to the console. If `x` is equal to 2 or 3, we print a different message. If `x` is between 4 and 6, we print yet another message. Finally, if `x` does not match any of the other patterns, we print a default message using the underscore pattern.

## Here are some additional examples

## If statements and conditional expressions


    let x = 10;
    if x > 5 {
        println!("x is greater than 5");
    } else if x < 5 {
        println!("x is less than 5");
    } else {
        println!("x is equal to 5");
    }

    let result = if x % 2 == 0 {
        "x is even"
    } else {
        "x is odd"
    };
    println!("{}", result);

In this example, we use an if statement to check if `x` is greater than 5. If it is, we print a message to the console. If it is not, we check if it is less than 5. If it is, we print a different message. Otherwise, we print a third message. We also use a conditional expression to assign a value to the `result` variable based on whether `x` is even or odd.

## For loops and looping structures


    let numbers = [1, 2, 3, 4, 5];
    for number in numbers.iter().rev() {
        println!("{}", number);
    }

    let mut counter = 0;
    while counter < 10 {
        counter += 1;
        println!("{}", counter);
    }

    let mut option = Some(5);
    while let Some(x) = option {
        println!("{}", x);
        option = if x > 0 { Some(x - 1) } else { None };
    } 

In this example, we use a for loop to iterate over the `numbers` array in reverse order and print each number to the console. We also use a while loop to repeatedly print the value of `counter` to the console until it reaches 10. Finally, we use a while let loop to repeatedly print the value of the `option` variable until it becomes `None`.

## Match expressions


    let x = 3;
    match x {
        1 | 2 => println!("x is less than or equal to 2"),
        3 | 4 | 5 => println!("x is between 3 and 5"),
        n if n % 2 == 0 => println!("x is an even number"),
        n if n % 2 != 0 => println!("x is an odd number"),
        _ => println!("x is something else"),
    }

In this example, we use a match expression to compare the value of `x` against several patterns. If `x` is less than or equal to 2, we print a message to the console. If `x` is between 3 and 5, we print a different message. If `x` is an even number, we print another message. If `x` is an odd number, we print yet another message. Finally, if `x` does not match any of the other patterns, we print a default message using the underscore pattern.

## Conclusion

In this lesson, we have learned about the different types of control structures in Rust, including if statements, conditional expressions, for loops, and match expressions. These control structures are essential for controlling the flow of a program and making decisions based on certain conditions. By understanding these control structures, you are now ready to move on to the next lesson and learn about functions in Rust.