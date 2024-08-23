# Switch Statement in Java

## Introduction:
The switch statement in Java is a control flow statement that allows you to execute one of many code blocks based on the value of a variable. It's an alternative to using multiple if-else statements and provides a more readable and organized way to handle multiple conditions.

[![](https://markdown-videos-api.jorgenkh.no/youtube/JRRFJfGw_HM)](https://youtu.be/JRRFJfGw_HM)

### Switch Statement Syntax:
```
switch (expression) {
    case value1:
        // Code to be executed if expression equals value1
        break;
    case value2:
        // Code to be executed if expression equals value2
        break;
    // More cases...
    default:
        // Code to be executed if expression doesn't match any case
        break;
}
```

## Key Components:
### 1. Expression:
* The switch statement evaluates the expression once and compares it with the values of each case.
* The expression must be of a type that can be converted to an integer, a string, an enum, or a character.

### 2. Case Labels:
* Each case label contains a value to compare with the switch expression.
* If the expression matches a case value, the corresponding block of code executes.

### Break Statement:
* The break statement terminates the switch statement.
* Without the break, execution would "fall through" to subsequent case labels, potentially causing unexpected behavior.
* Using break ensures that only the matched case block is executed.

### Default Case:
* The default case is optional and executes if no matching case labels are found.
* It's typically used to handle unexpected or default values.

## Example:
```
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    default:
        System.out.println("Weekend");
        break;
}
```

## Explanation:
* The variable day is set to 3.
* The switch statement evaluates the value of day and compares it with each case label.
* When it matches case 3, the statement System.out.println("Wednesday"); is executed.
* The break statement then terminates the switch statement, preventing fall-through to the next cases.
* If day had been any other value not matched by the case labels (e.g., 6 or 7), the default block would execute, printing "Weekend".

## Advantages of Using Switch Statements:
### 1. Readability:
* Switch statements are more readable than multiple if-else statements when dealing with numerous conditions.
* Each case is clearly separated, making the code easier to understand and maintain.

### 2. Performance:
* In some scenarios, switch statements can be more efficient than if-else chains, especially when the compiler can optimize the switch statement into a jump table.

### Organization:
* Switch statements help organize code by grouping related conditions together.
* This makes it easier to manage and update code, especially in large programs.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/control-flow-statements/if-else/IfElseTheory.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/tree/master/control-flow-statements/loops/while-loop)