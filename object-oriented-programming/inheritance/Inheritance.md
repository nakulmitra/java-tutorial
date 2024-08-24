# Inheritance in Java
Inheritance is a core concept in Object-Oriented Programming (OOP) that allows one class to inherit the fields (attributes) and methods (behavior) of another class. It facilitates code reusability, a natural hierarchy, and method overriding, enabling developers to build more complex systems in a structured and efficient way.

## What is Inheritance?
Inheritance allows a class (referred to as the **subclass** or **child class**) to inherit attributes and methods from another class (called the **superclass** or **parent class**). This allows the child class to automatically gain the functionality and properties of the parent class while also adding its own unique features.
* **Superclass:** The class being inherited from.
* **Subclass:** The class that inherits from the superclass.

### Example
```
// Superclass
public class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass
public class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.eat(); // Inherited method from Animal
        myDog.bark(); // Method from Dog
    }
}
```
In this example, the `Dog` class inherits the `eat()` method from the `Animal` class. The `Dog` class can now use the `eat()` method along with its own method `bark()`.

## The `extends` Keyword
To establish inheritance in Java, the `extends` keyword is used. This keyword allows a class to inherit from another class, meaning the subclass automatically inherits all non-private fields and methods from the superclass.

### Example
```
class Parent {
    void display() {
        System.out.println("This is the parent class.");
    }
}

class Child extends Parent {
    void show() {
        System.out.println("This is the child class.");
    }
}
```
In this example, `Child` extends `Parent`, thereby inheriting all the non-private methods and attributes of the `Parent` class.

## Types of Inheritance
* `Single Inheritance:` Involves one class inheriting from another class. This is the most common and is supported directly by Java Example: **Car** extends **Vehicle**.
* `Hierarchical Inheritance:` In this type, multiple subclasses inherit from a single superclass. Example: **Dog**, **Cat**, and **Bird** classes extend the **Animal** superclass.
* `Multilevel Inheritance:` A chain of inheritance, where a class is inherited by another class, which is further inherited by another class. Example: **Vehicle -> Car -> ElectricCar**.

Note: Java does not support multiple inheritance directly (i.e., a class cannot inherit from multiple classes simultaneously). However, this can be achieved through interfaces, which will be covered in a future topic.

## Inheritance Example in Java
Let's take a real-world example where a subclass (`Car`) inherits from a superclass (`Vehicle`):
```
// Superclass
public class Vehicle {
    String brand;
    int year;

    void honk() {
        System.out.println("Vehicle honks!");
    }
}

// Subclass
public class Car extends Vehicle {
    String model;

    void displayInfo() {
        System.out.println("Brand: " + brand + ", Model: " + model + ", Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.brand = "Toyota";
        myCar.model = "Camry";
        myCar.year = 2021;

        myCar.honk();  // Inherited method from Vehicle
        myCar.displayInfo();  // Method from Car
    }
}
```
In this example, `Car` inherits from `Vehicle`. The `Car` class gains access to the `honk()` method, along with the attributes `brand` and `year`, and can use them just like its own methods.

## Benefits of Inheritance
* `Code Reusability:` Inheritance allows you to reuse code from the superclass in the subclass, reducing redundancy.
* `Method Overriding:` Subclasses can override methods of the superclass to provide specific behavior for the subclass.
* `Establishes a Hierarchy:` It provides a clear relationship between classes, helping to manage and understand the code better.

## Limitation: Single Inheritance in Java
Java supports only **single inheritance**, meaning a class can only inherit from one superclass. This limitation avoids complexities like the diamond problem seen in languages that support multiple inheritance.
* `Diamond Problem:` This occurs when a class inherits from two classes that share a common ancestor, causing ambiguity about which method to inherit.
While Java doesn’t support multiple inheritance, it offers interfaces as a way to achieve similar functionality.

## Conclusion
Inheritance is a powerful feature of Object-Oriented Programming that promotes code reuse and establishes a hierarchy of classes. By inheriting from a superclass, a subclass can reuse methods and fields while also extending or modifying them.

Understanding inheritance enables you to write more organized and maintainable code. Try applying inheritance in your projects to create well-structured systems.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/encapsulation/Encapsulation.md)