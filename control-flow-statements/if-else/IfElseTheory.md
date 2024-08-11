If, Else, and Else If Statements in Java

Control flow statements in Java are fundamental for directing the execution flow based on certain conditions. Among the most essential control flow statements are if, else, and else if. These statements enable developers to create decision-making constructs within their programs.

1. If Statement
Definition:
The if statement allows you to execute a block of code only if a specified condition is true. This is useful for making decisions in your code based on dynamic conditions.

Syntax:
```
if (condition) {
    // Block of code to be executed if the condition is true
}
```

Example:
```
int number = 10;
if (number > 5) {
    System.out.println("The number is greater than 5");
}
```

Explanation:
In this example, the condition number > 5 is evaluated. Since 10 is greater than 5, the condition is true, and the code inside the if block executes, printing "The number is greater than 5" to the console.

2. Else Statement
Definition:
The else statement allows you to specify a block of code to be executed if the condition in the if statement is false. This provides an alternative path of execution when the initial condition is not met.

Syntax:
```
if (condition) {
    // Block of code to be executed if the condition is true
} else {
    // Block of code to be executed if the condition is false
}
```

Example:
```
int number = 3;
if (number > 5) {
    System.out.println("The number is greater than 5");
} else {
    System.out.println("The number is not greater than 5");
}
```

Explanation:
In this example, the condition number > 5 is false since 3 is not greater than 5. Therefore, the code inside the else block executes, printing "The number is not greater than 5" to the console.

3. Else If Statement
Definition:
The else if statement allows you to check multiple conditions. When the initial if condition is false, you can use else if to specify a new condition to be evaluated. This is useful for checking multiple conditions in a sequential manner.

Syntax:
```
if (condition1) {
    // Block of code to be executed if condition1 is true
} else if (condition2) {
    // Block of code to be executed if condition1 is false and condition2 is true
} else {
    // Block of code to be executed if both condition1 and condition2 are false
}
```

Example:
```
int number = 5;
if (number > 5) {
    System.out.println("The number is greater than 5");
} else if (number == 5) {
    System.out.println("The number is exactly 5");
} else {
    System.out.println("The number is less than 5");
}
```

Explanation:
In this example, the initial if condition number > 5 is false, so the program checks the else if condition number == 5. Since this condition is true, the code inside the else if block executes, printing "The number is exactly 5" to the console. If both the if and else if conditions were false, the code inside the else block would execute.

Summary:
* If Statement: Executes a block of code if the specified condition is true.
* Else Statement: Executes a block of code if the if condition is false.
* Else If Statement: Checks multiple conditions in a sequence, providing additional paths of execution.

These control flow statements are fundamental for implementing decision-making logic in Java programs. By using if, else, and else if statements, you can create dynamic and flexible code that responds to different conditions and inputs effectively.