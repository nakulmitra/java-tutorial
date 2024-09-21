# Nested Classes in Java
Nested classes in Java provide a way to logically group classes that are only used in one place, making the code more readable and maintainable. They allow you to structure your code better by keeping classes that logically belong together, closer. Nested classes are declared inside another class and can access the outer class's members, depending on their type.

There are four types of nested classes in Java:
* Static Nested Classes
* Non-static Inner Classes
* Local Classes
* Anonymous Classes

## Static Nested Classes
A **static nested class** is a class that is nested within another class and is marked as static. It behaves like a `static` member of the outer class, which means:
* It does not have access to non-static members of the outer class.
* It can be instantiated without creating an instance of the outer class.
### Example
```
class OuterClass {
    static class StaticNestedClass {
        void display() {
            System.out.println("Inside static nested class.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass.StaticNestedClass nested = new OuterClass.StaticNestedClass();
        nested.display();
    }
}
```
In this example, `StaticNestedClass` can be instantiated directly using the outer class name (`OuterClass.StaticNestedClass`), and it does not depend on any instance of `OuterClass`.

** Use case:** Static nested classes are typically used when the behavior of the nested class does not depend on an instance of the outer class and is logically independent of the outer class instance.

## Non-static Inner Classes
A **non-static inner class** is an instance-level class that has access to both static and non-static members of the outer class. To create an instance of a non-static inner class, an instance of the outer class must first be created.

### Example
```
class OuterClass {
    class InnerClass {
        void display() {
            System.out.println("Inside non-static inner class.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        OuterClass.InnerClass inner = outer.new InnerClass();
        inner.display();
    }
}
```
In this example, `InnerClass` requires an instance of `OuterClass` to be created before it can be used.

**Use case:** Non-static inner classes are used when you need to access or modify the outer class's instance variables or methods.

## Local Classes
A **local class** is a class defined within a method or block of code. It is accessible only within the scope in which it is defined, making it useful for encapsulating logic that should not be accessible outside that block.

### Example
```
class OuterClass {
    void outerMethod() {
        class LocalClass {
            void display() {
                System.out.println("Inside local class.");
            }
        }
        LocalClass local = new LocalClass();
        local.display();
    }
}

public class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```
Here, `LocalClass` is defined inside the `outerMethod()` method, and its scope is limited to that method. It can only be instantiated and used within the `outerMethod()`.

**Use case:** Local classes are useful for short-term, method-specific tasks that do not need to be accessible elsewhere in the code.

## Anonymous Classes
An **anonymous class** is a class without a name that is typically used to provide an implementation for an interface or an abstract class. Anonymous classes are created and instantiated in a single statement.

### Example
```
interface Greet {
    void sayHello();
}

public class Main {
    public static void main(String[] args) {
        Greet greet = new Greet() {
            @Override
            public void sayHello() {
                System.out.println("Hello from anonymous class!");
            }
        };
        greet.sayHello();
    }
}
```
In this example, an anonymous class is used to implement the `Greet` interface and provide a specific implementation of the `sayHello()` method.

**Use case:** Anonymous classes are useful when a one-time implementation of an interface or abstract class is required, and there is no need to create a named class.

## Advantages of Nested Classes
* `Encapsulation:` Nested classes allow you to logically group classes that are used only in one place, increasing the code's readability and maintainability.
* `Modularity:` They help break down complex classes into smaller, more manageable pieces.
* `Access to Outer Class Members:` Non-static nested classes have access to both static and non-static members of the outer class, allowing for tighter integration between the classes.

## Use Cases of Nested Classes
* `Static Nested Classes` are often used for helper or utility classes that are tightly coupled with the outer class but do not require access to the outer class's instance members.
* `Non-static Inner Classes` are used when there is a tight association between the outer class and the inner class, and the inner class needs access to instance-level members of the outer class.
* `Local Classes` are ideal when a class is only required within the scope of a method or block of code.
* `Anonymous Classes` are useful for quick, one-off implementations, especially when working with interfaces or abstract classes.

## Conclusion
Nested and inner classes in Java are powerful way for organizing and structuring our code. They allow for encapsulating logic in a more modular and readable manner. By choosing the appropriate type of nested class whether static, non-static, local, or anonymous. We can create more efficient and maintainable code. Understanding when to use each type of nested class is key to writing cleaner, more modular Java programs.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/object-oriented-programming/abstractandinterfaces/AbstractAndInterfaces.md)