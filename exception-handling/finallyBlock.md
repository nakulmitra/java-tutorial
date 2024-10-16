# Detailed Theory on Finally Block in Java
This repository contains a detailed explanation of the `finally` **block** in Java, including code examples and best practices. The `finally` block plays a key role in **exception handling** by ensuring that **cleanup operations** are always executed, regardless of whether an exception occurs. This documentation covers everything you need to know about using finally blocks and modern alternatives like **try-with-resources**.

## What is the Finally Block in Java?
The `finally` block is a crucial component of **Java's exception handling mechanism**. It is used to execute **code after the try-catch blocks**, regardless of whether an exception occurred.
* `Purpose:` Perform cleanup operations, such as **closing files**, **releasing memory**, or **disconnecting from a database**.
* `Execution Guarantee:` The `finally` block **always runs** after the try-catch block, even if an exception is thrown or the program exits prematurely.

### Example of try-catch-finally
```
public class Main {
    public static void main(String[] args) {
        try {
            int result = 50 / 2;  // No exception, runs smoothly
            System.out.println("Result: " + result);
        } catch (Exception e) {
            System.out.println("Error occurred.");
        } finally {
            System.out.println("This will always execute.");
        }
    }
}
```
### Explanation:
* `Try Block:` Contains code that may throw an exception.
* `Catch Block:` Handles the exception if one is thrown.
* `Finally Block:` Runs regardless of whether an exception was thrown or handled.

### Output
```
Result: 25
This will always execute.
```

If an **exception occurs** (like dividing by zero), the `finally` block **still runs**.

## Why Use the Finally Block?
The finally block is essential for cleanup tasks, such as:
* Closing files or network connections.
* Releasing database connections.
* Cleaning up temporary data to prevent resource leaks.

### Closing a File with Finally Block
```
import java.io.*;

public class Main {
    public static void main(String[] args) {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader("test.txt"));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        } finally {
            // Always close the BufferedReader
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    System.out.println("Error closing reader: " + e.getMessage());
                }
            }
            System.out.println("BufferedReader is closed.");
        }
    }
}
```
### Explanation
* If an exception occurs during **file reading**, the `finally` block ensures the **BufferedReader is closed**.
* This prevents **resource leaks** that could happen if resources are not released.

## Try-With-Resources
Introduced in **Java 7**, the **try-with-resources** statement automatically closes resources, simplifying the code and removing the need for `finally` in many cases.

### Example
```
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("test.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```
### Explanation
* The **resource (BufferedReader)** is created inside the try block's parentheses.
* Java ensures that the resource is **automatically closed** after the try block completes, whether an exception occurs or not.
* This makes the code **cleaner** and **less error-prone**.

## When to Use the Finally Block
While try-with-resources is preferred for managing resources, the `finally` block is still necessary for:
* `Non-closable resources:` Releasing locks or other temporary resources.
* `Custom cleanup:` Deleting temporary files or resetting states.
* `Debugging and Logging:` Printing logs before a program exits.

## Key Differences Between Finally Block and Try-With-Resources


## Summary
To wrap up, the `finally` block ensures that critical cleanup code always runs, regardless of whether an exception is thrown. It is an essential part of exception handling in Java.
* Use `finally` when dealing with non-closable resources or custom cleanup tasks.
* Use try-with-resources when working with resources that need to be closed automatically (like files or database connections).

## Conclusion
The **finally block** in Java is a powerful tool for **resource management and error handling**. While the **try-with-resources** statement has simplified resource management, the `finally` block remains relevant for handling non-closable resources and custom cleanup tasks.