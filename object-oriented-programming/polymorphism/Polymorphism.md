# Polymorphism in Java
Polymorphism is one of the four fundamental concepts of Object-Oriented Programming (OOP), alongside Encapsulation, Inheritance, and Abstraction. The term polymorphism is derived from the Greek words "poly" (many) and "morph" (forms), meaning that it allows objects to take on multiple forms. In Java, polymorphism allows a single method or interface to be used for different types of objects, giving flexibility and extensibility to the code.

Java supports two types of polymorphism:
* Compile-Time Polymorphism (Method Overloading)
* Runtime Polymorphism (Method Overriding)

## Compile-Time Polymorphism (Method Overloading)
Compile-time polymorphism occurs when multiple methods have the same name but differ in their parameter lists (i.e., the number or type of parameters). This is known as **method overloading**. The Java compiler determines which method to invoke based on the method signature at compile time. This enhances code readability and reusability by allowing a single method name to handle multiple use cases.

### Key Points About Method Overloading
* The methods must have the same name but different parameter lists (either the number, type, or order of parameters).
* The return type can be different, but return type alone cannot be used to overload methods.
* Method overloading can occur within the same class or across a class and its subclass.

#### Example of Method Overloading
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
### Advantages of Method Overloading
* `Improved Readability:` The same method name for related actions makes code easier to understand.
* `Increased Flexibility:` Different operations can be performed by using various parameter types.
* `Code Reusability:` Method overloading allows similar methods to be reused under a single method name.

### Overloading with Varargs:
Method overloading can also be implemented using variable-length argument lists (varargs). This allows a method to accept a variable number of parameters.
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

## Runtime Polymorphism (Method Overriding)
Runtime polymorphism occurs when a subclass provides a specific implementation of a method that is already defined in its superclass. This is known as **method overriding**. The decision about which method to call is made at runtime based on the actual object, not the reference type. It enables dynamic method dispatch and is key to implementing polymorphic behavior in OOP.

### Key Points About Method Overriding
* The method in the subclass must have the same name, return type, and parameter list as the method in the superclass.
* Overriding allows subclasses to provide a specific implementation for a method that is already defined in its parent class.
* Method overriding can only occur when inheritance is involved.
* The `@Override` annotation can be used to indicate that a method is being overridden.

#### Example of Method Overriding
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

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("The cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog();
        Animal myCat = new Cat();

        myAnimal.sound(); // Calls method in Animal
        myDog.sound(); // Calls overridden method in Dog
        myCat.sound(); // Calls overridden method in Cat
    }
}
```
In this example, the `sound()` method is overridden in both the `Dog` and `Cat` classes. During runtime, the actual type of the object determines which method is invoked.

### Advantages of Method Overriding
* `Polymorphism:` The same method can behave differently depending on the object that invokes it.
* `Flexibility:` Method overriding allows the subclass to provide a more specific implementation for a method.
* `Extensibility:` It allows for the extension of an existing class's functionality.

### Usage of `super` in Overriding
The `super` keyword can be used within an overridden method to call the superclass version of the method. This is useful when you want to retain some behavior of the parent method while extending it.
```
class Animal {
    void sound() {
        System.out.println("This animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        super.sound(); // Calls the superclass method
        System.out.println("The dog barks");
    }
}
```

## Summary of Polymorphism in Java
* `Method Overloading (Compile-Time Polymorphism)`: Occurs when methods share the same name but have different parameter lists. It is resolved at compile time.
* `Method Overriding (Runtime Polymorphism)`: Occurs when a subclass provides a specific implementation for a method defined in its superclass. It is resolved at runtime.

Polymorphism allows developers to design more flexible and maintainable code, making OOP powerful in creating scalable and adaptable systems.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/inheritance/Inheritance.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/method-overriding/MethodOverriding.md)