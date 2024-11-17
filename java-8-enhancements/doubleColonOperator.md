# Method References in Java (Double Colon :: Operator)
The double colon (::) operator, also known as the method reference operator, is a feature introduced in Java 8. It is a shorthand syntax for referring to methods or constructors without explicitly invoking them. Method references are a more concise way to use lambda expressions in functional programming and are especially useful when working with the **Stream API** or other functional interfaces.

## What Is the Double Colon (::) Operator?
The double colon operator allows us to refer to:
* Static methods
* Instance methods
* Constructors

It provides a clean and readable alternative to using lambda expressions in cases where the lambda merely calls an existing method.
### For example:
**Instead of writing:**
```
names.forEach(name -> System.out.println(name));
```

**We can write:**
```
names.forEach(System.out::println);
```

## Types of Method References
There are four primary types of method references in Java:
* **Reference to a Static Method**
This is used to refer to static methods of a class.
### Syntax
```
ClassName::staticMethodName
```

### Example
```
import java.util.Arrays;
import java.util.List;

public class StaticMethodRefExample {
    public static void printUpperCase(String s) {
        System.out.println(s.toUpperCase());
    }

    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.forEach(StaticMethodRefExample::printUpperCase);
    }
}
```

### Explanation
* StaticMethodRefExample::printUpperCase refers to the static method printUpperCase.
* Each element in the list is passed to this method during iteration.

* **Reference to an Instance Method of a Specific Object**
This type refers to an instance method of a particular object.

### Syntax
```
instance::instanceMethodName
```

### Example
```
import java.util.Arrays;
import java.util.List;

public class InstanceMethodRefExample {
    public void printName(String name) {
        System.out.println("Hello, " + name);
    }

    public static void main(String[] args) {
        InstanceMethodRefExample example = new InstanceMethodRefExample();
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.forEach(example::printName);
    }
}
```

### Explanation
* example::printName refers to the printName method of the specific object example.
* Each element in the list is passed to the method.

* **Reference to an Instance Method of an Arbitrary Object of a Particular Type**
This refers to instance methods, but instead of referring to a specific object, it applies to arbitrary objects of the specified type.

### Syntax
```
ClassName::instanceMethodName
```

### Example
```
import java.util.Arrays;
import java.util.List;

public class ArbitraryObjectMethodRefExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        names.stream()
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

### Explanation
* String::toUpperCase refers to the toUpperCase method of the String class.
* It applies the method to each element in the stream.

* **Reference to a Constructor**
This is used to create a new object using its constructor.

### Syntax
```
ClassName::new
```

### Example
```
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

class Person {
    String name;

    Person(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return name;
    }
}

public class ConstructorRefExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        List<Person> people = names.stream()
                                   .map(Person::new)
                                   .collect(Collectors.toList());

        people.forEach(System.out::println);
    }
}
```

### Explanation
* Person::new refers to the constructor of the Person class.
* Each name in the list is passed to the constructor to create a new Person object.

## When to Use Method References vs. Lambda Expressions
| Use Method References | Use Lambda Expressions |
| ----------------|-------|
|    When the lambda expression is a direct call to an existing method.     |  When the logic requires additional operations.  |
|    Example: list.forEach(System.out::println);     |  Example: list.forEach(name -> System.out.println(name.toUpperCase()));  |

## Combining Method References with Streams
Method references are often used in stream pipelines for operations like mapping, filtering, and printing.
### Example
```
import java.util.Arrays;
import java.util.List;

public class StreamMethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "bob", "Charlie");

        names.stream()
             .map(String::toUpperCase)          // Convert each name to uppercase
             .sorted(String::compareToIgnoreCase) // Sort names ignoring case
             .forEach(System.out::println);    // Print each name
    }
}
```

## Limitations of Method References
* Method references are only useful when the method being referred to matches the functional interface’s signature.
* If additional logic is required, lambdas are more suitable.

## Advantages of the Double Colon (::) Operator
* `Improved Readability:` Reduces boilerplate code by replacing verbose lambda expressions.
* `Functional Programming Style:` Fits naturally into Java's functional programming paradigm introduced in Java 8.
* `Reusability:` Methods and constructors can be reused without duplicating logic.
* `Consistency:` Works seamlessly with the Stream API and other functional interfaces.


## Key Takeaways
* The double colon (::) operator is a shorthand for referring to methods and constructors.
* It simplifies the code and enhances readability, especially in functional programming contexts.
* Use the appropriate type of method reference based on our use case:
1. Static methods for utility operations.
2. Instance methods for actions tied to specific objects.
3. Arbitrary object methods for operations on stream elements.
4. Constructors for object creation in pipelines.

## Conclusion
By understanding and using the double colon (::) operator effectively, we can write more concise and maintainable Java code. Mastering this feature is essential for anyone diving into functional programming in Java.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/lambda-expressions.md)