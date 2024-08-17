# Do-While Loop in Java
The do-while loop is a variation of the while loop in Java, designed to ensure that the code block inside the loop is executed at least once, even if the condition is false from the beginning. This is a key difference between the do-while loop and the standard while loop.

[![](https://markdown-videos-api.jorgenkh.no/youtube/nI2taTZaekk)](https://youtu.be/nI2taTZaekk)

## Syntax:
```
do {
    // code to be executed
} while (condition);
```

## How It Works:
### 1. Execution of Code Block: 
The code block inside the do statement is executed first, before the condition is tested.

### 2. Condition Check: 
After the execution of the code block, the while condition is evaluated. If the condition is true, the loop repeats, executing the code block again.

### 3. Loop Continuation: 
This process continues until the condition becomes false.

### 4. Guaranteed Execution: 
Since the condition is checked after the code block execution, the loop guarantees that the code block runs at least once, regardless of the condition's initial state.

## Example:
```
int i = 0;
do {
    System.out.println("i is: " + i);
    i++;
} while (i < 5);
```

## Explanation:
### 1. Initialization: 
int i = 0; initializes the loop control variable.

### 2. First Execution: 
The code block inside the do loop (System.out.println("i is: " + i);) is executed, printing the value of i (which is 0).

### 3. Increment: 
After printing, i is incremented by 1.

### 4. Condition Check: 
The condition i < 5 is checked. Since i is now 1, which is less than 5, the loop repeats.

### 5. Loop Continuation: 
The loop continues until i reaches 5. At that point, the condition i < 5 becomes false, and the loop terminates.

## Use Cases:
### 1. User Interaction: 
The do-while loop is particularly useful in scenarios where user interaction is required. For instance, when displaying a menu that should be shown at least once before asking the user to make a selection.

### 2. Input Validation: 
It's also effective for input validation, ensuring that the user is prompted for input at least once before any checks are performed.