# Introduction
Inter-Thread Communication (ITC) in Java allows multiple threads to coordinate their execution efficiently when working with shared resources. Without proper communication, race conditions, data inconsistency, and wasted CPU cycles may occur.

Java provides built-in methods such as `wait()`, `notify()`, and `notifyAll()` to facilitate thread communication within a **synchronized block** or **synchronized method**.

## Why Is Inter-Thread Communication Needed?
In a **multi-threaded** environment, multiple threads may attempt to access or modify a shared resource concurrently. This can lead to:

* **Race Conditions** – Threads may access shared data simultaneously, leading to inconsistent results.
* **Deadlocks** – Threads may indefinitely wait for each other, causing the program to hang.
* **Wasted CPU Cycles** – If a thread continuously checks for a condition without waiting efficiently, it may cause high CPU usage.

* **Example Scenario:**
- **Producer-Consumer Problem** - A producer thread adds items to a queue, while a consumer thread removes items from it. If they don't communicate properly:
  - The **producer** may try to add items to a full queue.
  - The **consumer** may try to consume from an empty queue.
  - Both must coordinate using `wait()` and `notify()`.

## Java's Built-in Methods for Inter-Thread Communication
Java provides **three methods** for thread communication, which must be used inside a **synchronized block**:

| Method         | Description |
|---------------|------------|
| `wait()`      | Causes the current thread to wait until another thread calls `notify()` or `notifyAll()`. |
| `notify()`    | Wakes up **one** waiting thread. |
| `notifyAll()` | Wakes up **all** waiting threads. |

## Understanding wait(), notify(), and notifyAll() with Example

### Example: Message Passing Between Threads
```
class Message {
    private String message;
    private boolean hasMessage = false;

    public synchronized void sendMessage(String msg) {
        while (hasMessage) {  // If a message is already sent, then wait for it to be read
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("Inside catch block for sendMessage() method");
            }
        }
        this.message = msg;
        hasMessage = true;
        System.out.println("Sent: " + msg);
        notify();  // Notify the receiver thread
    }

    public synchronized void receiveMessage() {
        while (!hasMessage) {  // If no message is available, then wait
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("Inside catch block for receiveMessage() method");
            }
        }
        System.out.println("Received: " + message);
        hasMessage = false;
        notify();  // Notify the sender thread
    }
}

public class WaitNotifyExample {
    public static void main(String[] args) {
        Message msg = new Message();

        Thread sender = new Thread(() -> {
            String[] messages = {
                "Hello", "How are you?", "How's your day going?", "Goodbye"
            };

            for (String m : messages) {
                msg.sendMessage(m);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Sender");

        Thread receiver = new Thread(() -> {
            for (int i = 0; i < 4; i++) {
                msg.receiveMessage();
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Receiver");

        sender.start();
        receiver.start();
    }
}
```

### Expected Output:
```
Sent: Hello
Received: Hello
Sent: How are you?
Received: How are you?
Sent: How's your day going?
Received: How's your day going?
Sent: Goodbye
Received: Goodbye
```

### Explanation:
* The **sender thread** sends a message and waits if a message is already pending.
* The **receiver thread** receives the message and **notifies** the sender to send the next one.
* **Synchronization ensures** that only one thread accesses the message at a time.

## The Producer-Consumer Problem
### What is the Producer-Consumer Problem?
The **Producer-Consumer Problem** is a **classic multi-threading problem** where:
- The **Producer** generates data (e.g., adding items to a queue).
- The **Consumer** processes the data (e.g., removing items from a queue).

* **Challenges Without Synchronization:**
- If the **buffer is full**, the producer must wait.
- If the **buffer is empty**, the consumer must wait.
- If multiple consumers and producers run without synchronization, **race conditions** occur.

## Producer-Consumer Solution Using wait() and notifyAll()
```
import java.util.LinkedList;
import java.util.Queue;

class SharedBuffer {
    private final Queue<Integer> buffer = new LinkedList<>();
    private final int capacity;

    public SharedBuffer(int capacity) {
        this.capacity = capacity;
    }

    public synchronized void produce(int item) {
        while (buffer.size() == capacity) {  // If buffer is full, wait
            System.out.println("Producer waiting: Buffer is full...");
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("Inside catch block for produce() method");
            }
        }
        buffer.add(item);
        System.out.println("Produced: " + item);
        notifyAll();  // Notify all consumers that an item is available
    }

    public synchronized void consume() {
        while (buffer.isEmpty()) {  // If buffer is empty, wait
            System.out.println("Consumer waiting: Buffer is empty...");
            try {
                wait();
            } catch (InterruptedException e) {
                System.out.println("Inside catch block for consume() method");
            }
        }
        int item = buffer.poll();
        System.out.println("Consumed: " + item);
        notifyAll();  // Notify all producers that space is available
    }
}

public class ProducerConsumerExample {
    public static void main(String[] args) {
        SharedBuffer shared = new SharedBuffer(5);

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 20; i+=2) {
                try {
                    shared.produce(i);
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Even Number");

        Thread t2 = new Thread(() -> {
            for (int i = 1; i < 20; i+=2) {
                try {
                    shared.produce(i);
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Odd Number");

        Thread t3 = new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                try {
                    shared.consume();
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "Consumer");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### Expected Output:
```
Produced: 0
Produced: 1
Consumed: 0
Produced: 2
Consumed: 1
Produced: 3
...

```

### How This Solves the Synchronization Issue?
* `wait()` makes the producer **wait** when the buffer is full. 
* `wait()` makes the consumer **wait** when the buffer is empty.
* `notifyAll()` ensures that all **waiting threads** are notified when an item is produced or consumed.
* Synchronization **prevents race conditions** and **data inconsistency**.

## 7. Summary
* `wait()`, `notify()`, and `notifyAll()` allow threads to **communicate** effectively.
* A **shared resource** must always be accessed within a **synchronized block**.
* The **Producer-Consumer Problem** demonstrates real-world **thread synchronization challenges** and their solutions.

## **8. Conclusion**
Inter-Thread Communication is crucial for building **efficient, thread-safe applications**. Java's **wait() and notifyAll()** methods provide a powerful mechanism to avoid **busy waiting** and improve **CPU efficiency**.