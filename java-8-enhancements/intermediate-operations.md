# Intermediate Operations in Stream API
The **Stream API** in Java provides a functional approach to processing data. Intermediate operations are a critical part of this functionality, allowing developers to transform, filter, and manipulate data in a concise, readable, and efficient manner. This document explains intermediate operations in detail, complete with examples, use cases, and best practices.

## What Are Intermediate Operations?
Intermediate operations in the Stream API are used to process and transform the elements of a stream. They are lazy, meaning they are not executed until a terminal operation (such as forEach, collect, or reduce) is invoked. This laziness allows the Stream API to optimize the execution of pipelines and reduce unnecessary computations.

Key Characteristics of Intermediate Operations
Lazy Execution: Intermediate operations are only executed when a terminal operation is called.
Return a Stream: Each intermediate operation returns a new stream, enabling method chaining.
Non-Destructive: They do not modify the original data structure but work on the data in the stream.

## Common Intermediate Operations
Here’s a detailed look at some of the most commonly used intermediate operations:
### filter(Predicate)
Filters elements based on a condition. Retains elements that match the condition and discards the rest.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class FilterExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Harshada", "Janet", "Shreya", "Aman", "Harika);

        names.stream()
             .filter(name -> name.startsWith("H")) // Retain names starting with "A"
             .forEach(System.out::println);        // Output: Harshada, Harika
    }
}
```

### map(Function)
Applies a transformation function to each element in the stream.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class MapExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Harshada", "Janet", "Aman");

        names.stream()
             .map(String::toUpperCase) // Convert each name to uppercase
             .forEach(System.out::println); // Output: HARSHADA, JANET, AMAN
    }
}
```

### flatMap(Function)
Converts a stream of collections into a single stream of elements, effectively flattening the nested structure.
#### Example: 
```
import java.util.Arrays;
import java.util.List;

public class FlatMapExample {
    public static void main(String[] args) {
        List<List<String>> nestedList = Arrays.asList(
            Arrays.asList("Janet", "Shreya"),
            Arrays.asList("Aman", "Sahil")
        );

        nestedList.stream()
                  .flatMap(List::stream) // Flatten nested lists
                  .forEach(System.out::println); // Output: Janet, Shreya, Aman, Sahil
    }
}
```

### distinct()
Eliminates duplicate elements from the stream.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class DistinctExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 4, 4, 5);

        numbers.stream()
               .distinct() // Remove duplicates
               .forEach(System.out::println); // Output: 1, 2, 3, 4, 5
    }
}
```

### sorted()
Sorts the elements in the stream. By default, it uses natural order, but you can also provide a custom comparator.
#### Natural Order Example:
```
import java.util.Arrays;
import java.util.List;

public class SortedExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Janet", "Shreya", "Aman");

        names.stream()
             .sorted() // Sort in natural order
             .forEach(System.out::println); // Output: Aman, Janet, Shreya
    }
}
```

#### Custom Order Example:
```
names.stream()
     .sorted((a, b) -> b.compareTo(a)) // Sort in reverse order
     .forEach(System.out::println); // Output: Shreya, Janet, Aman
```

### peek(Consumer)
Used to inspect elements as they pass through the pipeline. Commonly used for debugging.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class PeekExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Janet", "Shreya", "Aman");

        names.stream()
             .peek(name -> System.out.println("Processing: " + name)) // Inspect elements
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

### limit(long) and skip(long)
* `limit:` Restricts the number of elements processed by the stream.
* `skip:` Skips a specified number of elements.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class LimitSkipExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        numbers.stream()
               .limit(3) // Process only the first 3 elements
               .forEach(System.out::println); // Output: 1, 2, 3

        numbers.stream()
               .skip(3) // Skip the first 3 elements
               .forEach(System.out::println); // Output: 4, 5, 6
    }
}
```

### Combining Intermediate Operations
You can chain multiple intermediate operations to create a powerful data-processing pipeline.
#### Example:
```
import java.util.Arrays;
import java.util.List;

public class CombinedExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 2, 6, 4, 8, 8);

        numbers.stream()
               .filter(num -> num % 2 == 0) // Keep even numbers
               .map(num -> num * num)      // Square each number
               .distinct()                 // Remove duplicates
               .sorted((a, b) -> b - a)    // Sort in descending order
               .forEach(System.out::println); // Output: 64, 36, 16, 4
    }
}
```

## Key Points to Remember
* `Laziness:` Intermediate operations are not executed until a terminal operation is invoked.
* `Chaining:` Streams allow you to chain multiple operations, enabling concise and expressive code.
* `Efficiency:` Only the necessary elements are processed, optimizing performance.

## Best Practices
Use intermediate operations to build readable and maintainable pipelines.
Avoid modifying the original data structure during stream processing.
Use `peek` for debugging but remove it in production code for better performance.

## Conclusion
Intermediate operations in the Stream API are a cornerstone of Java’s functional programming features. By mastering these operations, you can process data efficiently and write cleaner, more expressive code. This document provided a comprehensive guide to the most commonly used intermediate operations, complete with examples and practical applications.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/introduction-to-streamAPI.md)