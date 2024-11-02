# ArrayList and LinkedList in Java - Internal Implementation, Differences, and Use Cases
In Java, `ArrayList` and `LinkedList` are two commonly used implementations of the `List` interface in the Java Collections Framework. Both provide dynamic data structures, but they differ significantly in how they store elements, manage memory, and perform various operations. Understanding these differences is crucial for choosing the right data structure in Java applications.

[![](https://markdown-videos-api.jorgenkh.no/youtube/fexSEe6qshQ)](https://youtu.be/fexSEe6qshQ)

## What is an ArrayList?
### Overview
`ArrayList` is a resizable array implementation in Java, stored in contiguous memory locations. Unlike regular arrays, `ArrayList` can dynamically grow or shrink as elements are added or removed.

### Internal Structure
Internally, `ArrayList` maintains an array to store elements. This array has an initial capacity (default is 10) and automatically resizes when the number of elements exceeds its capacity. When resizing, `ArrayList` creates a new array that is 1.5 times the original capacity, copies the elements to this new array, and discards the old one.

### Key Characteristics
* `Dynamic Resizing:` The array doubles its size as needed, allowing flexibility.
* `Direct Access:` Elements can be accessed quickly by index due to contiguous memory storage.
* `Index-Based Operations:` Operations like `get()` and `set()` are fast, making `ArrayList` ideal for read-heavy applications.

### Common Methods
* `add(E element):` Adds the element to the end of the list.
* `remove(int index):` Removes the element at the specified index, shifting elements to maintain order.
* `get(int index):` Retrieves the element at the specified index.
* `set(int index, E element):` Replaces the element at the specified index with the given element.
* `size():` Returns the current number of elements.

### Example
```
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> shoppingList = new ArrayList<>();
        shoppingList.add("Milk");
        shoppingList.add("Bread");
        shoppingList.add("Eggs");

        System.out.println("Shopping List: " + shoppingList);

        shoppingList.remove("Bread");
        System.out.println("After removing Bread: " + shoppingList);

        System.out.println("First item: " + shoppingList.get(0));

        shoppingList.set(1, "Cheese");
        System.out.println("After updating: " + shoppingList);

        System.out.println("List size: " + shoppingList.size());
    }
}
```

### Time Complexity Analysis
* `Access (get):` O(1) - Direct access by index.
* `Insertion at End (add):` Amortized O(1) - Resizing happens occasionally.
* `Insertion/Deletion in Middle:` O(n) - Elements must be shifted to maintain order.

### When to Use ArrayList
* When the application requires fast access to elements using an index.
* Suitable for scenarios with minimal insertions and deletions at the middle or beginning.

## What is a LinkedList?
### Overview
`LinkedList` is a doubly linked list in Java, where each element is stored in a `Node` object. Each node contains a reference to both the previous and next nodes, making insertions and deletions efficient, especially at the beginning or end of the list.

### Internal Structure
A `LinkedList` comprises nodes linked to each other. Each node has three components:
* `Data:` The actual element stored.
* `Next:` Reference to the next node.
* `Previous:` Reference to the previous node (doubly linked).
The first node is called the head, and the last node is the tail.

### Key Characteristics
* `Sequential Access:` Nodes are not stored in contiguous memory, so accessing elements by index requires traversal from the head or tail.
* `Efficient Insertions/Deletions:` Insertion and deletion operations at both ends are fast.
* `Higher Memory Usage:` Each element requires additional memory for storing references to the previous and next nodes.

### Common Methods
* `add(E element):` Adds the element to the end of the list.
* `addFirst(E element):` Adds the element to the beginning.
* `addLast(E element):` Adds the element to the end.
* `removeFirst():` Removes the first element.
* `removeLast():` Removes the last element.
* `getFirst():` Retrieves the first element without needing an index.
* `getLast():` Retrieves the last element.

###
```
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> tasks = new LinkedList<>();
        tasks.add("Finish homework");
        tasks.add("Wash dishes");
        tasks.addFirst("Go for a walk");

        System.out.println("Task List: " + tasks);

        tasks.removeLast();
        System.out.println("After removing last task: " + tasks);

        System.out.println("First task: " + tasks.getFirst());
    }
}
```

### Time Complexity Analysis
* `Access (get):` O(n) - Requires traversal from the head or tail.
* `Insertion/Deletion at Head or Tail:` O(1) - No shifting or resizing needed.
* `Insertion/Deletion in Middle:` O(n) - Traversal is required to reach the target position.

### When to Use LinkedList
* When frequent insertions or deletions are required, especially at the beginning or end.
* Suitable for applications where sequential access is sufficient, and random access is not critical.

## Comparison: ArrayList vs LinkedList
| Feature | ArrayList | LinkedList |
| ----------------|-------|-------|
|    Underlying Structure     |  Dynamic array  |  Doubly linked list  |
|    Access Time     |  O(1) for random access  |  O(n)  |
|    Insertion at End    |  O(1)  |  O(1)  |
|    Insertion/Deletion in Middle      |  O(n)  |  O(n)  |
|    Memory Overhead     |  Lower (no extra pointers)  |  Higher (additional pointers)  |
|    Best for    |  Fast access by index  |  Frequent insertions/deletions  |

## Practical Use Cases
### ArrayList
* `Use Cases:` Shopping cart lists, maintaining a list of items in a collection that rarely changes in size, etc.
* `Best For:` Quick access by index for applications with minimal insertions/deletions.

### LinkedList
* `Use Cases:` Implementing a queue or deque, managing playlists where items are frequently added/removed, etc.
* `Best For:` Applications with frequent insertions or deletions, particularly from the start or end.

## Conclusion
Both `ArrayList` and `LinkedList` are powerful data structures in Java’s `Collections` Framework, each with its strengths and trade-offs. `ArrayList` provides fast access by index, making it ideal for read-heavy applications, while `LinkedList` excels in insertions and deletions due to its linked nature. The choice between these two often comes down to specific application requirements — considering factors like access speed, memory usage, and the frequency of insertions and deletions.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-collections-framework/list.md)