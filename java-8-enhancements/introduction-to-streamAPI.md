# Stream API in Java
The Stream API, introduced in Java 8, is one of the most transformative additions to the language, enabling developers to process collections in a declarative, functional style. This guide explores the fundamentals, advantages, and practical usage of the Stream API, offering detailed insights and code examples.

## What Is the Stream API?
The Stream API is a powerful abstraction for processing data. It enables operations such as filtering, mapping, and reducing collections in a functional programming style.

Key Characteristics of the Stream API:
* `Declarative Programming:` Focuses on "what" to do, not "how" to do it.
* `Pipeline Architecture:` Combines a series of operations (intermediate and terminal) into a single stream pipeline.
* `Lazy Evaluation:` Intermediate operations are executed only when a terminal operation is invoked.
* `Immutable Data Processing:` Streams do not modify the original data source but work on a copy, ensuring thread safety.

## Differences Between Traditional Loops and Streams
| Aspect | Traditional Loops | Stream API |
| ----------------|-------|-------|
|    Programming Style     |  Imperative  |  Declarative  |
|    Focus     |  On "how" to achieve the result  |  On "what" the result should be  |
|    Code Verbosity    |  High due to manual iteration  |  Low, concise with predefined methods  |
|    Parallel Processing      |  Requires explicit multithreading code  |  Built-in parallelism support  |

## Example Comparison 
### Traditional Loop
```
List<String> names = Arrays.asList("Harshada", "Janet", "Shreya", "Aman", "Harika");
for (String name : names) {
    if (name.startsWith("H")) {
        System.out.println(name);
    }
}
```

### Stream API
```
names.stream()
     .filter(name -> name.startsWith("H"))
     .forEach(System.out::println);
```

## Creating Streams in Java
Streams can be created from various sources, such as collections, arrays, or even custom data structures.

### From Collections:
```
List<String> names = Arrays.asList("Harshada", "Janet", "Shreya", "Aman", "Harika");
Stream<String> nameStream = names.stream();
```

### From Arrays:
```
int[] numbers = {1, 2, 3, 4, 5};
IntStream numberStream = Arrays.stream(numbers);
```

### From Supplier (Infinite Stream):
```
Stream<Double> randomNumbers = Stream.generate(Math::random).limit(10);
randomNumbers.forEach(System.out::println);
```

## Stream Operations
Stream operations are divided into two categories:
* **Intermediate Operations** - Transform a stream into another stream (lazy evaluation).
**Examples:** `filter()`, `map()`, `sorted()`, `distinct()`.
* **Terminal Operations** - Trigger the pipeline and produce a result.
**Examples:** `forEach()`, `collect()`, `reduce()`, `count()`.

## Common Intermediate Operations
### filter()
Filters elements based on a predicate.
```
List<String> names = Arrays.asList("Harika", "Janet", "Harshada");
names.stream()
     .filter(name -> name.startsWith("H"))
     .forEach(System.out::println); // Output: Harika, Harshada
```

###  map()
Transforms each element using a mapping function.
```
List<String> names = Arrays.asList("Aman", "Sahil");
names.stream()
     .map(String::toUpperCase)
     .forEach(System.out::println); // Output: AMAN, SAHIL
```

### distinct()
Removes duplicate elements.
```
Stream.of(1, 2, 2, 3, 3)
      .distinct()
      .forEach(System.out::println); // Output: 1, 2, 3
```

### sorted()
Sorts elements in natural or custom order.
```
Stream.of(3, 1, 4, 2)
      .sorted()
      .forEach(System.out::println); // Output: 1, 2, 3, 4
```

## Common Terminal Operations
### forEach()
Performs an action for each element.
```
Stream.of("Harika", "Janet", "Harshada")
      .forEach(System.out::println);
```

### collect()
Gathers elements into a collection or custom structure.
```
List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("H"))
                                  .collect(Collectors.toList());
System.out.println(filteredNames); // Output: [Harshada, Harika]
```

### reduce()
Reduces elements into a single result using an accumulator.
```
int sum = Stream.of(1, 2, 3, 4, 5)
                .reduce(0, Integer::sum);
System.out.println(sum); // Output: 15
```

### count()
Counts the number of elements in a stream.
```
long count = Stream.of(1, 2, 3)
                   .count();
System.out.println(count); // Output: 3
```

## Benefits of Stream API
1. Concise Code:
* Eliminates boilerplate for loops and conditionals.
* Example:
```
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0)
                                   .collect(Collectors.toList());
```

2. Parallel Processing:
* Easily enable parallelism using `parallelStream()` for better performance on large datasets.
```
int sum = numbers.parallelStream()
                 .reduce(0, Integer::sum);
```

3. Lazy Evaluation:
* Intermediate operations are evaluated only when a terminal operation is invoked, ensuring efficiency.

4. Functional Style:
* Encourages functional programming, focusing on immutability and side-effect-free operations.

## Key Takeaways
* The Stream API provides a declarative way to process collections.
* It simplifies operations like filtering, mapping, and reducing.
* It supports parallel processing for performance optimization.
* Streams are immutable, ensuring thread safety in concurrent environments.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/doubleColonOperator.md)