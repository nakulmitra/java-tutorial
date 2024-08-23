# Encapsulation in Java
Encapsulation is one of the fundamental principles of Object-Oriented Programming (OOP) in Java. It is the process of wrapping code (methods) and data (variables) together into a single unit, usually in the form of a class. Encapsulation helps to control the access and modification of data by restricting direct access to the internal state of an object. Instead, the state is accessed and modified through public methods, often called "getters" and "setters."

## Purpose of Encapsulation
The primary purpose of encapsulation is to hide the internal representation (state) of an object and to protect the object’s integrity by preventing unauthorized access or modification. Encapsulation provides the following key benefits:
* `Data Protection:` The internal state of an object is hidden from the outside world, ensuring that its data cannot be changed inadvertently.
* `Control:` The access to the object’s data is controlled through getter and setter methods, allowing validation and conditional updates.
* `Modularity:` By keeping data and methods together, encapsulation makes the code more modular and easier to maintain.

## Access Modifiers
Access modifiers in Java determine the level of visibility and accessibility of classes, variables, and methods. There are four types of access modifiers:
* `private:` Accessible only within the same class.
* `public:` Accessible from anywhere.
* `protected:` Accessible within the same package and subclasses.
* `default (no modifier):` Accessible only within the same package.

### Example
```
public class Person {
    // Private field
    private int age;

    // Getter method for age
    public int getAge() {
        return age;
    }

    // Setter method for age with validation
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        } else {
            System.out.println("Age must be positive.");
        }
    }
}
```
In this example, the `age` field is private, and access to it is controlled using the `getAge()` and `setAge()` methods. The setter includes validation logic to ensure that the `age` is positive.

## Encapsulation in Practice
To implement encapsulation in Java:
* `Make fields private:` This hides the internal state from outside interference.
* `Use public getter and setter methods:` These provide controlled access to the private fields. The getter retrieves the value, and the setter modifies it after validation or specific conditions.

### Example
```
public class Car {
    // Private fields
    private String color;
    private String model;
    private int year;

    // Getter for color
    public String getColor() {
        return color;
    }

    // Setter for color
    public void setColor(String color) {
        this.color = color;
    }

    // Getter for model
    public String getModel() {
        return model;
    }

    // Setter for model
    public void setModel(String model) {
        this.model = model;
    }

    // Getter for year
    public int getYear() {
        return year;
    }

    // Setter for year with validation
    public void setYear(int year) {
        if (year > 1885) { // First car was invented around 1886
            this.year = year;
        } else {
            System.out.println("Invalid year for a car.");
        }
    }

    // Method to display car details
    public void displayInfo() {
        System.out.println("Model: " + model + ", Color: " + color + ", Year: " + year);
    }
}
```
### Main Class
```
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();

        // Setting values using setter methods
        myCar.setColor("Red");
        myCar.setModel("Toyota");
        myCar.setYear(2021);

        // Getting values using getter methods
        System.out.println("Car Model: " + myCar.getModel());
        System.out.println("Car Color: " + myCar.getColor());
        System.out.println("Car Year: " + myCar.getYear());

        // Display car details
        myCar.displayInfo();
    }
}
```
In this example, the `Car` class encapsulates the details of a car. The fields `color`, `model`, and `year` are private, and public getter and setter methods provide access to them. The setter method for the year field includes validation to ensure that the car's `year` is valid.

## Advantages of Encapsulation
* `Improved Maintainability:` Since the internal implementation is hidden, you can change it without affecting the external code that uses the class.
* `Controlled Access:` By controlling how the data is accessed and modified, encapsulation improves the integrity of the object’s state.
* `Modularity:` Classes encapsulate the logic and data into one cohesive unit, making the system easier to understand and maintain.
* `Security:` Encapsulation prevents unauthorized access to sensitive data by using private fields.

## Conclusion
Encapsulation is a key aspect of Java’s object-oriented design. It helps to create secure, modular, and maintainable code by restricting access to the internal state of an object and providing controlled ways to interact with it. Through encapsulation, Java allows developers to hide the complexities of data handling and ensures that objects can be used in a reliable manner.

Encapsulation, along with inheritance, polymorphism, and abstraction, forms the backbone of OOP in Java, enabling developers to build flexible and scalable applications.

[< Previous](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/constructors/Constructors.md)