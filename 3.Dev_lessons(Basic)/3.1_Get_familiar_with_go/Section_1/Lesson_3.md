# Lesson 3: Control Structures in Go

## Overview:

In this lesson, we will cover control structures in Go, including if statements and conditional expressions, loops and looping structures, and switch statements.

## Lesson Objectives:

By the end of this lesson, you should be able to:

-   Understand how to use if statements and conditional expressions in Go.
-   Use for loops and looping structures in Go.
-   Understand how to use switch statements in Go.

## Topics Covered:

-   If statements and conditional expressions
-   For loops and looping structures
-   Switch statements

## 1\. If Statements and Conditional Expressions

If statements are used in Go to execute a block of code if a certain condition is met. A simple if statement looks like this:


    if condition {
        // code to execute if condition is true
    }

Here's an example:

    package main

    import "fmt"

    func main() {
        x := 10
        if x > 5 {
            fmt.Println("x is greater than 5")
        }
    } 

In this example, the code inside the if statement will only execute if the condition `x > 5` is true. In this case, the output will be "x is greater than 5".

Conditional expressions are a shorthand way of writing if statements. They are often used when you want to assign a value to a variable based on a condition. Here's an example:


    package main

    import "fmt"

    func main() {
        x := 10
        message := ""
        if x > 5 {
            message = "x is greater than 5"
        } else {
            message = "x is less than or equal to 5"
        }
        fmt.Println(message)
    }

In this example, the conditional expression `x > 5` is evaluated. If it is true, the value of `message` is set to "x is greater than 5". Otherwise, the value of `message` is set to "x is less than or equal to 5". The output will be "x is greater than 5".

## 2\. For Loops and Looping Structures

In Go, for loops are used to execute a block of code repeatedly. The basic syntax of a for loop in Go is as follows:


    for initialization; condition; increment {
        // code block to be executed
    }

Here's an example of a for loop that prints the numbers from 0 to 4:


    package main

    import "fmt"

    func main() {
        for i := 0; i < 5; i++ {
            fmt.Println(i)
        }
    }

In this example, the initialization statement `i := 0` sets the initial value of the loop counter to 0. The condition `i < 5` is checked before each iteration of the loop. If the condition is true, the code block inside the loop is executed. After each iteration of the loop, the increment statement `i++` is executed, which increments the value of `i` by 1.

In addition to the basic for loop, Go provides several other looping structures, such as the while loop and the do-while loop. Here's an example of a while loop that prints the numbers from 0 to 4:


    package main

    import "fmt"

    func main() {
        i := 0
        for i < 5 {
            fmt.Println(i)
            i++
        }
    }

In this example, the condition `i < 5` is checked before each iteration of the loop, and the loop continues as long as the condition is true. The code block inside the loop is executed once per iteration.

Go does not have a built-in do-while loop, but you can simulate a do-while loop using a for loop and a break statement. Here's an example of a do-while loop that prints the numbers from 0 to 4:


    package main

    import "fmt"

    func main() {
        i := 0
        for {
            fmt.Println(i)
            i++
            if i == 5 {
                break
            }
        }
    }

In this example, the for loop has no initialization statement and no condition. The loop will execute indefinitely until the break statement is encountered. The code block inside the loop is executed once per iteration.

## 3\. Switch Statements

Switch statements are used in Go to execute different blocks of code depending on the value of an expression. Here's an example:


    package main

    import "fmt"

    func main() {
        x := 2
        switch x {
        case 1:
            fmt.Println("x is 1")
        case 2:
            fmt.Println("x is 2")
        default:
            fmt.Println("x is not 1 or 2")
        }
    } 

In this example, the expression `x` is evaluated and compared to each case value. If `x` is equal to 1, the first block of code is executed. If `x` is equal to 2, the second block of code is executed. If `x` is not equal to 1 or 2, the default block of code is executed. The output will be "x is 2".

Switch statements can also be used without an expression to create more complex control structures. Here's an example:

    package main

    import "fmt"

    func main() {
        x := 2
        switch {
        case x > 5:
            fmt.Println("x is greater than 5")
        case x < 5:
            fmt.Println("x is less than 5")
        default:
            fmt.Println("x is equal to 5")
        }
    } 

In this example, the switch statement has no expression. Instead, each case statement contains a condition. The first case statement is executed if `x` is greater than 5, the second case statement is executed if `x` is less than 5, and the default statement is executed if `x` is equal to 5. The output will be "x is less than 5".

## Conclusion

Control structures are an important part of any programming language, and Go provides several powerful control structures for controlling the flow of your code. In this lesson, we covered if statements and conditional expressions, for loops and looping structures, and switch statements. By mastering these control structures, you will be able to write more complex and powerful programs in Go.