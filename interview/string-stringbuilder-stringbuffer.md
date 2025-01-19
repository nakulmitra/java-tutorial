# Understanding String, StringBuilder, and StringBuffer in Java  

In Java, handling text is a common task in almost every application. Java provides three main classes for managing and manipulating
text: **String**, **StringBuilder**, and **StringBuffer**. Each of these classes has unique characteristics, and understanding when 
to use them is essential for writing efficient, scalable, and maintainable code.

## 1. String in Java
**Definition**:  
A `String` in Java is an **immutable** sequence of characters. Once a `String` object is created, its value cannot be changed.  

**Key Features**:  
- **Immutability**: Any modification (e.g., concatenation or replacement) creates a new `String` object rather than altering the 
original one.  
- **Security**: Immutability ensures that strings are safe for use in multi-threaded environments.  
- **Caching**: String objects are stored in the **String Pool** for memory efficiency.  

**Example**:  
```
String str = "Dev Portal";
str = str.toUpperCase(); // Creates a new object: "DEV PORTAL"
System.out.println(str); // Output: DEV PORTAL
```

In the above example, the original `str` object ("Dev Portal") remains unmodified, and a new object is created for "DEV PORTAL."  

**Use Case**:  
- Use `String` for text that does not change often, such as configuration keys, constants, or log messages.  

## 2. StringBuilder in Java 
**Definition**:  
`StringBuilder` is a **mutable** class introduced in Java 5. It allows for modification of string content without creating new objects, making it faster and more memory-efficient for single-threaded applications.  

**Key Features**:  
- **Mutability**: Operations like `append()`, `insert()`, or `delete()` modify the same object.  
- **Not Thread-Safe**: StringBuilder does not synchronize its methods, making it unsuitable for multi-threaded environments.  

**Example**:  
```
StringBuilder sb = new StringBuilder("Dev");
sb.append(" Portal");
System.out.println(sb); // Output: Dev Portal
```

In the example, the original `StringBuilder` object is modified directly, avoiding the creation of new objects.  

**Use Case**:  
- Use `StringBuilder` in **single-threaded environments** where frequent string modifications are needed, such as loops or dynamic text generation.  

## 3. StringBuffer in Java
**Definition**:  
`StringBuffer` is similar to `StringBuilder` but with **thread-safe** methods. It synchronizes its operations, ensuring only one thread can access the object at a time.  

**Key Features**:  
- **Thread-Safe**: All methods are synchronized, making it suitable for multi-threaded applications.  
- **Performance Trade-off**: Synchronization introduces a slight performance overhead compared to `StringBuilder`.  

**Example**:  
```
StringBuffer sb = new StringBuffer("Dev");
sb.append(" Portal");
System.out.println(sb); // Output: Dev Portal
```

**Use Case**:  
- Use `StringBuffer` in **multi-threaded environments** where multiple threads may modify the same string.

## 4. Key Differences Between String, StringBuilder, and StringBuffer

| Feature            | **String**             | **StringBuilder**        | **StringBuffer**         |
|---------------------|------------------------|--------------------------|--------------------------|
| **Mutability**      | Immutable              | Mutable                  | Mutable                  |
| **Thread-Safety**   | Thread-safe            | Not thread-safe          | Thread-safe              |
| **Performance**     | Slower for modifications | Faster (single-threaded) | Slower (due to synchronization) |
| **Use Case**        | Fixed or rarely modified data | Frequent modifications in single-threaded environments | Frequent modifications in multi-threaded environments |

## 5. Practical Examples 

### Example 1: Comparing Performance
Let's compare the performance of `String`, `StringBuilder`, and `StringBuffer` when appending text repeatedly.  
```
public class PerformanceTest {
    public static void main(String[] args) {
        long startTime, endTime;

        // String
        String str = "Java";
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
            str += " Dev Portal";
        }
        endTime = System.currentTimeMillis();
        System.out.println("String Time: " + (endTime - startTime) + "ms");

        // StringBuilder
        StringBuilder sb = new StringBuilder("Java");
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
            sb.append(" Dev Portal");
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuilder Time: " + (endTime - startTime) + "ms");

        // StringBuffer
        StringBuffer sbf = new StringBuffer("Java");
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
            sbf.append(" Dev Portal");
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuffer Time: " + (endTime - startTime) + "ms");
    }
}
```

**Expected Output**:  
- `String`: Slowest, as new objects are created on every iteration.  
- `StringBuilder`: Fastest, as it modifies the same object.  
- `StringBuffer`: Slightly slower than `StringBuilder` due to thread-safety overhead.  

---

### Example 2: Thread Safety with StringBuffer
Let's demonstrate thread safety with `StringBuffer`.  

```
class SharedResource {
    private StringBuffer sb = new StringBuffer("Java"); // Replace with StringBuilder to compare

    public void appendText(String text) {
        sb.append(text);
        System.out.println(Thread.currentThread().getName() + ": " + sb);
    }
}

public class ThreadSafetyTest {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Runnable task1 = () -> {
            for (int i = 0; i < 5; i++) {
                resource.appendText(" Dev");
                try { 
                    Thread.sleep(50); 
                } catch (InterruptedException e) { 
                    System.out.println("Inside task 1 catch block");
                }
            }
        };

        Runnable task2 = () -> {
            for (int i = 0; i < 5; i++) {
                resource.appendText(" Portal");
                try { 
                    Thread.sleep(50); 
                } catch (InterruptedException e) { 
                    System.out.println("Inside task 2 catch block");
                }
            }
        };

        Thread t1 = new Thread(task1, "Thread-1");
        Thread t2 = new Thread(task2, "Thread-2");

        t1.start();
        t2.start();
    }
}
```

**Output**:  
- The `StringBuffer` ensures thread-safe operations.  
- We'll see consistent, non-corrupted results, even with multiple threads.  

## 6. Best Practices 
* Use `String` for constant or rarely modified data.  
* Use `StringBuilder` for single-threaded applications requiring frequent string modifications.  
* Use `StringBuffer` for multi-threaded applications to ensure thread safety.  

## 7. Summary 
- **String**: Immutable, thread-safe, best for fixed or rarely changed data.  
- **StringBuilder**: Mutable, fast, but not thread-safe - ideal for single-threaded applications.  
- **StringBuffer**: Mutable and thread-safe, best for multi-threaded environments.

By understanding the characteristics and use cases of `String`, `StringBuilder`, and `StringBuffer`, we can make informed decisions about which class to use in our Java applications. This knowledge not only helps us write efficient code but also prepares us for technical interviews where these concepts are often discussed.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-8-enhancements/optional-class.md)