# Runtime Polymorphism in Java
**Runtime Polymorphism** is one of the core concepts of Object-Oriented Programming (OOP) that enables dynamic behavior in programs. In Java, runtime polymorphism is achieved through method overriding. It allows a method to be invoked based on the actual object (or instance) at runtime, rather than the reference type determined during compile time. This is a powerful feature that enables flexible and extensible code.

[![](https://markdown-videos-api.jorgenkh.no/youtube/VeSi4crtu9c)](https://youtu.be/VeSi4crtu9c)

## Key Concepts of Runtime Polymorphism
### Method Overriding
* Method overriding occurs when a subclass provides its own implementation of a method that is already defined in its superclass.
* The overriding method must have the same name, return type, and parameters as the method in the superclass.
* The `@Override` annotation is often used to indicate that a method is being overridden.

### Dynamic Binding
* In runtime polymorphism, the method call is resolved at runtime rather than compile-time.
* This is known as `dynamic binding` or `late binding`. At runtime, the JVM determines the actual object that the reference is pointing to and invokes the appropriate method.

### Parent Class Reference, Child Class Object
Runtime polymorphism is often implemented by using a parent class reference to point to a child class object. Even though the reference type is of the parent class, the method called will be the one in the child class.

#### Syntax and Example
Below is a basic example that demonstrates runtime polymorphism using method overriding
```
class Animal {
    // Method in parent class
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    // Overriding the sound method in Dog class
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    // Overriding the sound method in Cat class
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal;  // Parent class reference

        animal = new Dog();  // Reference points to a Dog object
        animal.sound();      // Calls Dog's overridden sound method

        animal = new Cat();  // Reference points to a Cat object
        animal.sound();      // Calls Cat's overridden sound method
    }
}
```
#### Explanation
* Here, `Animal` is the parent class, and both `Dog` and `Cat` are subclasses that override the `sound()` method.
* Even though the reference variable `animal` is of type `Animal`, it points to `Dog` and `Cat` objects at runtime, and the overridden methods in the respective subclasses are invoked.

## Advantages of Runtime Polymorphism
* `Flexibility:` Runtime polymorphism enables code to work flexibly with objects of different types while using a common interface. This allows for scalable and maintainable designs.
* `Code Reusability:` You can create more generic and reusable code. For example, you can write code that works with the superclass reference, and the actual method to be executed will depend on the specific object type at runtime.
* `Loosely Coupled Code:` Runtime polymorphism helps create loosely coupled code. You can change the implementation in subclasses without affecting the existing code that relies on the parent class interface.
* `Scalability:` This dynamic behavior of objects allows new classes to be easily introduced into the system without changing the existing code, making the application scalable.

## Best Practices for Runtime Polymorphism
* `Use Inheritance Wisely:` Inheritance should be applied thoughtfully. Only use inheritance when the "is-a" relationship holds between the parent and child classes.
* `Leverage Abstract Classes and Interfaces:` Use abstract classes and interfaces to define common behaviors that multiple classes can inherit or implement.
* `Avoid Excessive Downcasting:` Excessive use of downcasting (casting a parent type reference to a child type) can be dangerous and defeat the purpose of runtime polymorphism.

## Conclusion
Runtime polymorphism is a critical feature of OOP that allows objects to behave differently based on their actual types at runtime. Through method overriding, runtime polymorphism promotes flexibility, code reusability, and loose coupling, making it an indispensable tool for creating scalable and maintainable applications. By understanding and effectively implementing runtime polymorphism, developers can write more dynamic and flexible Java programs.