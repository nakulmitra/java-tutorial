# **Thread Lifecycle in Java**

In Java, **multithreading** is a crucial concept that allows multiple threads to run concurrently, improving performance and responsiveness in applications. A thread in Java undergoes multiple states during its lifetime, collectively known as the **Thread Lifecycle**.

[![](https://markdown-videos-api.jorgenkh.no/youtube/6sLXnypBWqA)](https://youtu.be/6sLXnypBWqA)

## **1. What is a Thread?**
A thread is the **smallest unit of execution** within a process. It allows parallel execution of tasks within a program, leading to **better resource utilization** and improved application performance.  

In Java, threads can be created in three ways:
1. **Extending the `Thread` class**
2. **Implementing the `Runnable` interface**
3. **Implementing the `Callable` interface**

## **2. Thread Lifecycle in Java**
A thread in Java undergoes the following states during its lifetime:

* **New**
* **Runnable**
* **Running**
* **Blocked**
* **Waiting**
* **Timed Waiting**
* **Terminated**

The following **state transition diagram** represents the Java Thread Lifecycle:

```
   +------------+       +-----------+
   |  New       | ----> | Runnable  |
   +------------+       +-----------+
         |                   |
         v                   v
    +-----------+       +-----------+       +--------------+
    | Running   |-----> | Blocked   |-----> | Waiting      |
    +-----------+       +-----------+       +--------------+
         |                   |                   |
         v                   v                   v
    +-----------+       +-----------+       +--------------+
    | Timed     |       |           |       |              |
    | Waiting   | ----> | Running   | ----> | Terminated   |
    +-----------+       +-----------+       +--------------+
```

Let's explore each of these states in detail.

## **3. Thread States and Transitions**

### **New State**
When a thread is **created but not yet started**, it is in the **New state**. This happens when an instance of the `Thread` class is created but `start()` has not been called.

* **Example:**
```
public class NewStateExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("Thread is running"));
        System.out.println("Thread State: " + t.getState());
    }
}
```

* **Key Points:**
- The thread is just an object at this stage.
- It hasn't entered the thread scheduler.

### **Runnable State**
A thread enters the **Runnable state** after calling `start()`. It is ready for execution but waiting for the CPU.

* **Example:**
```
public class RunnableStateExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("Thread is running"));
        t.start();
        System.out.println("Thread State: " + t.getState());
    }
}
```

* **Key Points:**
- The thread is **ready to run** but may not start immediately.
- The **thread scheduler** decides when it will run.

### **Running State**
A thread enters the **Running state** when the CPU picks it from the **Runnable queue** for execution.

* **Example:**
```
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is Running");
    }
}

public class RunningStateExample {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

* **Key Points:**
- The thread **actively executes** its task inside the `run()` method.
- It remains in this state **until it completes** or is interrupted.

### **Blocked State**
A thread enters the **Blocked state** when it tries to access a synchronized resource **already locked** by another thread.

* **Example:**  
```
class SharedResource {
    synchronized void accessResource() {
        System.out.println(Thread.currentThread().getName() + " is accessing!!!");
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            System.out.println("Inside catch block!!!");
        }
    }
}

public class BlockedThreadDemo {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        Thread t1 = new Thread(() -> resource.accessResource(), "Thread-1");
        Thread t2 = new Thread(() -> resource.accessResource(), "Thread-2");

        t1.start();
        t2.start();

        Thread.sleep(1000);

        System.out.println("Thread - 2 state: " + t2.getState());
    }
}
```

* **Key Points:**
- **Thread-2 enters the Blocked state** if **Thread-1 already owns the lock**.
- The thread **remains blocked until the lock is released**.

### **Waiting State**
A thread enters the **Waiting state** when it waits indefinitely for another thread to signal it (via `notify()`).

* **Example:**
```
class WaitingThreadDemo {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            synchronized (Thread.currentThread()) {
                try {
                    System.out.println("Thread is waiting");
                    Thread.currentThread().wait();
                    System.out.println("Thread is resumed!!!");
                } catch (InterruptedException e) {
                    System.out.println("Inside catch block!!!");
                }
            }
        });

        t1.start();
        Thread.sleep(1000);

        System.out.println("Thread state: " + t1.getState());
        Thread.sleep(3000);
        
        synchronized (t1) {
            t1.notify();
        }
    }
}
```

* **Key Points:**
- `wait()` puts the thread in the **Waiting state**.
- `notify()` wakes it up to **Runnable state**.

### **Timed Waiting State**
A thread enters the **Timed Waiting state** when it waits for a **fixed time** (e.g., `Thread.sleep()` or `join()`).

* **Example:**
```
class TimedWaitingExample {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            try {
                Thread.sleep(5000); 
            } catch (InterruptedException e) {
                System.out.println("Inside catch block!!!");
            }
        });

        t1.start();
        Thread.sleep(1000); 
        System.out.println("Thread State: " + t1.getState());
    }
}
```

* **Key Points:**
- The thread **automatically wakes up** after the specified time.

### **Terminated State**
A thread enters the **Terminated state** after completing execution or being stopped.

* **Example:**
```
public class TerminatedStateExample {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> System.out.println("Thread is running"));
        t.start();
        t.join(); 
        System.out.println("Thread State: " + t.getState());
    }
}
```

* **Key Points:**
- A **terminated thread cannot be restarted**.

## 4. Best Practices for Thread Management
* Use **ExecutorService** instead of manually creating threads.
* Avoid excessive use of **synchronized blocks** to prevent deadlocks.
* Always **handle `InterruptedException`** properly.
* Use **join()** to ensure threads finish execution in the correct order.

## 5. Conclusion
Understanding the **Thread Lifecycle** is critical for effective multithreading. Java provides robust mechanisms to manage thread states efficiently, ensuring smooth execution in concurrent applications.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/multithreading/create-thread.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/multithreading/thread-synchronization.md)