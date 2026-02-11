# 📖 Introduction to Java
Java is a versatile, platform-independent, object-oriented programming language used for developing a wide range of applications. Java is known for its Write Once, Run Anywhere principle.

## What is Java?
Java is a high-level, object-oriented programming language known for its platform independence, meaning Java programs can run on any device with a Java Virtual Machine (JVM). It was designed to be simple, secure and robust.

## Features of Java
* ``Platform Independence:`` Java programs are compiled into bytecode, which can be executed on any device with a JVM.
* ``Object-Oriented:`` Java is based on the concept of objects, allowing for modular and reusable code.
* ``Robustness:`` Java's strong type system and automatic memory management (garbage collection) make it robust and reliable.
* ``Security:`` Java's security features, like sandboxing and bytecode verification, protect against malicious code.
* ``Simplicity:`` Java was designed to be easy to learn and use, with a straightforward syntax and extensive documentation.

## Setting Up Java Development Environment
* ``Installing JDK:`` The Java Development Kit (JDK) contains tools like the Java compiler (javac) and the Java Runtime Environment (JRE). Download the JDK from the Oracle website and follow the installation instructions for your operating system.
* ``Setting Environment Variables:`` After installing the JDK, set the JAVA_HOME variable to the JDK installation directory and add the JDK's bin directory to the PATH variable. This allows you to run Java commands from any directory in your terminal or command prompt.

## Basic Syntax
1. ``Java Program Structure:`` A Java program consists of one or more classes. Each class contains methods, which contain the program's code. The entry point of a Java program is the main method.

```
public class MyClass {
    public static void main(String[] args) {
        // Program code goes here
    }
}
```

2. ``Writing and Running First Java Program:`` Write a simple "Hello, World!" program and save it as MyClass.java. Compile it using javac MyClass.java and run it using java MyClass.
3. ``Comments in Java:`` Java supports single-line (//) and multi-line (/* */) comments. Comments are ignored by the compiler and are used for documentation and explanation.
```
// This is a single-line comment

/*
 * This is a multi-line comment
 * It can span multiple lines
 */
```
## Data Types and Variables
1. ``Primitive Data Types:`` Java has eight primitive data types: byte, short, int, long, float, double, char, and boolean. These are used to store simple values like numbers and characters.
2. ``Reference Data Types:`` Reference types, also called objects, are instances of classes. They include classes, arrays, and interfaces.
3. ``Variables and Constants:`` Variables are used to store data values. They must be declared with a data type before they can be used. Constants are variables whose values cannot be changed after initialization, declared using the final keyword.
4. ``Type Conversion (Casting):`` Java supports automatic type conversion (implicit casting) for compatible data types. For incompatible types, explicit casting is required.
```
int x = 10;
double y = x; // implicit casting
double z = 10.5;
int w = (int) z; // explicit casting
```

## Operators
1. ``Arithmetic Operators:`` Arithmetic operators are used to perform mathematical operations like addition, subtraction, multiplication, division, and modulus.
2. ``Relational Operators:`` Relational operators are used to compare values. They return a boolean value (true or false).
3. ``Logical Operators:`` Logical operators are used to perform logical operations like AND (&&), OR (||), and NOT (!).
4. ``Assignment Operators:`` Assignment operators are used to assign values to variables.
5. ``Conditional (Ternary) Operator:`` The conditional operator (? :) is used to make decisions based on a condition.
```
int x = 10;
int y = 20;
int max = (x > y) ? x : y;
```

## Control Flow
1. ``If-Else Statements:`` If-else statements are used to execute code based on a condition.
2. ``Switch Statements:`` Switch statements are used to execute different blocks of code based on different conditions.
3. ``Loops:`` Loops are used to execute a block of code repeatedly. Java supports for, while, and do-while loops.
4. ``Break and Continue Statements:`` The break statement is used to exit a loop or switch statement. The continue statement is used to skip the current iteration of a loop.
```
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        continue; // skip iteration if i is 5
    }
    if (i == 8) {
        break; // exit loop if i is 8
    }
    System.out.println(i);
}
```

## Arrays
1. ``Declaring and Initializing Arrays:`` Arrays are used to store multiple values of the same type. They must be declared with a specific size or initialized with values.
2. ``Accessing Array Elements:`` Array elements are accessed using their index. Arrays are zero-indexed, meaning the first element has an index of 0.
3. ``Multidimensional Arrays:`` Arrays can have multiple dimensions, represented as arrays of arrays.
4. ``Array Methods:`` The java.util.Arrays class provides methods for working with arrays, such as sorting and searching.
```
int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers[0]); // prints 1
int[][] matrix = {{1, 2}, {3, 4}};
System.out.println(matrix[0][1]); // prints 2
Arrays.sort(numbers);
```

## Methods
1. ``Declaring and Calling Methods:`` Methods are declared within classes and contain a block of code. They can be called from other methods or objects.
2. ``Method Parameters and Return Types:`` Methods can have parameters and return values. Parameters are variables passed to the method, and the return type defines the type of value the method returns.
3. ``Method Overloading:`` Method overloading allows a class to have multiple methods with the same name but different parameters.
4. ``Recursion:`` Recursion is a technique in which a method calls itself to solve a problem.

[< Previous Page](https://github.com/nakulmitra/java-tutorial) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/introduction-to-java/JavaHistory.md)