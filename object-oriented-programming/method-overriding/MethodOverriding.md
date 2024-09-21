# Method Overriding in Java
Method overriding is a fundamental concept in Object-Oriented Programming (OOP) that enables a subclass to provide a specific implementation of a method that is already defined in its superclass. It plays a crucial role in achieving runtime polymorphism in Java.

[![](https://markdown-videos-api.jorgenkh.no/youtube/2vaBwAuraNM)](https://youtu.be/2vaBwAuraNM)

## Key Concepts
* **Inheritance:** Method overriding occurs only when there is inheritance, meaning a subclass inherits the methods and properties from a superclass.
* **Same Method Signature:** For method overriding to occur, the method in the subclass must have the same name, return type, and parameters as the method in the superclass.
* **Overriding vs Overloading:** Method overriding should not be confused with method overloading. Overloading is when multiple methods have the same name but differ in parameters, while overriding is about redefining the method in the subclass with the same signature.

## Syntax of Method Overriding
To override a method in Java, we simply declare the method in the subclass with the same signature as in the superclass. We can use the `@Override` annotation to inform the compiler that you intend to override the method, which provides error checking to ensure the method matches the superclass’s method signature.

### Example
```
class Animal {
    void sound() {
        System.out.println("This animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks");
    }
}
```
In this example, the `sound()` method is defined in both the `Animal` superclass and the `Dog` subclass. The Dog class provides its specific implementation of the `sound()` method.

## Why Use Method Overriding?
* **Polymorphism:** Method overriding allows a subclass to provide a specific implementation for a method, enabling polymorphism. This means that the same method call can behave differently depending on the object that calls it. For instance, both `Animal` and `Dog` objects can call the `sound()` method, but the result will depend on the type of object.
* **Dynamic Method Dispatch:** At runtime, the method to be executed is determined by the type of the object, not the type of reference. This process is known as dynamic method dispatch or runtime polymorphism.
* **Reusability and Extensibility:** Overriding allows extending or modifying the behavior of inherited methods. This promotes code reuse, as the subclass can inherit common behavior while providing additional functionality or overriding behavior as needed.

## Example with `super` Keyword
The `super` keyword is often used in method overriding to call the superclass’s version of a method. This is useful when you want to retain the behavior of the parent class’s method while adding additional functionality in the subclass.
```
class Animal {
    void sound() {
        System.out.println("This animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        super.sound();  // Calls the superclass method
        System.out.println("The dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.sound();  // Calls the overridden method
    }
}
```
Here, the `Dog` class overrides the `sound()` method but uses the `super.sound()` call to invoke the original behavior from the `Animal` class before adding its own behavior.

## Rules for Method Overriding
* The method must have the same signature as in the superclass.
* The method must be in a subclass of the class that contains the original method.
* The method in the subclass should have the same or more accessible access modifier. For example, if a method is `protected` in the superclass, it cannot be `private` in the subclass.
* We cannot override `final`, `static`, or `private` methods.

## Example with Multiple Subclasses
Let’s extend the concept with multiple subclasses to see how overriding leads to polymorphism.
```
class Vehicle {
    void start() {
        System.out.println("The vehicle starts");
    }
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("The car starts with a key ignition");
    }
}

class Bike extends Vehicle {
    @Override
    void start() {
        System.out.println("The bike starts with a kick");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myVehicle = new Vehicle();
        myVehicle.start();  // Calls the start method in Vehicle

        Vehicle myCar = new Car();
        myCar.start();  // Calls the overridden start method in Car

        Vehicle myBike = new Bike();
        myBike.start();  // Calls the overridden start method in Bike
    }
}
```
In this example, `Car` and `Bike` classes both override the `start()` method of the `Vehicle` superclass. The specific implementation is executed depending on the type of object at runtime.

## Method Overriding and Access Modifiers
* **Public** methods can be overridden, but they must remain public or more accessible in the subclass.
* **Protected** methods can also be overridden, and they can be kept `protected` or made `public`.
* **Private** methods are not visible to the subclass and cannot be overridden.

## Advantages
* Provides runtime polymorphism.
* Helps in implementing the concept of "programming to an interface."
* Encourages code reuse by allowing existing methods to be modified for specific needs.

## Conclusion
Method overriding is an essential feature in Java that allows subclasses to modify the behavior of inherited methods, enhancing the flexibility and modularity of your code. By mastering method overriding, you can effectively implement polymorphism and build robust, maintainable object-oriented systems.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/polymorphism/Polymorphism.md)
| [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/method-overloading/MethodOverloading.md)