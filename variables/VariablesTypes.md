# Types of Variables in Java
In Java, variables are used to store data that can be manipulated by the program. Java provides three main types of variables, each with its own scope, lifetime, and characteristics. These types are:
* Local Variables
* Instance Variables
* Static Variables (Class Variables)

[![](https://markdown-videos-api.jorgenkh.no/youtube/LvmW2KqCjGI)](https://youtu.be/LvmW2KqCjGI)

## Local Variables
`Definition:` Local variables are declared within a method, constructor, or block of code and are only accessible within that scope. These variables are temporary and only exist during the execution of the method or block in which they are defined.

### Characteristics
* `Scope:` Limited to the method, constructor, or block where they are declared.
* `Lifetime:` Created when the method is called and destroyed once the method exits.
* `Initialization:` Must be explicitly initialized before use.

### Example
```
public class Example {
    public void displayMessage() {
        String message = "Hello, World!"; // Local variable
        System.out.println(message);
    }

    public static void main(String[] args) {
        Example example = new Example();
        example.displayMessage();
    }
}
```
In this example, `message` is a local variable that only exists within the `displayMessage()` method. Once the method completes, the variable is destroyed.

## Instance Variables
`Definition:` Instance variables are declared within a class but outside any method, constructor, or block. They are associated with an instance of the class (i.e., an object), and each object has its own copy of the instance variables.

### Characteristics
* `Scope:` Accessible throughout the class in which they are declared, including methods and constructors.
* `Lifetime:` Exists for as long as the object is alive (i.e., created when an object is instantiated and destroyed when the object is destroyed).
* `Default Values:` Automatically initialized with default values if not explicitly initialized (e.g., `0` for int, `null` for objects).

### Example
```
public class Car {
    String color; // Instance variable
    int speed;    // Instance variable

    public void displayDetails() {
        System.out.println("Color: " + color);
        System.out.println("Speed: " + speed);
    }

    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.color = "Red";
        myCar.speed = 100;
        myCar.displayDetails();
    }
}
```
In this example, `color` and `speed` are instance variables. Each `Car` object will have its own `color` and `speed` values.

## Static Variables (Class Variables)
Definition: Static variables are declared with the `static` keyword within a class but outside any method, constructor, or block. They are associated with the class rather than instances of the class. This means all objects of the class share the same static variable.

### Characteristics
* `Scope:` Accessible throughout the class, similar to instance variables, but can also be accessed using the class name (without needing an instance).
* `Lifetime:` Created when the class is loaded into memory and destroyed when the class is unloaded.
* `Shared Among Instances:` All instances of the class share the same static variable.

### Example
```
public class Car {
    static int numberOfCars = 0; // Static variable (class variable)
    String color;                // Instance variable

    public Car(String color) {
        this.color = color;
        numberOfCars++;
    }

    public static void main(String[] args) {
        Car car1 = new Car("Red");
        Car car2 = new Car("Blue");
        System.out.println("Number of cars: " + Car.numberOfCars);
    }
}
```
In this example, `numberOfCars` is a static variable that is shared among all `Car` objects. Each time a new `Car` object is created, the value of `numberOfCars` increases.

## Conclusion
In Java, variables can be classified into three types based on their scope, lifetime, and behavior:
* `Local Variables:` Declared within a method or block, limited in scope and lifetime to that method or block.
* `Instance Variables:` Declared within a class but outside methods; associated with objects of the class and exist as long as the object exists.
* `Static Variables:` Declared with the `static` keyword and associated with the class itself; shared among all instances of the class.
Understanding the types of variables in Java is crucial for writing clean, efficient, and maintainable code.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/variables/FloatingPointDataType.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/control-flow-statements/if-else/IfElseTheory.md)