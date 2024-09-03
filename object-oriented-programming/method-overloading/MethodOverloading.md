# Introduction
Polymorphism is one of the fundamental concepts in Object-Oriented Programming (OOP). It refers to the ability of a function, method, or object to take on multiple forms. Polymorphism in Java is mainly classified into two types:
* **Compile-Time Polymorphism** (also known as static polymorphism or method overloading)
* **Runtime Polymorphism** (also known as dynamic polymorphism or method overriding)

In this section, we will focus on Compile-Time Polymorphism, achieved through method overloading.
[![](https://markdown-videos-api.jorgenkh.no/youtube/soR3cZfksr0)](https://youtu.be/soR3cZfksr0)

## What is Compile-Time Polymorphism?
Compile-Time Polymorphism in Java occurs when multiple methods in the same class have the same name but different parameters. The method that is executed is determined at compile-time based on the method signature, which includes the method's name, the number of parameters, and the types of parameters.

## Characteristics of Method Overloading
* `Same method name:` All overloaded methods must have the same name.
* `Different parameter lists:` The methods must differ in the number of parameters or the type of parameters.
* `Overloading in the same class:` Method overloading generally occurs within the same class. However, it can also occur in a subclass via inheritance.
* `Return type:` The return type of the methods can be different, but return type alone does not constitute method overloading.

## Benefits of Method Overloading
* `Improved Readability:` Overloading methods make it easier to understand related methods in the code.
* `Increased Flexibility:` The same method name can perform different actions based on varying parameters.
* `Code Reusability:` By reusing method names with different signatures, you eliminate the need to create new method names for similar actions.

### Example of Method Overloading
```
public class Calculator {
    // Method to add two integers
    public int add(int a, int b) {
        return a + b;
    }
    
    // Overloaded method to add two doubles
    public double add(double a, double b) {
        return a + b;
    }
    
    // Overloaded method to add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("Sum of two integers: " + calc.add(5, 10));
        System.out.println("Sum of two doubles: " + calc.add(5.5, 10.2));
        System.out.println("Sum of three integers: " + calc.add(1, 2, 3));
    }
}
```
### Explanation
The class Calculator contains three overloaded add() methods:
* One takes two integers as parameters.
* Another takes two doubles.
* The last one takes three integers.

Depending on the arguments passed during the method call, the compiler determines which add() method to invoke.

## Method Overloading with Varargs
Java also supports variable-length argument lists (varargs) in method overloading. This enables methods to accept a varying number of arguments of the same type.

### Example of Varargs in Method Overloading
```
public class VarargsExample {
    // Method with varargs
    public void displayNumbers(int... numbers) {
        for (int number : numbers) {
            System.out.println(number);
        }
    }

    public static void main(String[] args) {
        VarargsExample example = new VarargsExample();
        example.displayNumbers(1, 2, 3);
        example.displayNumbers(4, 5);
    }
}
```
### Explanation
* The `displayNumbers()` method uses the `int... numbers` syntax, which means that it can accept a variable number of `int` arguments.
* The method can be called with any number of integer arguments, making it highly flexible.

## Method Overloading Across Parent and Child Classes
Method overloading can also occur between a superclass and a subclass. If the subclass defines a method with the same name but a different parameter list, it is considered method overloading.

### Example of Method Overloading Across Parent and Child Classes
```
class Parent {
    void showMessage(String message) {
        System.out.println("Parent says: " + message);
    }
}

class Child extends Parent {
    void showMessage(String message, String name) {
        System.out.println(name + " says: " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.showMessage("Hello"); // Calls Parent's method
        child.showMessage("Hello", "Child"); // Calls Child's overloaded method
    }
}
```
### Explanation
* The Child class overloads the `showMessage()` method of the Parent class by adding an extra parameter `name`.
* When the method is called with a single string, it invokes the `Parent` class’s method, but when it is called with two strings, it invokes the `Child` class’s method.

## Rules for Method Overloading
* `Same Method Name:` Overloaded methods must have the same name.
* `Different Parameter List:` Methods must have different parameter lists (either the number or types of parameters).
* `Different Return Types:` Methods may have different return types, but return type alone cannot be used to distinguish overloaded methods.
* `Compile-Time Decision:` Method overloading is resolved at compile-time, hence known as compile-time polymorphism.

## Advantages of Compile-Time Polymorphism
* `Code Organization:` It makes code more structured and easier to manage.
* `Readability:` Reusing method names with different signatures can make code easier to understand.
* `Modularity:` Methods are logically grouped under the same name, improving modularity and cohesion.
* `Flexibility:` Overloaded methods provide flexibility by allowing methods to handle different types and quantities of arguments.

## Conclusion
Compile-time polymorphism, or method overloading, is a powerful feature of Java that allows methods to be reused based on different parameter lists. It helps in improving code readability, modularity, and reusability, making programs more maintainable. In Java, method overloading occurs within the same class or across parent and child classes, with the method to be invoked determined at compile time based on the arguments passed.