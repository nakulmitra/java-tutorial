# Detailed Theory on throw and throws Keywords in Java
In Java, the `throw` and `throws` keywords play an essential role in exception handling by providing developers with control over how exceptions are raised and propagated through a program. These two keywords work together to make the code more robust, flexible, and easier to debug.

This document will give a comprehensive overview of both keywords, how to use them effectively, and their real-world use cases, with complete code examples.

[![](https://markdown-videos-api.jorgenkh.no/youtube/2e2HgCt1Xag)](https://youtu.be/2e2HgCt1Xag)

## What is the throw Keyword?
The `throw` keyword is used to explicitly throw an exception from a method or block of code. This keyword allows you to raise exceptions based on specific conditions, giving developers control over the flow of their application.

How it Works:
* When `throw` is encountered in a program, the execution stops at that point.
* The exception is then **propagated** up the call stack until it is caught by a **try-catch block** or **terminates the program**.

### Syntax
```
throw new ExceptionType("Error Message");
```
* `ExceptionType` is the type of exception being thrown (e.g., `ArithmeticException`, `IOException`).
* A new instance of the exception is created with an optional message.

### Example: Using throw for Age Validation
In this example, the `throw` keyword raises an `ArithmeticException` if the provided age is less than 18.
```
public class Main {
    public static void main(String[] args) {
        validateAge(15);  // This will throw an exception
    }

    public static void validateAge(int age) {
        if (age < 18) {
            throw new ArithmeticException("Not eligible to vote.");
        } else {
            System.out.println("Eligible to vote.");
        }
    }
}
```

### Explanation:
* `Condition Check:` The `validateAge` method checks if the input age is less than 18.
* `Throwing Exception:` If the condition is met, it throws an `ArithmeticException` with the message "Not eligible to vote."
* `Handling the Exception:` If no catch block handles this exception, the program terminates with an error message.

This example demonstrates how `throw` gives developers control over when exceptions are raised based on certain conditions.

### Common Use Cases for throw
* `Input Validation:` Throw exceptions when invalid data is detected, like an invalid age or negative value.
* `Custom Exceptions:` Raise custom exceptions to provide more meaningful error messages.
* `Manual Error Handling:` Manually raise an exception to stop further execution when the program encounters a critical condition.

## What is the throws Keyword?
The `throws` **keyword** is used in the method signature to declare the types of exceptions that a method might throw. It **informs the calling method** that it must either handle these exceptions or propagate them further up the call stack.

### How it Works:
* `throws` allows a method to declare multiple exceptions it might throw.
* It shifts the responsibility of exception handling to the **calling method**.

### Syntax
```
public void methodName() throws ExceptionType1, ExceptionType2 {
    // Method implementation
}
```
* `ExceptionType1`, `ExceptionType2` are the exceptions that this method might throw.

### Example: Using throws for File Handling
In this example, the `throws` keyword declares that the `readFile` method might throw an `IOException` if the file is not found or there’s an issue reading it.
```
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        readFile("file.txt");  // Handle or propagate the exception
    }

    public static void readFile(String fileName) throws IOException {
        BufferedReader br = new BufferedReader(new FileReader(fileName));
        System.out.println(br.readLine());
        br.close();
    }
}
```

### Explanation:
* `Method Declaration:` The `readFile` method declares `throws IOException`, indicating it might throw an `IOException`.
* `Calling Method Responsibility:` The `main` method propagates the exception by also declaring `throws IOException` in its signature.
* `Exception Handling:` If the exception is not handled, the program will terminate with an appropriate error message.

This example shows how `throws` shifts responsibility for handling exceptions to the calling method.

### Common Use Cases for throws
* `File Operations:` Declaring exceptions like `IOException` for reading or writing files.
* `Database Connections:` Propagating `SQLException` if a database operation fails.
* `Thread Operations:` Declaring `InterruptedException` for methods dealing with concurrency.

## Difference Between throw and throws
| throw | throws |
| ----------------|---------|
|  Used within the method to raise an exception |  Declares exceptions a method might throw  |
|  Follows by creating a new exception object using new |  Appears in the method signature  |
|  Example: throw new IOException("Error"); |  Example: public void method() throws IOException  |
|  Used to manually signal exceptions  | Delegates responsibility for exception handling to the calling method |

## Using throw and throws Together
```
import java.io.*;

class CustomFileReader {
    public void readFile(String fileName) throws IOException {
        // If file not found, throw IOException
        BufferedReader br = new BufferedReader(new FileReader(fileName));
        System.out.println(br.readLine());
        br.close();
    }
}

public class Main {
    public static void main(String[] args) {
        CustomFileReader reader = new CustomFileReader();
        try {
            reader.readFile("non_existent_file.txt");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```
### Explanation
* The `throws` **keyword** in the `readFile` method declares the potential `IOException`.
* The `throw` **keyword** inside the method raises the exception if the file is not found.
* In the `main` **method**, the exception is **caught and handled** using a try-catch block.

## Key Takeaways
* `throw` is used within a method to **manually raise an exception** based on specific conditions.
* `throws` declares exceptions that a method might throw, delegating the responsibility to the calling method.
* Both `throw` and `throws` are essential tools for creating **robust and maintainable code**.

## Common Exceptions in Java
* `IOException:` Input/Output operation failure.
* `SQLException:` Issues with SQL database operations.
* `ArithmeticException:` Division by zero or mathematical error.
* `NullPointerException:` Attempt to access an object that has not been initialized.

## Conclusion
* `throw` is used to **manually raise exceptions** based on specific conditions.
* `throws` is used to **declare exceptions** that a method might throw.

Both keywords work together to give developers **more control over exception handling** and ensure **clean code with well-defined error handling mechanisms**.
