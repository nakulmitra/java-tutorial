# Introduction
In Java, multithreading allows concurrent execution of two or more parts of a program to maximize CPU utilization. The Java platform provides multiple ways to create and manage threads, each with its pros and cons. This guide explores **three approaches to creating threads**:

1. **Extending the `Thread` class**
2. **Implementing the `Runnable` interface**
3. **Using `Callable` and `Future` for returning results from threads**

Let's dive deep into each approach with examples and key takeaways.

## 1. Creating Threads by Extending the Thread Class
The simplest way to create a thread in Java is by **extending the `Thread` class** and overriding the `run()` method.

### How It Works
- The `Thread` class is available in the `java.lang` package.
- We override the `run()` method to define the task to be executed in the new thread.
- The `start()` method is used to initiate the thread execution.

### Example: Extending `Thread` Class
```
// Step 1: Create a thread by extending Thread class
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - Count: " + i);
            try {
                Thread.sleep(1000); // some work
            } catch (InterruptedException e) {
                System.out.pritln("Inside catch block due to " + Thread.currentThread().getName());
            }
        }
    }
}

// Step 2: Run the thread
public class Main {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        MyThread thread2 = new MyThread();

        thread1.start(); // Starts thread1
        thread2.start(); // Starts thread2
    }
}
```

### Output (Example Execution)
```
Thread-0 - Count: 1  
Thread-1 - Count: 1  
Thread-0 - Count: 2  
Thread-1 - Count: 2  
...

```

### Key Takeaways
* Simple to implement.
* Each thread runs independently.
* The `run()` method defines the task logic.
* Call `start()` instead of `run()` to execute in a separate thread.
* **Limitation:** Java supports single inheritance, meaning a class cannot extend another class if it already extends `Thread`.

## Creating Threads by Implementing the Runnable Interface
A more flexible way to create threads is by implementing the `Runnable` interface.

### Why Use `Runnable` Instead of `Thread`?
- Java **does not support multiple inheritance**, so extending `Thread` prevents a class from extending another class.
- `Runnable` **allows better separation of concerns** by defining the task separately from the execution mechanism.
- It's the **preferred approach** in most cases.

### Example: Implementing `Runnable`
```
// Step 1: Create a class that implements Runnable
class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - Count: " + i);
            try {
                Thread.sleep(1000); //some work
            } catch (InterruptedException e) {
                System.out.pritln("Inside catch block due to " + Thread.currentThread().getName());
            }
        }
    }
}

// Step 2: Create Thread objects
public class Main {
    public static void main(String[] args) {
        MyRunnable task = new MyRunnable(); // Runnable instance

        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        thread1.start(); // Starts thread1
        thread2.start(); // Starts thread2
    }
}
```

### Output (Example Execution)
```
Thread-0 - Count: 1  
Thread-1 - Count: 1  
Thread-0 - Count: 2  
Thread-1 - Count: 2  
...

```

### Key Takeaways
* Preferred approach as it allows **multiple inheritance**.
* Separates **task definition** (`Runnable`) from **execution mechanism** (`Thread`).
* The `run()` method still defines the task logic.
* The `Runnable` instance is passed to a `Thread` object.
* Call `start()` instead of `run()` to execute in a separate thread.

## Using Callable and Future (Returning Results from Threads)
The `Runnable` interface is useful but **cannot return a result**. If a thread needs to return a value, Java provides the `Callable` and `Future` interfaces.

### Why Use `Callable` Instead of `Runnable`?
- Unlike `Runnable`, `Callable<T>` **returns a result**.
- `Callable` **throws checked exceptions**, making error handling more robust.
- It works with **`Future`** to retrieve results asynchronously.

### Example: Using `Callable` and `Future`
```
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

// Step 1: Create a Callable class
class MyCallable implements Callable<Integer> {
    @Override
    public Integer call() throws Exception {
        int sum = 0;
        for (int i = 1; i <= 5; i++) {
            sum += i;
            Thread.sleep(100); // some work
        }
        return sum; // Returning the sum of first 5 numbers
    }
}

// Step 2: Execute the Callable task using ExecutorService
public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(new MyCallable());

        try {
            // Retrieving the result
            Integer result = future.get();
            System.out.println("Sum: " + result);
        } catch (InterruptedException | ExecutionException e) {
            System.out.pritln("Inside catch block!!!");
        }

        executor.shutdown();
    }
}
```

### Output
```
Sum: 15
```

### Key Takeaways
* `Callable` is similar to `Runnable`, but it **can return a result**.
* The `call()` method executes the logic and **returns a value**.
* `Future` is used to **retrieve the result asynchronously**.
* `ExecutorService` manages the execution of `Callable` tasks.

## Summary

| Approach  | Features | Use Case |
|-----------|----------|----------|
| **Extending `Thread` Class** | Simple, easy to use, but lacks flexibility due to single inheritance. | When you need a quick implementation and do not require extending another class. |
| **Implementing `Runnable`** | Preferred approach, allows multiple inheritance, separates task logic from execution. | When you need reusable task execution without returning a result. |
| **Using `Callable` & `Future`** | Supports returning results, asynchronous execution, and exception handling. | When you need to return a result from a thread or handle exceptions. |

## When to Use What?
* Use **Thread class:** When you need a simple, standalone thread.
* Use **Runnable:** When you need flexibility and separation of concerns.
* Use **Callable & Future:** When you need a result from a thread.


[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/multithreading/introduction.md)