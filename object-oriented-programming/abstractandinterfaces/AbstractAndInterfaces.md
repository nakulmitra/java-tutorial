# Using Abstract Classes and Interfaces Together in Java
In Java, abstract classes and interfaces serve distinct but complementary roles in object-oriented design. Abstract classes are used to define common behavior that can be shared among related classes, while interfaces provide a way to enforce specific behaviors across unrelated classes. By using both together, we can create flexible and scalable systems.

## Real-World Example: Payment Processing System
Imagine we are building a **Payment Processing System** with various payment methods such as **Credit Card**, **PayPal**, and **Bank Transfer**. Some payment methods support refunds, while others do not. We can use abstract classes to define the core payment behavior and interfaces to define additional behaviors like refunds.

[![](https://markdown-videos-api.jorgenkh.no/youtube/jXSn3jlNkMI)](https://youtu.be/jXSn3jlNkMI)

## Abstract Class for Core Payment Logic
First, we define an abstract class called `Payment`, which will serve as the base class for all payment methods. The `Payment` class will contain common payment logic, such as processing the payment and showing the amount.

```
abstract class Payment {
    double amount;
    
    Payment(double amount) {
        this.amount = amount;
    }

    // Abstract method that must be implemented by subclasses
    abstract void processPayment();

    // Concrete method with common functionality
    void showAmount() {
        System.out.println("Processing payment of: $" + amount);
    }
}
```

The `Payment` class has an abstract method `processPayment()`, which will be implemented by subclasses. It also has a concrete method `showAmount()` to display the payment amount, common to all payment methods.

## Interface for Refund Behavior
Next, we define an interface `Refundable` for payment methods that support refunds. This interface contains a method `processRefund()` that must be implemented by classes supporting refunds.
```
interface Refundable {
    void processRefund(double amount);
}
```

## Implementing Concrete Payment Methods
Now, let's implement the payment methods. The CreditCard class extends the `Payment` abstract class and implements the `Refundable` interface because it supports refunds.
```
class CreditCard extends Payment implements Refundable {
    CreditCard(double amount) {
        super(amount);
    }

    @Override
    void processPayment() {
        System.out.println("Processing credit card payment of: $" + amount);
    }

    @Override
    public void processRefund(double amount) {
        System.out.println("Refunding credit card payment of: $" + amount);
    }
}
```
In the `CreditCard` class, we provide implementations for both the `processPayment()` and `processRefund()` methods.
For **PayPal**, we only need to extend the `Payment` class, as PayPal does not support refunds in this example:

```
class PayPal extends Payment {
    PayPal(double amount) {
        super(amount);
    }

    @Override
    void processPayment() {
        System.out.println("Processing PayPal payment of: $" + amount);
    }
}
```

## Example of Using the Payment System
We can now create instances of different payment methods and process payments. If a payment method supports refunds, we can cast it to the `Refundable` interface and call the `processRefund()` method.

```
public class Main {
    public static void main(String[] args) {
        Payment payment1 = new CreditCard(100.0);
        payment1.processPayment();
        ((Refundable) payment1).processRefund(100.0);

        Payment payment2 = new PayPal(200.0);
        payment2.processPayment();
    }
}
```
In this example:
* We process a credit card payment and issue a refund by casting the `CreditCard` object to the `Refundable` interface.
* We process a PayPal payment, but since PayPal does not support refunds, we don’t call the `processRefund()` method.

## Adding Another Payment Method: Bank Transfer
Let’s add another payment method: **BankTransfer**, which supports refunds like the `CreditCard` class.
```
class BankTransfer extends Payment implements Refundable {
    BankTransfer(double amount) {
        super(amount);
    }

    @Override
    void processPayment() {
        System.out.println("Processing bank transfer payment of: $" + amount);
    }

    @Override
    public void processRefund(double amount) {
        System.out.println("Refunding bank transfer payment of: $" + amount);
    }
}
```

## Updated Main Method with BankTransfer
```
public class Main {
    public static void main(String[] args) {
        Payment payment1 = new CreditCard(100.0);
        payment1.processPayment();
        ((Refundable) payment1).processRefund(100.0);

        Payment payment2 = new PayPal(200.0);
        payment2.processPayment();

        Payment payment3 = new BankTransfer(300.0);
        payment3.processPayment();
        ((Refundable) payment3).processRefund(300.0);
    }
}
```

### Key Takeaways
* **Abstract Classes** are used to define common behavior that can be shared among related classes.
* **Interfaces** provide a way to enforce certain behaviors across unrelated classes.
* By combining abstract classes and interfaces, we can create more flexible and extensible systems. In our example, the abstract class `Payment` defines the common payment behavior, and the interface `Refundable` is used for specific payment methods that support refunds.
* The design of this system allows for future extensibility. For example, adding a new payment method like Apple Pay would simply involve extending the `Payment` class and optionally implementing the `Refundable` interface.

This example demonstrates how abstract classes and interfaces can work together to design robust, maintainable, and scalable systems in Java.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/abstractclassesvsinterfaces/AbstractClassesVsInterfaces.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/nestedclasses/NestedClasses.md)