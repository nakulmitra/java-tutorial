# **Introduction**
In Java, handling concurrency properly is essential to ensure thread safety and avoid race conditions. Traditionally, the `synchronized` keyword was used for this purpose, but it has several limitations. To address these issues, Java introduced **Locks** (from `java.util.concurrent.locks`) and **Atomic Variables** (from `java.util.concurrent.atomic`).

[![](https://markdown-videos-api.jorgenkh.no/youtube/oiEXFKLNQpc)](https://youtu.be/oiEXFKLNQpc)

## Problems with `synchronized` Methods and Blocks
The `synchronized` keyword ensures that only one thread can execute a critical section at a time, preventing race conditions. However, it has several limitations:

### Limitations of `synchronized`
* **Thread Blocking** - If a thread enters a `synchronized` method/block, all other threads must wait, even if they only need to read shared data.
* **No Timeout Handling** - If a thread holding the lock gets stuck, other threads must wait indefinitely.
* **No Try-Lock Mechanism** - Threads cannot check if a lock is available without blocking.
* **Unfair Locking** - No control over which thread gets the lock next, leading to thread starvation.
* **Deadlocks** - If multiple threads hold locks and wait for each other to release them, the system may enter a deadlock.
* **Performance Issues** - Excessive blocking can lead to reduced CPU efficiency and slower execution.

### Example: The Problem with `synchronized`
```
class SharedCounter {
    private int count = 0;

    public synchronized void increment() {
        count++;
        System.out.println(Thread.currentThread().getName() + " - Count: " + count);
    }
}

public class SynchronizedProblem {
    public static void main(String[] args) {
        SharedCounter counter = new SharedCounter();

        Runnable task = () -> {
            for (int i = 0; i < 5; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();
    }
}
```

* This ensures thread safety but forces all threads to wait unnecessarily, impacting performance.

## Overcoming Limitations with Locks
Java provides the **Lock API (`java.util.concurrent.locks.Lock`)** to offer more flexibility in handling concurrency.

### Benefits of Locks over `synchronized`
* **Explicit Locking & Unlocking** - We have more control over acquiring and releasing locks.
* **Try-Lock Mechanism** - A thread can check if a lock is available without blocking.
* **Timeout Handling** - Threads can avoid waiting indefinitely.
* **Fairness Policy** - Ensures the longest-waiting thread gets the lock first.

### Example: Using Lock Instead of `synchronized`
```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class SharedCounter {
    private int count = 0;
    private final Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock();  // Acquiring the Lock
        try {
            count++;
            System.out.println(Thread.currentThread().getName() + " - Count: " + count);
        } finally {
            lock.unlock();  // Releasing the Lock
        }
    }
}

public class LockExample {
    public static void main(String[] args) {
        SharedCounter counter = new SharedCounter();

        Runnable task = () -> {
            for (int i = 0; i < 5; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();
    }
}
```

**Key Takeaways:**
* We explicitly acquire and release the lock, reducing the chances of deadlocks.
* Other threads don't wait unnecessarily if they don't need the lock.

## Introduction to Atomic Variables for Lock-Free Synchronization
While **Locks** prevent race conditions, they block threads, potentially impacting performance. **Atomic Variables** provide a non-blocking alternative.

### What are Atomic Variables?
* Atomic Variables (from `java.util.concurrent.atomic`) allow thread-safe operations **without using locks**.
* They use **hardware-level atomic operations** like **CAS (Compare-And-Swap)** for fast execution.
* This improves performance, especially in **high-concurrency scenarios**.

### Example: Using Atomic Variables
```
import java.util.concurrent.atomic.AtomicInteger;

class AtomicCounter {
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet();  // Atomic operation
        System.out.println(Thread.currentThread().getName() + " - Count: " + count.get());
    }
}

public class AtomicVariableDemo {
    public static void main(String[] args) {
        AtomicCounter counter = new AtomicCounter();

        Runnable task = () -> {
            for (int i = 0; i < 5; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();
    }
}
```

**Key Takeaways:**
* **Non-blocking execution** - Atomic variables avoid performance issues caused by locks.
* **Faster execution** - Best for simple counter-based operations.

## Best Practices for Using Locks and Atomic Variables
### Best Practices for Locks
* Always use **try-finally** to ensure the lock is released.
* Prefer **tryLock()** over blocking locks to avoid deadlocks.
* Use **ReadWriteLock** when reads are frequent but writes are rare.
* Avoid **nested locks** to prevent deadlocks.
* Use **fair locks (`new ReentrantLock(true)`)** if thread order matters.

### Best Practices for Atomic Variables
* Use **Atomic variables** for simple operations (increment, decrement, compare-and-swap).
* Avoid Atomic variables for **complex logic** (use Locks instead).
* **Don't mix Atomic Variables with Locks**, as this can lead to inconsistent results.

## Summary
**Key Takeaways:**
* **`synchronized` ensures thread safety** but has limitations like blocking, no timeout handling, and potential deadlocks.
* **Locks provide better control**, allowing timeout handling, fairness, and try-lock mechanisms.
* **Atomic Variables offer lock-free synchronization**, improving performance for simple operations.
* **Use Locks for complex operations** and **Atomic Variables for lightweight, frequent updates.**

By understanding and applying Locks and Atomic Variables properly, you can write efficient, high-performance multi-threaded applications in Java!

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/multithreading/thread-synchronization.md)