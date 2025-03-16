# Thread Synchronization in Java
Thread synchronization is a crucial concept in Java when working with multithreading. It ensures that multiple threads do not interfere with each other while accessing shared resources, preventing issues such as race conditions and inconsistent data.

## What is Thread Synchronization?
Thread synchronization is the mechanism of controlling the execution of multiple threads to ensure **data consistency** when accessing shared resources.

### Why is Synchronization Needed?
When multiple threads access a **shared resource simultaneously**, it can lead to:
* `Race conditions:` Two or more threads modifying shared data at the same time.
* `Data inconsistency:` One thread modifies data while another thread reads an outdated value.
* `Unpredictable results:` Different execution orders may lead to unexpected behaviors.

## Understanding Race Conditions
A **race condition** occurs when multiple threads try to modify a shared resource simultaneously, leading to incorrect results.

### Example Without Synchronization (Race Condition)
```
class BankAccount {
    private int balance = 100;

    public void withdraw(int amount) {
        if (balance >= amount) {
            System.out.println(Thread.currentThread().getName() + " is withdrawing: " + amount);
            balance -= amount;
            System.out.println(Thread.currentThread().getName() + " new balance: " + balance);
        } else {
            System.out.println(Thread.currentThread().getName() + " insufficient balance.");
        }
    }

    public int getBalance(){
        return balance;
    }
}

public class RaceConditionExample {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        Runnable task = () -> account.withdraw(80);

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();

        Thread.sleep(5000);
        System.out.println("Final amount:" + account.getBalance());
    }
}
```
### Possible Incorrect Output (Due to Race Condition)
```
Thread-1 is withdrawing: 80
Thread-2 is withdrawing: 80
Thread-1 new balance: 20
Thread-2 new balance: -60
Final amount: -60
```
**Issue:** Both threads read the balance as `100` before modifying it, leading to an incorrect final balance.

* **Solution:** Use **synchronization** to ensure only one thread executes the critical section at a time.

## Types of Synchronization
Java provides three main ways to synchronize threads:
1. **Synchronized Methods**
2. **Synchronized Blocks**
3. **Static Synchronization**

### Synchronized Methods
A **synchronized method** ensures that only **one thread at a time** can execute the method.

### Example: Using Synchronized Method
```
class BankAccount {
    private int balance = 100;

    // Synchronized Method
    public synchronized void withdraw(int amount) {
        if (balance >= amount) {
            System.out.println(Thread.currentThread().getName() + " is withdrawing: " + amount);
            balance -= amount;
            System.out.println(Thread.currentThread().getName() + " new balance: " + balance);
        } else {
            System.out.println(Thread.currentThread().getName() + " insufficient balance.");
        }
    }
}
```
* **Correct Output (Race Condition Prevented)**
```
Thread-1 is withdrawing: 80
Thread-1 new balance: 20
Thread-2 insufficient balance.
Final amount: 20
```
**How it works?**
* The `synchronized` keyword ensures that **only one thread** can execute the `withdraw` method at a time.

### Synchronized Blocks
Instead of synchronizing an entire method, **a synchronized block** allows you to **lock only a specific critical section**, improving performance.

### Example: Using Synchronized Block
```
class BankAccount {
    private int balance = 100;

    public void withdraw(int amount) {
        // Synchronizing Only the Critical Section
        synchronized (this) {
            if (balance >= amount) {
                System.out.println(Thread.currentThread().getName() + " is withdrawing: " + amount);
                balance -= amount;
                System.out.println(Thread.currentThread().getName() + " new balance: " + balance);
            } else {
                System.out.println(Thread.currentThread().getName() + " insufficient balance.");
            }
        }
    }
}
```
### Why Use Synchronized Blocks?
* `More efficient:` Other methods can execute while only the critical section is locked.
* `Fine control:` **Only locks the required part** of the method instead of the whole method.

### Static Synchronization
If multiple threads access **static methods** that modify **shared static variables**, we must use **static synchronization** to prevent race conditions.

### Example Without Static Synchronization (Race Condition)
```
class Counter {
    private static int count = 0;

    // Race Condition: Multiple threads can modify 'count' simultaneously
    public static void increment() {
        count++;
    }

    public static int getCount() {
        return count;
    }
}

public class StaticSyncExample {
    public static void main(String[] args) {
        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                Counter.increment();
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.out.println("Inside catch block!!!");
        }

        System.out.println("Final Count: " + Counter.getCount());  
    }
}
```
* **Incorrect Output Due to Race Condition:**
```
Final Count: 1892 (Instead of 2000)
```

* **Fix Using Static Synchronization**
```
class Counter {
    private static int count = 0;

    public synchronized static void increment() { 
        count++;
    }

    public static int getCount() {
        return count;
    }
}
```
* **Correct Output:**
```
Final Count: 2000
```

## Thread.sleep() vs. Thread.yield()
### Thread.sleep(milliseconds)
* Pauses the **current thread** for a specified time (in milliseconds).
* **Does NOT release the lock** if inside a synchronized block.
```
Thread.sleep(2000);  
```

### Thread.yield()
* Suggests the scheduler to pause the current thread and give CPU time to another waiting thread.
* Does NOT guarantee immediate yielding.
```
Thread.yield(); 
```

| Feature            | `Thread.sleep()` | `Thread.yield()` |
|--------------------|----------------|----------------|
| Effect            | Pauses execution | Suggests to yield CPU |
| Guarantee?        | Yes (definite pause) | No (depends on scheduler) |
| Lock Release?     | No | No |

## Best Practices for Synchronization
* `Minimize synchronization:` Only synchronize when necessary to improve performance.
* `Use synchronized blocks instead of methods:` Provides better control and efficiency.
* `Use `volatile` for single-variable synchronization:` Ensures visibility of shared variables.
* Prefer `ReentrantLock` over `synchronized` when advanced locking is needed.

## Conclusion
* Thread synchronization **prevents race conditions** and **ensures thread safety**.
* Use `synchronized` methods, blocks, or static synchronization **based on the requirement**.
* Be mindful of **performance impacts** while using synchronization mechanisms.