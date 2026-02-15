# For Loops in Java
A for loop is a control flow statement that allows code to be executed repeatedly based on a given Boolean condition. It is particularly useful when we know in advance how many times we want to execute a statement or a block of statements.

[![](https://markdown-videos-api.jorgenkh.no/youtube/oV7o5pzw4Zw)](https://youtu.be/oV7o5pzw4Zw)

## Syntax:
The syntax of a for loop in Java is:
```
for (initialization; condition; increment/decrement) {
    // code to be executed
}
```

## Break down each part of the for loop:
### 1. Initialization: 
This is executed only once, before the loop starts. It is used to initialize the loop control variable.

### 2. Condition: 
This is evaluated before each iteration of the loop. If the condition is true, the loop body is executed. If it is false, the loop terminates.

### 3. Increment/Decrement: 
This is executed after each iteration of the loop body. It is usually used to update the loop control variable.

## Example:
Here is a basic example of a for loop:
```
for (int i = 0; i < 5; i++) {
    System.out.println("i is: " + i);
}
```

## In this example:
1. int i = 0 is the initialization, which sets the starting value of i to 0.
2. i < 5 is the condition, which means the loop will run as long as i is less than 5.
3. i++ is the increment, which increases the value of i by 1 after each iteration.
4. The loop body System.out.println("i is: " + i); is executed five times, printing the values of i from 0 to 4.

## Iterating Over Arrays:
### For loops are often used to iterate over arrays.
```
int[] numbers = {10, 20, 30, 40, 50};
for (int i = 0; i < numbers.length; i++) {
    System.out.println("Number: " + numbers[i]);
}
```

In this example:
1. int[] numbers = {10, 20, 30, 40, 50}; initializes an array of integers.
2. for (int i = 0; i < numbers.length; i++) sets up a for loop that runs from i = 0 to i < numbers.length (i.e., from 0 to 4).
3. System.out.println("Number: " + numbers[i]); prints each element of the numbers array.

## Advantages of For Loops:
### 1. Clarity: 
For loops provide a clear and concise way to iterate over a range of values.
### 2. Control: 
They give us precise control over the initialization, condition, and increment/decrement steps.
### 3. Versatility: 
For loops can be used for a variety of tasks, such as iterating over arrays, collections, and other data structures.

## Use Cases:
* Counting iterations: When we need to perform an action a specific number of times.
* Traversing arrays or collections: When we need to access each element in an array or a collection.
* Performing repetitive tasks: When we need to repeat a block of code multiple times.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/control-flow-statements/loops/while-loop/WhileLoopTheory.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/control-flow-statements/loops/do-while-loop/DoWhileLoopTheory.md)