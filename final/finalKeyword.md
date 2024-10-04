# Understanding the final Keyword in Java
In Java, the `final` keyword is used to apply restrictions to variables, methods, and classes. Once a variable, method, or class is declared as `final`, certain rules come into play to prevent modification. This can be useful for creating constants, locking down behavior, and ensuring that certain code structures remain intact.

In this repository, we’ll cover the three main usages of the `final` keyword:
* **Final Variables** - Creating constants that cannot be changed once assigned.
* **Final Methods** - Preventing method overriding in subclasses.
* **Final Classes** - Preventing a class from being inherited by any other class.

## Final Variables: Defining Constants
A `final` variable in Java is essentially a constant; its value can be assigned only once, and after that, it cannot be modified. These variables are used to store fixed values that remain unchanged throughout the program's execution, such as mathematical constants (e.g., `PI`), configuration settings, or limits.

[![](https://markdown-videos-api.jorgenkh.no/youtube/SBMooaxh9oU)](https://youtu.be/SBMooaxh9oU)

### Example
```
class FinalVariableExample {
    final int MAX_LIMIT = 100;

    void displayLimit() {
        System.out.println("The maximum limit is: " + MAX_LIMIT);
    }
}

public class Main {
    public static void main(String[] args) {
        FinalVariableExample obj = new FinalVariableExample();
        obj.displayLimit();
    }
}
```
In the example above, `MAX_LIMIT` is declared as `final`, which means it’s a constant and cannot be changed. If you attempt to modify `MAX_LIMIT`, the compiler will throw an error. This helps in maintaining consistency, as constants are essential when defining values that should not be altered.

### Key Features of Final Variables:
* Once assigned, their value cannot be changed.
* Final variables are often used to create constants.
* Best practices include declaring final variables in uppercase with underscores (`MAX_LIMIT`).

## Final Methods: Preventing Method Overriding
A `final` method is a method that cannot be overridden by subclasses. This is useful when you want to ensure that certain functionality remains unchanged, even when inherited by other classes. In situations where altering a method’s behavior could break core functionality, marking it as `final` guarantees that the method will behave the same in all instances.

[![](https://markdown-videos-api.jorgenkh.no/youtube/r1MjgcMVYGY)](https://youtu.be/r1MjgcMVYGY)

### Example
```
class Parent {
    final void show() {
        System.out.println("This is a final method.");
    }
}

class Child extends Parent {
    // void show() { System.out.println("Trying to override"); } // This will cause an error
}

public class Main {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.show();  // Calls the final method from Parent class
    }
}
```
In this example, the `show()` method in the `Parent` class is marked as `final`, preventing the `Child` class from overriding it. Attempting to override the method in the `Child` class would result in a compilation error.

### Key Features of Final Methods:
* Prevents method overriding in subclasses.
* Ensures that critical functionality is locked and not altered accidentally.
* Commonly used in frameworks and libraries where the base functionality must remain consistent.

## Final Classes: Preventing Inheritance
A `final` class is a class that cannot be extended or inherited by any other class. This is particularly useful when you want to prevent modification of the class's behavior via inheritance. For example, many core classes in Java, such as the `String` class, are declared as `final` to prevent altering their behavior or internal implementation.

[![](https://markdown-videos-api.jorgenkh.no/youtube/e1BOyEWA5MA)](https://youtu.be/e1BOyEWA5MA)

### Example
```
final class Parent {
    void display() {
        System.out.println("This is a method in a final class.");
    }
}

// The following line will cause an error
// class Child extends Parent { }  // Error: Cannot inherit from final class

public class Main {
    public static void main(String[] args) {
        Parent obj = new Parent();
        obj.display();
    }
}
```
In the example, `Parent` is marked as `final`, which means no other class can extend it. Any attempt to create a subclass of `Parent` would result in a compilation error.

### Key Features of Final Classes:
* Prevents inheritance, ensuring the class’s implementation remains unchanged.
* Often used for utility classes or classes where inheritance could compromise performance or functionality (e.g., `String` class in Java).
* Provides a way to secure critical classes in frameworks and libraries.

## When to Use `final` Keyword
* `Final Variables:` Use when you need to define constants that should not change once initialized.
* `Final Methods:` Use to lock critical methods to ensure they are not overridden and their behavior remains consistent across all instances.
* `Final Classes:` Use when you want to prevent any class from extending the current class, ensuring the internal structure and behavior are not altered.

## Conclusion
The `final` keyword in Java provides a useful way to impose restrictions on variables, methods, and classes. By using final variables, methods, and classes, you can create a more secure and reliable codebase where critical functionality and values remain intact throughout the program's execution.

This repository contains examples and code snippets demonstrating the use of the `final` keyword in various scenarios. Feel free to explore the code and experiment with the examples to deepen your understanding of how `final` works in Java.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/static-members/StaticMembers.md)