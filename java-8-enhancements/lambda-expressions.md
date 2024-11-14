# Overview
Lambda Expressions were introduced in **Java 8** to bring **functional programming** capabilities to Java, simplifying code structure, improving readability, and reducing boilerplate code. They enable Java developers to write cleaner and more concise code, particularly when working with collections and streams.

## What is Functional Programming?
Functional programming is a programming paradigm focused on what to do rather than how to do it. It allows treating functions as **first-class citizens**, meaning:
* Functions can be passed as parameters to other functions.
* Functions can be returned as values.
* Functions can be assigned to variables.

Java’s inclusion of Lambda Expressions and other features like the **Stream API** in Java 8 added functional programming capabilities, enabling developers to write code that is more declarative and concise.

## What are Lambda Expressions?
A **Lambda Expression** in Java is an anonymous function, providing a way to write a function inline. It allows you to pass behavior (in the form of a function) as data, making your code more flexible and expressive.

Key Points:
Lambda expressions are often used to simplify inline implementations of interfaces with a single method (known as **functional interfaces**).
Lambdas help to reduce boilerplate code, especially in scenarios where you have simple, one-time-use functions.

### Example
Consider a scenario where we sort a list of strings alphabetically
* Without Lambda Expression
```
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});
```

* With Lambda Expression
```
Collections.sort(names, (a, b) -> a.compareTo(b));
```
As you can see, using a lambda expression makes the code shorter and more readable.

## Lambda Expression Syntax
The syntax of a lambda expression is:
```
(parameters) -> expression
(parameters) -> { statements }
```

### Syntax Variations
* No Parameters
```
() -> System.out.println("Hello, World!");
```

* One Parameter (no parentheses needed if there's only one parameter):
```
name -> System.out.println(name);
```

* Multiple Parameters
```
(a, b) -> a.compareTo(b);
```

* Block Body with Multiple Statements
```
(a, b) -> {
    System.out.println("Comparing " + a + " and " + b);
    return a.compareTo(b);
};
```

## Examples of Lambda Expressions
### Example 1: Sorting a List of Strings
```
List<String> names = Arrays.asList("Janet", "Aman", "Shreya");
Collections.sort(names, (a, b) -> a.compareTo(b));
System.out.println("Sorted names: " + names);
```

### Example 2: Filtering Even Numbers Using Stream API
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> evenNumbers = numbers.stream()
                                    .filter(n -> n % 2 == 0)
                                    .collect(Collectors.toList());
System.out.println("Even Numbers: " + evenNumbers); // Output: [2, 4, 6]
```

### Example 3: Transforming Data with map
```
List<String> names = Arrays.asList("Janet", "Aman", "Shreya");
List<String> uppercaseNames = names.stream()
                                   .map(name -> name.toUpperCase())
                                   .collect(Collectors.toList());
System.out.println("Uppercase Names: " + uppercaseNames); // Output: [JANET, AMAN, SHREYA]
```

## Functional Interfaces and Lambda Expressions
A **functional interface** in Java is an interface that has only one abstract method, which makes it eligible to be used with lambda expressions. Some commonly used functional interfaces in Java:
* Runnable (from java.lang)
* Comparator<T> (from java.util)
* Callable<V> (from java.util.concurrent)
* Predicate<T>, Function<T, R>, and Consumer<T> (from java.util.function)

### Creating a Custom Functional Interface
```
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}
```

### Using a Lambda Expression with Custom Interface
```
MathOperation addition = (a, b) -> a + b;
System.out.println("Sum: " + addition.operate(5, 3)); // Output: Sum: 8
```

## Benefits of Using Lambda Expressions
* `Concise Code` Lambda expressions reduce the need for boilerplate code by providing a more compact syntax.
* `Improved Readability` Lambda expressions make code easier to read, especially in scenarios where anonymous inner classes would otherwise be used.
* `Functional Programming Style` By allowing functions to be passed as arguments, lambda expressions enable a functional programming style, making code more expressive.
* `Enhanced API Usability` Java’s API, especially the Stream API, becomes much more powerful and flexible with lambda expressions.

## Best Practices for Using Lambda Expressions
1. `Keep Lambdas Concise` Use lambda expressions for simple operations. For more complex logic, consider using a regular method for clarity.
2. `Avoid Side Effects` Functional programming favors pure functions—those without side effects. Try to avoid modifying external variables within a lambda expression.
3. `Use Method References Where Possible` If a lambda expression only calls an existing method, use a method reference for cleaner code.

### Example
Instead of
```
list.forEach(item -> System.out.println(item));
```

Use
```
list.forEach(System.out::println);
```

## Conclusion
Lambda Expressions are a fundamental addition to Java 8, enabling a functional approach to Java programming. By writing code that is concise, expressive, and easy to read, lambda expressions help developers focus on the “**what**” rather than the “**how**”.

`Key Takeaways:`
* Lambda expressions allow us to pass behavior as data.
* They simplify the use of Java’s functional interfaces.
* They are especially useful when combined with the Stream API for data processing.