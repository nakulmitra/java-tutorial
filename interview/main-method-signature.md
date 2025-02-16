# Understanding `public static void main(String[] args)` in Java
The **`main` method** is the entry point of any Java application. It serves as the first method that the **Java Virtual Machine (JVM)** calls when executing a Java program. The signature of the `main` method in Java is:  

```
public static void main(String[] args)
```

Each keyword in this method has a **specific purpose**, making it recognizable and executable by the JVM. In this document, we will break down each component of the `main` method, explore its significance, and discuss different scenarios related to it.

## 1. Why Does Java Need a Main Method?
Java is a **platform-independent, object-oriented language**, and it requires a **defined entry point** for program execution. The `main` method acts as this entry point where execution starts.  

Without a valid `main` method, the JVM will **throw a runtime error**, and the program will not run.  

**Example of a valid Java program:**
```
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
**Output:**
```
Hello World!
```

## 2. Breaking Down `public static void main(String[] args)`

Each part of this method serves a crucial role:

| **Keyword**  | **Purpose**  |
|-------------|-------------|
| `public`    | Makes the method accessible to the JVM from anywhere. |
| `static`    | Allows JVM to call `main` without creating an instance of the class. |
| `void`      | Specifies that the method does not return any value. |
| `main`      | The predefined method name that JVM looks for as the entry point. |
| `String[] args` | Stores command-line arguments passed when running the program. |

## 3. Understanding Each Keyword in Detail

### Why `public`?
- The **JVM needs to access** the `main` method from **outside the class**.
- If the `main` method is not **public**, the JVM **won't be able to access it**, leading to a runtime error.

**Example (without `public`):**
```
class Main {
    static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
**Output:**
```
error: 'main' method is not declared 'public static'
```

### Why `static`?
- The `main` method is **called by the JVM before any objects are created**.
- If `main` were not static, the JVM would need to **create an object** of the class before calling it, which would be unnecessary overhead.
- Static methods **belong to the class itself** and not to a specific instance.

**Example (without `static`):**
```
class Main {
    public void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
**Output:**
```
error: 'main' method is not declared 'public static'
```

### Why `void`?
- The `main` method does **not return any value** to the JVM.
- The JVM is only responsible for executing the method and does not expect any return value.

**Example (changing `void` to `int`):**
```
class Main {
    public static int main(String[] args) {
        System.out.println("Hello World!");
        return 0;
    }
}
```
**Output:**
```
error: 'main' method is not declared with a return type of 'void'
```

### Why `main`?
- The **JVM specifically looks for a method named `main`** as the starting point.
- Renaming the method will cause a **runtime error**.

**Example (changing `main` to `start`):**
```
public class Main {
    public static void start(String[] args) {
        System.out.println("Hello World!");
    }
}
```
**Output:**
```
error: can't find main(String[]) method in class: demo.devportal.Main
```

### Why `String[] args`?
- Allows the program to accept **command-line arguments**.
- Each argument is stored as a **string in the array**.

**Example (using `args`):**
```
public class Main {
    public static void main(String[] args) {
        System.out.println("Inside main method!!!");

        for(String str : args){
            System.out.println(str);
        }

        System.out.println("End of main method!!!");
    }
}
```
**Run the program with arguments:**
```
devportal java tutorial
```
**Output:**
```
devportal
java
tutorial
```

## 4. Can We Modify the `main` Method?

### Can We Change the Order of `public` and `static`?
Yes! The order of `public` and `static` **doesn't matter**.
```
public class Main {
    static public void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
**Valid and will execute successfully.**

### Can We Overload the `main` Method?
Yes! But the JVM will always call the **standard `main` method**.
```
public class Main {
	 public static void main(String[] args) {
		System.out.println("Inside main method!!!");
		main(new int[] {1, 2, 3});
		System.out.println("End of main method!!!");
	}
	
	public static void main(int[] args) {
		System.out.println("Inside main method with int arguments!!!");
		
		for(int str : args) {
			System.out.println(str);
		}
		
		System.out.println("End of main method with int args!!!");
	}

}
```
**Output:**
```
Inside main method!!!
Inside main method with int arguments!!!
1
2
3
End of main method with int args!!!
End of main method!!!
```
The overloaded method **will not be executed automatically**.

### Can We Add Extra Modifiers like `final`, `synchronized`?
Yes! But it is **not commonly used**.
```
public static final void main(String[] args) {
    System.out.println("Hello World!");
}
```
**Valid and will execute successfully.**

```
public static synchronized void main(String[] args) {
    System.out.println("Hello World!");
}
```
**Valid but rarely used.**

### Can We Declare `main` as `abstract`?
No! Abstract methods **cannot have a body**, and `main` **requires a body**.
```
public abstract class Main {
    public abstract static void main(String[] args);
}
```
**Compilation error: Illegal combination of modifiers.**

## 5. Summary
- **`public`**: Required so that the JVM can access the `main` method.
- **`static`**: Allows execution without creating an object.
- **`void`**: No return value is expected by the JVM.
- **`main`**: The predefined method name recognized by the JVM.
- **`String[] args`**: Used for passing command-line arguments.

The `main` method **follows strict rules**, and any modification may lead to **compilation or runtime errors**.

## 6. Conclusion
Understanding the `main` method is **fundamental** for Java developers, especially for **interviews and coding assessments**. Following the correct method signature ensures our Java application runs smoothly.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/interview/doubelEqualsAndEqualsMethod.md)