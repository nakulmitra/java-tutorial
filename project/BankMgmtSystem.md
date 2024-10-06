# Bank Management System Project in Java (Using OOP Concepts)

## Introduction
In this project, we are building a **Bank Management System using key Object-Oriented Programming (OOP)** concepts in Java. This system simulates real-world banking features such as account creation, deposit, withdrawal, balance inquiry, and fund transfer. It is a simple yet powerful example to showcase how OOP principles can be applied to solve real-world problems.

[![](https://markdown-videos-api.jorgenkh.no/youtube/wY0fUVH-8TE)](https://youtu.be/wY0fUVH-8TE)

We will cover the following OOP concepts:
* `Encapsulation:` Protecting the data of accounts by limiting direct access through public methods.
* `Inheritance:` Using a base class to define shared properties and methods, with specialized subclasses for different types of accounts.
* `Polymorphism:` Overriding methods to customize behavior for specific account types.
* `Abstraction:` Simplifying complex operations like banking into easy-to-use interfaces and methods.

## Class Structure Overview
### Account (Base Class)
The `Account` class represents the base for all account types, encapsulating common properties and behaviors such as:
* `accountNumber:` The unique identifier for each account.
* `accountHolder:` The name of the person holding the account.
* `balance:` The current balance of the account.

#### Key methods:
* `deposit(double amount):` Adds the specified amount to the balance.
* `withdraw(double amount):` Subtracts the specified amount from the balance if sufficient funds are available.
* `checkBalance():` Displays the current balance.

### SavingsAccount (Subclass)
The SavingsAccount class inherits from Account and introduces a new property:
* `interestRate:` The interest rate associated with the savings account.

#### Additional methods:
* `addInterest():` Adds interest to the balance based on the interest rate.

### CurrentAccount (Subclass)
The CurrentAccount class also inherits from Account but includes an additional feature:
* `overdraftLimit:` Allows withdrawals even if the balance goes below zero, but only up to the overdraft limit.

#### Overridden methods:
* `withdraw(double amount):` Customizes the withdrawal logic to allow overdraft usage.

### Bank (Manager Class)
The `Bank` class manages a collection of `Account` objects. It provides methods to add accounts, find accounts, and transfer funds between them. This class demonstrates the power of polymorphism, as it works with both `SavingsAccount` and `CurrentAccount` objects through their shared `Account` interface.

## Step-by-Step Breakdown
* **Account Class (Base Class)**
The Account class serves as the parent class for all account types. It contains fields for storing common information and methods to operate on that data.
```
class Account {
    private String accountNumber;
    private String accountHolder;
    protected double balance;

    public Account(String accountNumber, String accountHolder, double balance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    public void deposit(double amount) {
        balance += amount;
        System.out.println(amount + " deposited. New balance: " + balance);
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println(amount + " withdrawn. New balance: " + balance);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    public void checkBalance() {
        System.out.println("Balance: " + balance);
    }

    public String getAccountNumber() {
        return accountNumber;
    }
}
```

* **SavingsAccount (Subclass)**
The SavingsAccount class inherits from Account and adds the capability to accrue interest.
```
class SavingsAccount extends Account {
    private double interestRate;

    public SavingsAccount(String accountNumber, String accountHolder, double balance, double interestRate) {
        super(accountNumber, accountHolder, balance);
        this.interestRate = interestRate;
    }

    public void addInterest() {
        double interest = balance * (interestRate / 100);
        deposit(interest);
        System.out.println("Interest added: " + interest);
    }
}
```

* **CurrentAccount (Subclass)**
The CurrentAccount class inherits from Account and introduces the concept of overdrafts.
```
class CurrentAccount extends Account {
    private double overdraftLimit;

    public CurrentAccount(String accountNumber, String accountHolder, double balance, double overdraftLimit) {
        super(accountNumber, accountHolder, balance);
        this.overdraftLimit = overdraftLimit;
    }

    @Override
    public void withdraw(double amount) {
        if (amount <= balance + overdraftLimit) {
            balance -= amount;
            System.out.println(amount + " withdrawn. New balance: " + balance);
        } else {
            System.out.println("Withdrawal exceeds overdraft limit.");
        }
    }
}
```

* **Bank Class (Manager Class)**
The Bank class is responsible for managing multiple accounts. It uses a List to store and operate on accounts, demonstrating how polymorphism works in Java.
```
import java.util.ArrayList;

class Bank {
    private ArrayList<Account> accounts = new ArrayList<>();

    public void addAccount(Account account) {
        accounts.add(account);
        System.out.println("Account added: " + account.getAccountNumber());
    }

    public Account findAccount(String accountNumber) {
        for (Account acc : accounts) {
            if (acc.getAccountNumber().equals(accountNumber)) {
                return acc;
            }
        }
        System.out.println("Account not found.");
        return null;
    }

    public void transferFunds(String fromAccountNumber, String toAccountNumber, double amount) {
        Account fromAccount = findAccount(fromAccountNumber);
        Account toAccount = findAccount(toAccountNumber);

        if (fromAccount != null && toAccount != null) {
            fromAccount.withdraw(amount);
            toAccount.deposit(amount);
            System.out.println("Transferred " + amount + " from " + fromAccountNumber + " to " + toAccountNumber);
        }
    }
}
```

* **Main Class (Simulation)**
The Main class brings everything together by creating accounts, performing transactions, and transferring funds between accounts.
```
public class Main {
    public static void main(String[] args) {
        Bank bank = new Bank();

        SavingsAccount savings = new SavingsAccount("SA123", "John Doe", 5000, 2.5);
        CurrentAccount current = new CurrentAccount("CA456", "Jane Smith", 10000, 2000);

        bank.addAccount(savings);
        bank.addAccount(current);

        savings.deposit(1000);
        current.withdraw(12000);  // With overdraft limit

        savings.addInterest();

        bank.transferFunds("SA123", "CA456", 500);
        savings.checkBalance();
        current.checkBalance();
    }
}
```

## Key OOP Concepts Used in This Project
* `Encapsulation:` We protect account details (`accountNumber`, `accountHolder`, `balance`) by using `private` and `protected` access modifiers, ensuring that account details can only be accessed or modified through controlled methods like `deposit()` and `withdraw()`.
* `Inheritance:` We create subclasses `SavingsAccount` and `CurrentAccount` that inherit from the base `Account` class. This allows these classes to share common properties and behaviors while adding their own specialized features.
* `Polymorphism:` The `Bank` class demonstrates polymorphism by working with `Account` objects. It doesn't need to know whether an account is a `SavingsAccount` or `CurrentAccount` — it simply treats them as `Account` objects and calls the appropriate methods.
* `Method Overriding:` The `CurrentAccount` class overrides the `withdraw()` method to allow for overdrafts, showing how subclasses can modify inherited behavior.

## Conclusion
This Bank Management System project demonstrates how powerful **Object-Oriented Programming (OOP)** concepts can be when applied to real-world applications. We created a modular and scalable system using `encapsulation`, `inheritance`, and `polymorphism` to ensure the code is flexible and maintainable.

You can easily extend this project by adding features such as:
* User authentication and account management
* Account history tracking
* Interest calculation for various account types
* Implementing a graphical user interface (GUI)

Feel free to explore the code and experiment with adding your own features!