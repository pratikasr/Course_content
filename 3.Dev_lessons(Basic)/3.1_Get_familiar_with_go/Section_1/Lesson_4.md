# Lesson 4: Functions in Go

## Overview

In this lesson, we will cover functions in Go, including how to declare and call functions, pass arguments to functions, and return values from functions.

## Lesson Objectives

By the end of this lesson, you should be able to:

-   Understand how to declare and call functions in Go.
-   Pass arguments to functions in Go.
-   Return values from functions in Go.

## Topics Covered

-   Declaring and calling functions
-   Passing arguments to functions
-   Returning values from functions

## Declaring and Calling Functions

Functions in Go are declared using the `func` keyword followed by the function name and the parameter list enclosed in parentheses. If the function returns a value, the return type is specified after the parameter list.

Here is an example of a function that takes two integer arguments and returns their sum:


    func add(x int, y int) int {
        return x + y
    } 

To call this function, you simply provide the arguments in the order they are declared in the function definition:


    sum := add(3, 5)
    fmt.Println(sum) // Output: 8 

## Passing Arguments to Functions

In Go, function arguments can be passed by value or by reference. By value means that a copy of the value is passed to the function, while by reference means that a reference to the original value is passed to the function.

Here is an example of a function that takes a slice of integers and modifies it in place:


    func doubleValues(values []int) {
        for i := 0; i < len(values); i++ {
            values[i] *= 2
        }
    } 

To call this function, you simply pass a slice of integers:


    numbers := []int{1, 2, 3, 4}
    doubleValues(numbers)
    fmt.Println(numbers) // Output: [2 4 6 8] 

Note that since slices are reference types in Go, the function modifies the original slice.

## Returning Values from Functions

In Go, functions can return multiple values. The return type is specified after the parameter list, and the values are separated by commas in the return statement.

Here is an example of a function that returns both the minimum and maximum values of a slice of integers:


    func minMaxValues(values []int) (int, int) {
        min, max := values[0], values[0]
        for _, v := range values {
            if v < min {
                min = v
            }
            if v > max {
                max = v
            }
        }
        return min, max
    } 

To call this function, you can assign the return values to variables:

goCopy code

    numbers := []int{5, 2, 9, 1, 7}
    min, max := minMaxValues(numbers)
    fmt.Printf("Min: %d, Max: %d\n", min, max) // Output: Min: 1, Max: 9 

## Conclusion

In this lesson, we covered the basics of functions in Go, including how to declare and call functions, pass arguments to functions, and return values from functions. With this knowledge, you should be able to write your own functions and use them in your Go programs.