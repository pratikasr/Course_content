# Lesson 8: Concurrency in Rust

Concurrency is an important topic in modern programming, and Rust provides powerful tools for working with concurrent code. In this lesson, we will explore the basics of concurrency in Rust, including threads, channels, race conditions, and synchronization.

## Introduction to Concurrency in Rust

Concurrency is the ability of a program to execute multiple tasks or processes simultaneously. In Rust, concurrency is achieved through the use of threads, which allow multiple sections of a program to run in parallel.

Rust's concurrency model is based on the concept of ownership and borrowing, which we have already discussed in previous lessons. Rust's ownership model ensures that each piece of data has a single owner, and this owner is responsible for managing the lifetime of the data. This makes it easier to reason about concurrent code and prevents many common concurrency bugs, such as data races and deadlocks.

## Using Threads and Channels

In Rust, threads are created using the `std::thread` module. Here is an example of how to create a new thread:


    use std::thread;

    fn main() {
        let handle = thread::spawn(|| {
            println!("Hello from a new thread!");
        });

        handle.join().unwrap();
    } 

This code creates a new thread using the `thread::spawn` function and passes in a closure that contains the code to be executed in the new thread. The `join` method is used to wait for the thread to finish executing.

In addition to threads, Rust also provides channels for communication between threads. Channels are created using the `std::sync::mpsc` module, which stands for "multiple producer, single consumer". Here is an example of how to use channels:


    use std::sync::mpsc;
    use std::thread;

    fn main() {
        let (tx, rx) = mpsc::channel();

        thread::spawn(move || {
            tx.send("Hello from a thread!").unwrap();
        });

        let msg = rx.recv().unwrap();
        println!("{}", msg);
    } 

This code creates a channel using the `mpsc::channel` function and passes the sender and receiver ends of the channel to separate threads. The `send` method is used to send a message through the channel, and the `recv` method is used to receive the message on the other end of the channel.

## Understanding Race Conditions and Synchronization

In concurrent programming, race conditions occur when multiple threads access and modify the same shared data concurrently, resulting in an unexpected outcome. Synchronization is a technique used to avoid race conditions and ensure that multiple threads can safely access and modify shared data.

Rust provides several synchronization primitives such as mutexes, semaphores, and channels to manage concurrency and prevent race conditions. Mutexes are a type of lock that allows only one thread to access shared data at a time, while semaphores can be used to limit the number of threads that can access shared data simultaneously. Channels provide a safe way to transfer data between threads, ensuring that only one thread can access the data at a time.

Understanding race conditions and synchronization is critical for writing correct and efficient concurrent programs in Rust. It is essential to design concurrent programs carefully, identifying potential race conditions and using appropriate synchronization techniques to prevent them.

Let's consider an example of a program that maintains a counter that can be incremented or decremented by multiple threads concurrently. Without proper synchronization, race conditions can occur, resulting in unexpected outcomes.


    use std::sync::{Arc, Mutex};
    use std::thread;

    fn main() {
        let counter = Arc::new(Mutex::new(0)); // create a shared counter protected by a mutex
        let mut handles = vec![]; // vector to store thread handles

        for _ in 0..10 {
            let counter_clone = Arc::clone(&counter); // create a clone of the shared counter
            let handle = thread::spawn(move || {
                let mut value = counter_clone.lock().unwrap(); // acquire the mutex lock and get the counter value
                *value += 1; // increment the counter
            });
            handles.push(handle); // store the thread handle in the vector
        }

        for handle in handles {
            handle.join().unwrap(); // wait for all threads to finish
        }

        println!("Counter value: {}", *counter.lock().unwrap()); // print the final counter value
    } 

In this example, we create a shared counter protected by a `Mutex`. We then spawn 10 threads that each increment the counter value. Without proper synchronization, race conditions can occur when multiple threads try to modify the counter value simultaneously.

To prevent race conditions, we use a `Mutex` to protect the counter and ensure that only one thread can access and modify it at a time. The `lock()` method is used to acquire the lock, and the `unwrap()` method is used to get the counter value.

After all the threads finish, we print the final counter value. The output should be 10, which is the expected value after incrementing the counter 10 times.

This example demonstrates the importance of proper synchronization and the use of synchronization primitives like `Mutex` to prevent race conditions in concurrent programs.