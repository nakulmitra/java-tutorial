# Interfaces in Java
In Java, interfaces are one of the key mechanisms for achieving abstraction and flexibility in Object-Oriented Programming (OOP). An interface defines a contract or blueprint for classes, specifying the methods that a class must implement but without defining how these methods should behave. Interfaces are used to provide a way to achieve abstraction, multiple inheritance, and polymorphism in Java.

[![](https://markdown-videos-api.jorgenkh.no/youtube/D2Hh6UDUexE)](https://youtu.be/D2Hh6UDUexE)

## Definition of an Interface
An interface in Java is a reference type, similar to a class, that can contain:
* Abstract methods (methods without a body)
* Constants (public, static, and final by default)
* Since Java 8, default methods and static methods

An interface is declared using the `interface` keyword and cannot contain any concrete method implementations (except for default and static methods added in Java 8).
```
interface Animal {
    void sound();  // Abstract method
}
```
In this example, the `Animal` interface declares an abstract method `sound()`. Any class that implements the `Animal` interface must provide an implementation for this method.

## Implementing an Interface
To use an interface, a class must implement it using the `implements` keyword. The implementing class is required to provide concrete implementations for all abstract methods defined in the interface.

### Example
```
class Dog implements Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}

class Cat implements Animal {
    public void sound() {
        System.out.println("Cat meows");
    }
}
```
In the above example, both `Dog` and `Cat` classes implement the `Animal` interface and provide their own implementations for the `sound()` method.

## Multiple Inheritance with Interfaces
One of the limitations of Java is that it doesn't support multiple inheritance with classes. However, interfaces provide a way to achieve multiple inheritance. A class in Java can implement multiple interfaces, thus inheriting behavior from multiple sources.

### Example
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
Here, the `Dog` class implements both the `Animal` and `Pet` interfaces. This allows the class to inherit behavior from both interfaces, achieving multiple inheritance in a clean and efficient manner.

## Default Methods in Interfaces (Java 8)
Prior to Java 8, interfaces could only contain abstract methods. However, with the introduction of default methods in Java 8, interfaces can now provide concrete implementations for some methods.

A **default method** is a method defined in an interface with a body, and implementing classes can choose to either use the provided implementation or override it.

### Example
```
interface Animal {
    void sound();

    default void sleep() {
        System.out.println("The animal is sleeping.");
    }
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}
```
In this example, the `Animal` interface provides a default method `sleep()`. The `Dog` class does not need to implement this method because it has a default implementation in the interface. However, the `Dog` class can still override the `sleep()` method if needed.

### Benefits of Default Methods:
* `Backward compatibility:` New functionality can be added to existing interfaces without breaking the code of classes that implement these interfaces.
* `Code reuse:` Common behavior across implementing classes can be shared through default methods, reducing duplication.

## Static Methods in Interfaces (Java 8)
Interfaces can also contain **static methods** starting from Java 8. These methods are similar to static methods in classes and can be called on the interface itself, without the need for an implementing class.

### Example
```
interface Utility {
    static void printMessage() {
        System.out.println("This is a static method in the interface.");
    }
}

public class Main {
    public static void main(String[] args) {
        Utility.printMessage();  // Static method is called on the interface
    }
}
```
Static methods in interfaces are not inherited by the implementing classes and must be called on the interface itself.

## Marker Interfaces
A marker interface is an interface that does not have any methods or fields. It is used to signal or mark that a class possesses a certain quality or belongs to a certain category. Examples of marker interfaces in Java include:
* Serializable
* Cloneable
* Remote

### Example
```
class Data implements Serializable {
    // Class marked as Serializable, no methods to implement
}
```
Marker interfaces are often used in conjunction with runtime mechanisms such as serialization and cloning.

## Polymorphism with Interfaces
Interfaces allow for a higher degree of flexibility through polymorphism. By using interfaces as reference types, you can refer to any object that implements that interface, regardless of the specific class of the object. This is particularly useful for writing flexible and scalable code.

### Example
```
Animal animal;  // Interface reference

animal = new Dog();
animal.sound();  // Calls Dog's implementation of sound()

animal = new Cat();
animal.sound();  // Calls Cat's implementation of sound()
```
In this example, both `Dog` and `Cat` objects are referenced by the `Animal` interface type. The method that is invoked depends on the actual object type at runtime, showcasing the polymorphism capabilities of interfaces.

## Best Practices for Using Interfaces
* `Use interfaces for abstraction:` Interfaces are best used when you want to define a contract that different classes can implement, without worrying about how they will do so.
* `Prefer interfaces over abstract classes when possible:` Interfaces provide more flexibility than abstract classes, especially when you want to achieve multiple inheritance.
* `Leverage default methods cautiously:` Default methods can be useful, but overuse may lead to complex and hard-to-maintain interfaces.
* `Design for the long term:` When designing interfaces, consider future growth and backward compatibility, especially if your interface is likely to be implemented by multiple classes.

## Conclusion
Interfaces are a fundamental part of Java's OOP framework, providing powerful tools for abstraction, multiple inheritance, and polymorphism. By defining common behavior through interfaces, Java developers can create more modular, maintainable, and flexible code.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/runtime-polymorphism/RuntimePolymorphism.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/interfaces/InterfacesExample.md)