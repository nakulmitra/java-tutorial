# Functional Interfaces in Java

Functional interfaces are one of the core concepts introduced in **Java 8**. They enable **functional-style programming** by allowing us to pass behavior (functions) as arguments, making Java more expressive, concise, and readable.

Functional interfaces serve as the **foundation for lambda expressions, method references, and the Streams API**. In this document, we'll explore what functional interfaces are, why they matter, and how to use them effectively in real-world Java development.

## What Is an Interface in Java?

Before diving into functional interfaces, let's revisit the concept of an interface.

An **interface** in Java is a reference type that defines a **contract** - it contains method signatures without implementations. A class that implements an interface must provide implementations for all of its methods.

```
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Woof");
    }
}
```

**Key Points:**
- Interfaces enable **abstraction**.
- They support **polymorphism**.
- Java allows a class to implement **multiple interfaces**, supporting multiple inheritance of type.

## Why Do We Need Interfaces?

Interfaces help in:
- Designing loosely coupled systems.
- Promoting flexibility by programming to an interface, not an implementation.
- Sharing common behavior across unrelated classes (e.g., `Printer`, `Scanner`, and `Fax` all implementing `start()`).

## What Is a Functional Interface?

A **Functional Interface** is an interface that contains **only one abstract method**. It can have **any number of default or static methods**, but only a **single abstract method** (SAM). This is why it is also called a **SAM interface**.

### Key Features:
- Exactly **one abstract method**.
- Can contain **default** and **static methods**.
- Can **extend** other functional interfaces as long as the single abstract method rule is preserved.
- **@FunctionalInterface** annotation is **recommended** (but not mandatory).

### Example:

```
@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();
}

// Using lambda expression
MyFunctionalInterface task = () -> System.out.println("Hello from Lambda!");
task.doSomething(); // Output: Hello from Lambda!
```

## Why Use @FunctionalInterface Annotation?

The `@FunctionalInterface` annotation is **optional** but highly recommended. It:
- Ensures the interface **has only one abstract method**.
- Gives a **compile-time error** if someone accidentally adds more abstract methods.
- Clearly communicates the interface's purpose to developers.

```
@FunctionalInterface
interface Task {
    void perform();       // Only one abstract method
    // void anotherTask(); // Would cause compile-time error
}
```

## Real-World Use Cases of Functional Interfaces

Functional interfaces are the **backbone** of:
- **Lambda Expressions**
- **Method References**
- **Streams API**

### Lambda Expression Example:
```
Runnable runner = () -> System.out.println("Running...");
runner.run();
```

### Method Reference Example:
```
Consumer<String> printer = System.out::println;
printer.accept("Print this line");
```

### Streams API Example:
```
List<String> names = Arrays.asList("Dev", "Portal", "Java");
names.stream()
     .filter(name -> name.startsWith("D"))
     .forEach(System.out::println);
```

## Custom Functional Interface Example

```
@FunctionalInterface
interface Calculate {
    void calculate(int a, int b);
}

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        Calculate add = (a, b) -> System.out.println("Add: " + (a + b));
        add.calculate(6, 5);

        Calculate sub = (a, b) -> System.out.println("Subtract: " + (a - b));
        sub.calculate(6, 5);

        Calculate mult = (a, b) -> System.out.println("Multiply: " + (a * b));
        mult.calculate(6, 5);

        Calculate div = (a, b) -> System.out.println("Divide: " + (a / b));
        div.calculate(6, 5);
    }
}
```

## Built-in Functional Interfaces (from `java.util.function` package)

Java 8 provides many **predefined functional interfaces** such as:

| Interface      | Abstract Method       | Description                            |
|----------------|------------------------|----------------------------------------|
| `Predicate<T>` | `boolean test(T t)`    | Returns true/false                     |
| `Function<T, R>` | `R apply(T t)`       | Converts type T to type R              |
| `Consumer<T>`  | `void accept(T t)`     | Performs operation on T, no result     |
| `Supplier<T>`  | `T get()`              | Returns a result, takes no input       |
| `UnaryOperator<T>` | `T apply(T t)`     | Like Function, input and output are same type |
| `BinaryOperator<T>` | `T apply(T t1, T t2)` | Operates on two values of the same type |

## Benefits of Functional Interfaces

- Simplifies code using **lambda expressions** and **method references**.
- Enables **functional-style programming**.
- Enhances readability and reduces boilerplate.
- Improves testability by easily passing behavior as parameters.

## Summary

| Concept | Description |
|--------|-------------|
| Functional Interface | Interface with one abstract method |
| Annotation | `@FunctionalInterface` enforces single method |
| Usage | Lambda expressions, method references, Streams API |
| Benefit | Cleaner code, functional programming in Java |

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/optional-class.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/interview/string-stringbuilder-stringbuffer.md)