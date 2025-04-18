# Java Optional Class
The **Optional** class, introduced in **Java 8**, is a powerful tool designed to handle null values in a cleaner, safer, and more functional way. By eliminating the need for explicit null checks, Optional improves code readability, reduces the risk of **NullPointerException**, and aligns Java with modern functional programming paradigms.

[![](https://markdown-videos-api.jorgenkh.no/youtube/K-q1G-b4jkc)](https://youtu.be/K-q1G-b4jkc)

## Why Was the Optional Class Introduced?
In Java, null values have been a common cause of errors, leading to the infamous **NullPointerException**. Traditionally, developers needed to write verbose code to handle null checks, which could result in cluttered and less readable code.
The Optional class addresses these issues by providing a container to represent the presence or absence of a value explicitly.

## Key Features of the Optional Class
### Null-Safe Programming:
* Optional eliminates the need for null checks and provides a clear API for handling potential null values.

### Functional Style:
* Encourages developers to adopt a more functional programming style using methods like `map`, `filter`, and `ifPresent`.

### Readable and Intent-Revealing:
* Code becomes more expressive, making it clear when a value might be absent and how to handle it.

## Creating Optional Objects
There are three ways to create an Optional object:
1. Using `Optional.of(value)`:
* Use this when the value is guaranteed to be non-null.
* Throws a `NullPointerException` if the value is null.
```
Optional<String> nonNullValue = Optional.of("Hello, Java 8!");
```

2. Using `Optional.ofNullable(value)`:
* Use this when the value might be null.
* Wraps a non-null value or creates an empty Optional if the value is null.
```
Optional<String> nullableValue = Optional.ofNullable(null);
```

3. Using `Optional.empty()`:
* Explicitly creates an empty Optional to represent an absent value.
```
Optional<String> emptyValue = Optional.empty();
```

## Accessing Values in Optional
1. `get()`:
* Retrieves the value if present; throws `NoSuchElementException` if empty.
* Use with caution!
```
String value = nonNullValue.get(); // Output: "Hello, Java 8!"
```

2. `orElse(defaultValue)`:
* Returns the value if present; otherwise, returns the provided default value.
```
String fallback = nullableValue.orElse("Default Value"); // Output: "Default Value"
```

3. `orElseGet(Supplier)`:
* Similar to `orElse` but allows lazy computation of the default value using a `Supplier`.
```
String fallback = nullableValue.orElseGet(() -> "Lazy Default Value");
```

## Performing Actions Conditionally
1. `ifPresent(Consumer)`:
* Executes the given action if the value is present.
```
nonNullValue.ifPresent(value -> System.out.println("Value: " + value));
```

2. `ifPresentOrElse(Consumer, Runnable)`:
* Performs an action if the value is present; otherwise, executes a fallback action.
```
nonNullValue.ifPresentOrElse(
    value -> System.out.println("Value: " + value),
    () -> System.out.println("Value is absent")
);
```

## Combining Optional Methods
1. `map(Function)`:
Transforms the value inside the Optional if present.
```
Optional<String> upperCase = nonNullValue.map(String::toUpperCase);
System.out.println(upperCase.orElse("No Value")); // Output: "HELLO, JAVA 8!"
```

2. `filter(Predicate)`:
* Retains the value only if it matches the given condition.
```
Optional<String> filtered = nonNullValue.filter(value -> value.startsWith("H"));
System.out.println(filtered.orElse("No Match")); // Output: "Hello, Java 8!"
```

## Real-World Example: Handling Database Results
The following example demonstrates how Optional can be used to handle null values when retrieving data from a simulated database:
* `Code Example:`
```
import java.util.Optional;

class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}

class UserRepository {
    public Optional<User> findUserById(int id) {
        if (id == 1) {
            return Optional.of(new User("Nakul", "nakul@example.com"));
        } else if (id == 2) {
            return Optional.of(new User("Sahil", null));
        } else {
            return Optional.empty();
        }
    }
}

public class OptionalExample {
    public static void main(String[] args) {
        UserRepository repository = new UserRepository();
        Optional<User> userOptional = repository.findUserById(1);

        userOptional.ifPresent(
            user -> {
                System.out.println("Name: " + user.getName());
                String email = Optional.ofNullable(user.getEmail()).orElse("No Email Provided");
                System.out.println("Email: " + email);
            });

        if(!userOptional.ifPresent()){
            System.out.println("User not found!!!");
        }
    }
}
```

`Explanation:`
* `Simulated Database:` The `UserRepository` simulates a database lookup, returning an Optional of User or an empty Optional.
* `Null Handling with Optional:` Ensures email is handled gracefully with `Optional.ofNullable()`.
* `Clear Code:` Eliminates manual null checks for user presence and email availability.

## Best Practices for Using Optional
* `Favor Safe Methods:` Use `orElse`, `orElseGet`, and `ifPresent` over `get()` to avoid runtime exceptions.
* `Avoid Overusing Optional:` Optional should not be used for every nullable field. Use it for return types of methods instead of method parameters or class fields.
* `Chain Methods for Complex Logic:` Combine `map`, `filter`, and `orElse` for expressive and concise code.

## Advanced Techniques
* `Chaining Operations:`
```
Optional<String> result = Optional.ofNullable("Dev Portal")
    .filter(value -> value.startsWith("D"))
    .map(String::toUpperCase);
System.out.println(result.orElse("No Match")); // Output: "DEV PORTAL"
```

* `Avoid NullPointerException in Streams:` Optional integrates well with the Stream API, helping handle null values gracefully.

## Conclusion
The **Optional** class is a powerful addition to Java that enables developers to handle null values safely and efficiently. By eliminating verbose null checks, Optional improves readability and reduces the risk of NullPointerException.

`Key Takeaways:`
* Use `Optional.of()`, `Optional.ofNullable()`, and `Optional.empty()` to create Optional objects.
* Use methods like `orElse`, `ifPresent`, and `map` for concise and functional code.
* Incorporate Optional into real-world scenarios, such as database handling, to write robust, error-free code.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/terminal-operations.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/functional-interface.md)