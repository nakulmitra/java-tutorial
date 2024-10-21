# Custom Exceptions in Java
In Java, exceptions are a way to handle unexpected events or errors that disrupt the normal flow of the program. While Java provides built-in exceptions like `NullPointerException`, `IOException`, and `ArithmeticException`, sometimes domain-specific exceptions are needed to provide better clarity and control.

This guide explains how to create and use custom exceptions to handle application-specific scenarios efficiently.

## Why Create Custom Exceptions?
Built-in exceptions are general-purpose and may not be suitable for specific business logic. Custom exceptions allow:
* `Domain-specific clarity:` Help describe what exactly went wrong.
* `Improved debugging:` Provide more contextual information, such as **error codes** or detailed messages.
* `Cleaner code:` Avoid cluttered logic by catching and handling specific exceptions elegantly.

## Use Case Example
Consider a **banking application**. If a user tries to **withdraw more than their balance**, a generic `Exception` or `ArithmeticException` might not convey the specific issue clearly. A custom `InsufficientBalanceException` makes it easier to manage this case explicitly.

## How to Create a Custom Exception in Java?
In Java, a custom exception is created by extending the `Exception` class (for checked exceptions) or `RuntimeException` class (for unchecked exceptions). Below are the steps involved.

### Step 1: Create a Custom Exception Class
```
// Custom exception class
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);  // Call the parent class constructor with the message
    }
}
```
This `InsufficientBalanceException` class extends `Exception` to indicate it is a **checked exception**, requiring the caller to either **handle** it or **declare it using throws**.

### Step 2: Using the Custom Exception in Code
Let’s apply the custom exception to simulate **bank withdrawals** in a `BankAccount` class.
```
public class BankAccount {
    private double balance;

    // Constructor to initialize balance
    public BankAccount(double balance) {
        this.balance = balance;
    }

    // Withdraw method that may throw a custom exception
    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException(
                "Insufficient balance! You tried to withdraw: " + amount);
        }
        balance -= amount;
        System.out.println("Withdrawal successful. Remaining balance: " + balance);
    }

    public static void main(String[] args) {
        BankAccount account = new BankAccount(500);
        try {
            account.withdraw(600);  // Attempting to withdraw more than the balance
        } catch (InsufficientBalanceException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```
#### Explanation:
* **Constructor** initializes the account balance.
* `withdraw` **method** checks if the requested amount is greater than the available balance.
* If yes, it **throws the custom** `InsufficientBalanceException`.
* In the `main` method, the custom exception is **caught and handled** gracefully, preventing program crashes.

## Enhancing Custom Exceptions with Additional Information
Sometimes, we may want to **pass more data** with an exception, such as **error codes** for logging or **detailed messages** for better debugging.
```
// Enhanced custom exception with an error code
class InsufficientBalanceException extends Exception {
    private int errorCode;  // Additional field for error code

    public InsufficientBalanceException(String message, int errorCode) {
        super(message);
        this.errorCode = errorCode;
    }

    // Getter method to retrieve the error code
    public int getErrorCode() {
        return errorCode;
    }
}
```
Now, let’s use this **enhanced custom exception** in the `BankAccount` class.

```
public class BankAccount {
    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException(
                "Insufficient balance!", 101);  // 101: Error code for balance issues
        }
        balance -= amount;
        System.out.println("Withdrawal successful. Remaining balance: " + balance);
    }

    public static void main(String[] args) {
        BankAccount account = new BankAccount(500);
        try {
            account.withdraw(600);  // Withdrawal attempt with insufficient balance
        } catch (InsufficientBalanceException e) {
            System.out.println("Error: " + e.getMessage() +
                               " | Error Code: " + e.getErrorCode());
        }
    }
}
```
### Explanation:
* We added an **errorCode field** to the custom exception class for better logging or debugging.
* The **error code and message** are both passed when the exception is thrown.
* The **getter method** retrieves the error code to display it alongside the message.

## When to Use Custom Exceptions?
* `Domain-Specific Errors:` Use custom exceptions when built-in exceptions are too generic (e.g., `InsufficientBalanceException`).
* `Improving Code Readability:` Clearly communicate the cause of an error to other developers and users.
* `Error Codes and Context:` Add error codes and extra fields to enhance error tracking and logging.

## Best Practices for Custom Exceptions
* `Extend the appropriate class:` Use `Exception` for **checked exceptions** and `RuntimeException` for **unchecked exceptions**.
* `Meaningful Error Messages:` Provide clear and concise error messages in custom exceptions.
* `Use when necessary:` Avoid overusing custom exceptions—only create them when the logic demands it.
* `Follow Naming Conventions:` Name custom exceptions meaningfully, ending with "Exception" (e.g., `InsufficientBalanceException`).

## Conclusion
In this tutorial, we learned:
* How to create **custom exceptions** by extending Java's built-in `Exception` class.
* The advantages of using custom exceptions for **domain-specific** errors.
* How to **enhance exceptions** by adding **fields like error** codes for better tracking.
* Best practices for using custom exceptions effectively.

Custom exceptions help make your code **more maintainable**, **readable**, and **easier to debug**. They give you **control over error handling** in ways that built-in exceptions may not provide.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/exception-handling/throw-and-throws.md)