# Abstract Classes vs Interfaces in Java
In Java, abstract classes and interfaces are two fundamental concepts used to implement abstraction and achieve polymorphism. They play a critical role in defining the structure and behavior of Java applications. Understanding the differences between them and knowing when to use each is key to mastering Object-Oriented Programming (OOP) in Java. This detailed guide explains the main distinctions between abstract classes and interfaces and provides use cases, benefits, and practical examples.

[![](https://markdown-videos-api.jorgenkh.no/youtube/pARL1d3tS2Y)](https://youtu.be/pARL1d3tS2Y)

## Purpose and Design Philosophy
* `Abstract Classes:` Abstract classes are designed to serve as a blueprint for other classes. They allow you to define some common functionality (through concrete methods) and also enforce that subclasses provide their own implementation for certain behaviors (through abstract methods). They are ideal for situations where you need shared behavior among a group of related classes.

* `Interfaces:` Interfaces define a contract that any implementing class must adhere to, but they don't specify how the methods should be implemented. They are primarily used to achieve total abstraction and to define methods that unrelated classes can implement. Interfaces are useful when you want to specify a behavior across multiple, potentially unrelated, classes.

## Methods
### `Abstract Classes`
* Can contain both abstract methods (without a body) and concrete methods (with a body).
* Subclasses are required to implement the abstract methods.
* Concrete methods provide default behavior that can be used or overridden by subclasses.

### `Interfaces`
* Prior to Java 8, interfaces could only contain abstract methods.
* Since Java 8, interfaces can have default methods (with a body) and static methods.
* Abstract methods in an interface must be implemented by the implementing class.

### Example
#### Abstract Class
```
abstract class Animal {
    // Abstract method (no body)
    abstract void sound();

    // Concrete method (with body)
    void sleep() {
        System.out.println("The animal is sleeping.");
    }
}

class Dog extends Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}
```
#### Interface
```
interface Animal {
    void sound(); // Abstract method
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

## Multiple Inheritance
* `Abstract Classes` A class in Java can only extend one abstract class. This is because Java does not support multiple inheritance with classes.

* `Interfaces` A class can implement multiple interfaces, allowing it to inherit behavior from multiple sources. This is one of the primary benefits of interfaces and provides a way to achieve multiple inheritance in Java.

### Example of Multiple Interface Implementation
```
interface Animal {
    void sound();
}

interface Pet {
    void play();
}

class Dog implements Animal, Pet {
    public void sound() {
        System.out.println("Dog barks");
    }

    public void play() {
        System.out.println("Dog plays fetch");
    }
}
```

## Constructors
* `Abstract Classes` Can have constructors, which are called when an instance of a subclass is created. These constructors can be used to initialize fields that are inherited by subclasses.

* `Interfaces` Cannot have constructors because they are not part of the class hierarchy. They only specify behavior that classes must implement, and thus don't manage instance state.

## Fields
* `Abstract Classes` Can have instance variables (fields) that can be initialized and used by the class or its subclasses.

* `Interfaces` Can only contain public, static, final fields, which are essentially constants. Fields in interfaces are implicitly public, static, and final, meaning they cannot be modified.

### Example of Fields in an Abstract Class and Interface
#### Abstract Class
```
abstract class Vehicle {
    int speed; // instance variable

    Vehicle(int speed) {
        this.speed = speed;
    }

    abstract void drive();
}
```
#### Interface
```
interface Vehicle {
    int MAX_SPEED = 120; // public static final by default

    void drive();
}
```

## Access Modifiers
* `Abstract Classes` Methods and variables in an abstract class can have any access modifier (private, protected, or public). This allows you to define varying levels of visibility for the class members.

* `Interfaces` All methods in an interface are implicitly public, and fields are implicitly public, static, and final. You cannot use other access modifiers in interfaces for methods or fields.

## Inheritance vs. Implementation
* `Abstract Classes` A class extends an abstract class, inheriting its methods and fields. Subclasses can override inherited methods or use the default implementations provided by the abstract class.

* `Interfaces` A class implements an interface, meaning it must provide specific implementations for all the abstract methods defined in the interface.

### Example
```
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}

interface Payment {
    void makePayment(double amount);
}

class CreditCard implements Payment {
    public void makePayment(double amount) {
        System.out.println("Paid " + amount + " using Credit Card.");
    }
}
```

## Use Cases
* `Abstract Classes` Use abstract classes when you want to provide common functionality (such as fields or methods) that multiple related classes can inherit.
Example: A `Vehicle` class with common attributes like speed, and subclasses like `Car` and `Bike` inheriting this behavior.

* `Interfaces` Use interfaces when you want to define a contract that can be implemented by any class, whether or not they are related.
Example: A `Payment` interface that can be implemented by different payment types like `CreditCard`, `PayPal`, etc.

## Performance Considerations
* `Abstract Classes` Tend to be slightly faster because abstract classes provide some method implementations, which reduce the overhead of resolving methods at runtime.

* `Interfaces` Can introduce more runtime overhead when multiple interfaces are implemented, as Java needs to perform method resolution to determine which method to call from the interface.

## Conclusion
Both abstract classes and interfaces are essential tools for implementing abstraction and defining behavior in Java. The choice between them depends on your design goals:
* Use abstract classes when there is a strong relationship between the classes and you want to share code.
* Use interfaces when you want to define a contract that can be implemented by any class, regardless of its place in the class hierarchy.

Understanding these differences will help you design more flexible, scalable, and maintainable Java applications.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/abstract/AbstractClasses.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/abstractandinterfaces/AbstractAndInterfaces.md)