# Byte Data Type in Java
The `byte` data type in Java is a primitive data type that represents an 8-bit signed integer. This makes it the smallest integer data type in Java in terms of memory usage. A `byte` in Java occupies 1 byte of memory (8 bits), and its value ranges from **-128** to **127**.

The key characteristics of the `byte` data type are:
* `Size:` 8 bits (1 byte)
* `Value Range:` -128 to 127
* `Default Value:` 0

[![](https://markdown-videos-api.jorgenkh.no/youtube/m98bySz9EH8)](https://youtu.be/m98bySz9EH8)

## Why Use byte?
The `byte` data type is mainly used to save memory in large arrays where memory savings are critical. For example, when dealing with a large set of data such as an image or stream of data where you don’t need a larger data type like `int`, you can use `byte` to save space.

## Understanding the byte Data Type
1. ### 8-bit Signed Integer
The `byte` data type is called an 8-bit signed integer because it uses 8 bits to represent the value, and one of these bits is reserved to represent the sign (whether the value is positive or negative). The remaining 7 bits are used to represent the actual number.

2. ### Binary Representation
Since a `byte` uses 8 bits, there are **2^8** possible combinations of bits, which equals 256 unique values. These values range from **-128** to **127**.

#### Positive Values
* Positive numbers, including zero, are represented using simple binary numbers.
* The binary representation of 0 is `00000000` and for 1, it's `00000001`.
* The maximum positive value, 127, is represented as `01111111`.

#### Negative Values
* Negative numbers are represented using **two’s complement** notation.
* The minimum negative value, -128, is represented as `10000000`.
* The binary representation of -1 is `11111111`.

## Two’s Complement: How Negative Numbers are Represented
### What is Two's Complement?
In Java, negative numbers are stored using a method called **two’s complement**. This technique allows the computer to store negative numbers using the same set of bits as it uses for positive numbers.

### Steps to Calculate Two’s Complement
1. Start with the positive binary representation of the number.
2. Invert all the bits (flip 0s to 1s and 1s to 0s).
3. Add 1 to the inverted bits.
#### Example: Two’s Complement of -1
Let's walk through the process of finding the two’s complement of -1
1. Start with the binary representation of 1: `00000001`
2. Invert all the bits: `11111110`
3. Add 1 to the inverted bits: `11111111`
Thus, `11111111` represents `-1` in two's complement form.

### Why is the Range -128 to 127?
The range of `byte` is -128 to 127 because:
1. We have **256 possible combinations** of 8 bits.
2. These 256 values are split between **128 negative values** and **128 non-negative values** (including zero).
* Negative values range from -128 to -1.
* Non-negative values range from 0 to 127.
This gives a total range of **-128** to **127**, which sums up to 256 possible values.

## Examples of Using byte in Java
### Declaring a byte Variable
```
byte b = 10;  // A byte variable holding a positive value
byte c = -20; // A byte variable holding a negative value
```
### Byte Overflow Example
```
byte x = 127;
x++;  // This will cause overflow, and x will wrap around to -128
System.out.println(x);  // Output: -128
```
In the example above, when `x` exceeds 127, it overflows and becomes -128 because `byte` has a limited range.

## Why Use Two’s Complement?
Two’s complement is widely used in computers for the following reasons
* It simplifies the hardware required for arithmetic operations.
* There’s no need to handle separate cases for positive and negative numbers; addition, subtraction, and multiplication all work using the same binary rules.
* Zero has only one representation (`00000000`), which simplifies logic and storage.

## Conclusion
In summary, the byte data type in Java
* Occupies 8 bits of memory.
* Uses two's complement to represent both positive and negative integers.
* Has a range from -128 to 127.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/variables/IntroductionToVaraibles.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/variables/IntegralDataTypes.md)

