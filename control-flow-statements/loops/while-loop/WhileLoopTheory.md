# While Loop in Java

## Introduction:
Loops are a fundamental part of programming, allowing us to execute a block of code multiple times. In Java, the while loop is particularly useful when you need to repeat a task as long as a certain condition is true.

[![](https://markdown-videos-api.jorgenkh.no/youtube/w6Q9K-E_KmA)](https://youtu.be/w6Q9K-E_KmA)

## While Loop Syntax:
```
while (condition) {
    // code to be executed
}
```

## Key Components:
### 1. Condition:
* The loop continues to execute as long as this condition is true.
* Before each iteration, the condition is evaluated.
* If the condition is false at the beginning, the loop will not execute at all.

### 2. Loop Body:
* The block of code that you want to repeat.
* It can contain one or more statements.

### Example:
```
int i = 0;
while (i < 5) {
    System.out.println("i is: " + i);
    i++;
}
```

### Explanation:
1. The variable i is initialized to 0.
2. The while loop checks the condition i < 5 before each iteration.
3. If the condition is true, the loop body executes: it prints the value of i and increments i by 1.
4. This process repeats until i is no longer less than 5.

## Common Use Cases:
### 1. Reading Data:
* While loops are often used to read data until a certain condition is met, such as reading user input until a specific value is entered.

### 2. Processing Files:
* You can use a while loop to process each line of a file until the end of the file is reached.

### 3. Repeating Tasks:
* Any task that needs to be repeated a variable number of times based on dynamic conditions can utilize a while loop.