## Lesson: Basic syntax and data types in Go

### Introduction:

Go is a statically typed programming language designed to make it easy to build efficient and scalable software. In this lesson, we will learn about the basic syntax and data types in Go.

### 1\. Hello World program in Go

Let's start by creating a "Hello World" program in Go. Open your favorite text editor and type the following code:


    package main

    import "fmt"

    func main() {
        fmt.Println("Hello, World!")
    }

Save the file with a `.go` extension, for example, `hello.go`. Open your terminal or command prompt and navigate to the directory where you saved the file. Run the following command to compile and run the program:

`go run hello.go` 

You should see the message "Hello, World!" printed on the screen. Congratulations, you have written your first Go program!

### 2\. Variables

Variables are used to store values in Go. In Go, you need to declare the type of the variable before using it. Here's an example:


    package main

    import "fmt"

    func main() {
        var x int = 10
        var y float32 = 2.5
        var message string = "Hello, World!"

        fmt.Println(x)
        fmt.Println(y)
        fmt.Println(message)
    }

In this example, we have declared three variables of different types: `x` (`int`), `y` (`float32`), and `message` (`string`). We have assigned values to these variables and printed them using the `fmt.Println` function.

You can also declare variables without specifying their type, and Go will infer the type based on the value you assign to them:


    package main

    import "fmt"

    func main() {
        x := 10
        y := 2.5
        message := "Hello, World!"

        fmt.Println(x)
        fmt.Println(y)
        fmt.Println(message)
    }

### 3\. Data Types

Go has several built-in data types. Let's take a look at some of the most common ones:

-   `int`: used to represent integer values (e.g., 0, 1, 2, -1, -2)
-   `float32`, `float64`: used to represent floating-point values (e.g., 1.0, 2.5, -3.1415)
-   `bool`: used to represent boolean values (`true` or `false`)
-   `string`: used to represent text strings (e.g., "Hello, World!")

Go also has several other data types, such as arrays, slices, maps, and structs. We will cover these in more detail in later lessons.

### 4\. Operators

Go supports several operators that allow you to perform arithmetic, logical, and comparison operations. Here are some of the most common operators:

-   Arithmetic operators: `+`, `-`, `*`, `/`, `%`
-   Comparison operators: `==`, `!=`, `<`, `<=`, `>`, `>=`
-   Logical operators: `&&`, `||`, `!`

Here's an example that shows how to use these operators:


    package main

    import "fmt"

    func main() {
        x := 10
        y := 5

        fmt.Println(x + y) // prints 15
        fmt.Println(x - y) // prints 5
        fmt.Println(x * y) // prints 50
        fmt.Println(x / y) // prints 2
        fmt.Println(x % y) // prints 0
        fmt.Println(x == y) // prints false
        fmt.Println(x != y) // prints true
        fmt.Println(x < y) // prints false
        fmt.Println(x <= y) // prints false
        fmt.Println(x > y) // prints true
        }

Go also supports the standard comparison operators, including `==`, `!=`, `<`, `>`, `<=`, and `>=`. Here's an example of using these operators in Go:

yamlCopy code

`a := 5
b := 7
fmt.Println(a == b)   // Output: false
fmt.Println(a != b)   // Output: true
fmt.Println(a < b)    // Output: true
fmt.Println(a > b)    // Output: false
fmt.Println(a <= b)   // Output: true
fmt.Println(a >= b)   // Output: false` 

## Conclusion

In this lesson, we covered the basic syntax and data types in Go, how to declare and initialize variables, and how to use basic operators. This is the foundation you'll need to write Go programs, so make sure you're comfortable with these concepts before moving on to more complex topics.