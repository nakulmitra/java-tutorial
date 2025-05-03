# Access Modifiers in Java: Detailed Explanation
In Java, **access modifiers** control the visibility and accessibility of classes, methods, variables, and constructors. These modifiers are essential for implementing **encapsulation** — one of the fundamental principles of Object-Oriented Programming (OOP). Using access modifiers correctly allows you to secure your code by restricting access to critical parts of your program while exposing only the necessary parts.

[![](https://markdown-videos-api.jorgenkh.no/youtube/XaihsgrG1pM)](https://youtu.be/XaihsgrG1pM)

Java provides four main access modifiers:
* Private
* Default (Package-Private)
* Protected
* Public

Each modifier provides a different level of access control. Let’s explore them in detail:

## Private Access Modifier
The private access modifier restricts access to the members (variables or methods) only within the class in which they are declared. No other class, even within the same package, can access private members.

### Key Points
* Only accessible within the same class.
* Used to secure class properties and methods from external access.
* Often used in conjunction with **getter** and **setter** methods to control how fields are accessed and modified.

### Example
```java
class User {
    private String name;  // Private variable

    // Constructor
    public User(String name) {
        this.name = name;
    }

    // Private method
    private void displayName() {
        System.out.println("User name: " + name);
    }

    // Public method to access private method
    public void showDetails() {
        displayName();  // Accessing private method within the same class
    }
}

public class Main {
    public static void main(String[] args) {
        User user = new User("John Doe");
        user.showDetails();  // Allowed
        // user.displayName();  // Error: Cannot access private method outside the class
    }
}
```
In this example:
* The `name` variable and `displayName()` method are private. They cannot be accessed directly from outside the User class.
* The `showDetails()` method, which is public, is used to access the private method within the class.

## Default (Package-Private) Access Modifier
When no access modifier is specified, Java uses the default or package-private access level. Members with default access are accessible only within the same package. They cannot be accessed from classes in different packages.

### Key Points
* Accessible only within the same package.
* If no access modifier is specified, it defaults to package-private.
* Ideal for internal package-level visibility without exposing functionality to external packages.

### Example
```java
class Product {
    String productName;  // Default (package-private) access

    void displayProduct() {
        System.out.println("Product: " + productName);
    }
}

public class Main {
    public static void main(String[] args) {
        Product product = new Product();
        product.productName = "Laptop";
        product.displayProduct();  // Allowed within the same package
    }
}
```
Both the `productName` variable and `displayProduct()` method are accessible within the same package but not outside of it.

## Protected Access Modifier
The protected access modifier allows access within the same package and to subclasses in different packages. This modifier is typically used when inheritance is involved, allowing derived classes to access protected members of the parent class.

### Key Points
* Accessible within the same package and by subclasses in other packages.
* Useful when designing inheritance hierarchies where the subclass needs access to some members of the parent class.

### Example
```java
class Employee {
    protected String employeeName;  // Protected variable

    // Protected method
    protected void displayEmployee() {
        System.out.println("Employee: " + employeeName);
    }
}

public class Manager extends Employee {
    public void showManagerDetails() {
        employeeName = "Alice";
        displayEmployee();  // Accessible due to inheritance
    }
}

public class Main {
    public static void main(String[] args) {
        Manager manager = new Manager();
        manager.showManagerDetails();  // Allowed due to inheritance
    }
}
```
The `employeeName` variable and `displayEmployee()` method are protected. They are accessible in the `Manager` subclass even though `Manager` is a separate class.

## Public Access Modifier
The public access modifier allows access from any other class, inside or outside the package. Public members are accessible everywhere in the application.

### Key Points
* Accessible from anywhere—inside the class, other classes, within the same package, and from external packages.
* Used when you want to make the members of a class universally accessible.

### Example
```java
public class Car {
    public String model;  // Public variable

    // Public method
    public void displayModel() {
        System.out.println("Car Model: " + model);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.model = "Tesla Model S";  // Accessible everywhere
        car.displayModel();  // Accessible everywhere
    }
}
```
Both the `model` variable and `displayModel()` method are public and can be accessed from any class, including external ones.

## Summary of Access Modifiers in Java
| Access Modifier | Class | Package | Subclass | Global |
| ----------------|-------|---------|----------|--------|
|     private     |  Yes  |   No    |    No    |   No   |
|     default     |  Yes  |   Yes   |    No    |   No   |
|    protected    |  Yes  |   Yes   |    Yes   |   No   |
|     public      |  Yes  |   Yes   |    Yes   |   Yes  |


## Key Takeaways
* `Private:` Restricts access to within the same class. Typically used for securing sensitive data or implementation details.
* `Default:` Allows access within the same package. Often used for package-level functionality.
* `Protected:` Allows access within the same package and through inheritance in subclasses.
* `Public:` Provides universal access, suitable for methods and variables that need to be accessible across the application.

## Conclusion
In this guide, we've covered the four primary access modifiers in Java: **private**, **default**, **protected**, and **public**. Understanding these access levels is crucial for controlling the visibility of your code and implementing encapsulation, ensuring that only the necessary parts of your code are exposed.

Use access modifiers thoughtfully to protect the integrity of your classes and ensure your Java programs are both **secure** and **maintainable**.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/final/finalKeyword.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/exception-handling/Introduction.md)