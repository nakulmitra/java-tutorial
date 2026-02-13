### 🖋️ Variables in Java
In Java, variables are a fundamental concept that allows developers to store and manipulate data. A variable can be thought of as a "container" that holds values for processing. Just like containers in a kitchen hold different items, Java variables hold different types of data. Understanding variables is crucial for managing and using data in Java programs.

[![](https://markdown-videos-api.jorgenkh.no/youtube/3qSlNbmpTa0)](https://youtu.be/3qSlNbmpTa0)

## What is a Variable?
A **variable** in Java is a container for storing data values. Each variable must be declared with a specific data type that determines the kind of data the variable can hold, such as integers, floating-point numbers, characters, or more complex data like objects.

### Example
```
int age = 25;  // A variable that stores an integer value
```

### Key Points
* A variable stores data temporarily during program execution.
* Variables must be declared with a data type to specify what kind of data it can hold.

## Types of Variables in Java
Java has several types of variables, each serving different purposes. These variables can be categorized into **Primitive Data Types** and **Non-Primitive Data Types**.

1. ### Primitive Data Types
Primitive data types are the most basic types available in Java. They are predefined by the Java language and hold simple data values.
* `int:` Stores integers (whole numbers).
### Example
```
int num = 10;
```
* `float:` Stores floating-point numbers (decimal numbers).
### Example
```
float weight = 65.5f;
```
* `char:` Stores a single character.
### Example
```
char grade = 'A';
```
* `boolean:` Stores true or false values.
### Example
```
boolean isFresh = true;
```
2. ### Non-Primitive Data Types
Non-primitive data types, also known as reference types, are defined by the programmer and can be used to store objects, arrays, and instances of classes.
* `String:` Stores sequences of characters.
#### Example
```
String name = "John Doe";
```
* `Array:` Stores multiple values of the same type in a single variable.
#### Example
```
int[] numbers = {1, 2, 3, 4, 5};
```
* `Class/Objects:` Variables that store instances of user-defined classes.
#### Example
```
Car myCar = new Car();
```

## How to Declare Variables in Java
To declare a variable, we need to specify the data type followed by the variable's name and, optionally, assign a value.
### Syntax
```
dataType variableName = value;
```
### Example
```
int age = 25;
float height = 5.9f;
String name = "abc";
```

## Rules for Naming Variables
1. `Valid Characters:` Variable names can start with a letter, dollar sign ($), or an underscore (_). Subsequent characters can be letters, digits, dollar signs, or underscores. For example: `myAge`, `_counter`, `$balance`.
2. `No Reserved Keywords:` Variable names cannot be any Java reserved keywords, such as `int`, `class`, `public`.
3. `Case Sensitivity:` Java is case-sensitive, so `myAge` and `MyAge` would be treated as two different variables.
4. `Meaningful Names:` It's best practice to give our variables meaningful names that describe the data they store. For example:
```
int totalPrice; //Good
int tp; //Bad
```

## Primitive vs. Non-Primitive Data Types
Java has two categories of data types: **Primitive** and **Non-Primitive**.
### Primitive Data Types
* Include basic types like `int`, `float`, `char`, `boolean`.
* These types store actual values.
* They are not objects and do not belong to any class.
### Non-Primitive Data Types
* Include objects, arrays, and instances of classes.
* These types store references to the objects, not the actual data.
* Strings, arrays, and custom classes are examples of non-primitive types.

## Is Java Purely Object-Oriented?
While Java is often called an object-oriented programming language, it's not purely object-oriented because it includes primitive data types, which are not objects. Additionally:
* **Static methods** can be called without creating an object of the class, which deviates from the OOP principle where everything should be an object.
Thus, Java is considered a **mixed-paradigm** language, supporting **object-oriented**, **procedural**, and **functional programming** (with features like lambda expressions and functional interfaces introduced in Java 8).

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/architecture/jdk-jre-jvm/JDKvsJREvsJVM.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/variables/ByteDataType.md)