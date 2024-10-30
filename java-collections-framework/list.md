# Java List Interface
The `List` interface in Java is part of the Java Collections Framework, a powerful library designed to help developers store, manage, and manipulate groups of objects efficiently. Unlike arrays, which are static and limited in functionality, `List` implementations are dynamic, resizable, and provide additional methods to enhance data management and manipulation.

[![](https://markdown-videos-api.jorgenkh.no/youtube/E9XEMlYlhmc)](https://youtu.be/E9XEMlYlhmc)

## Key Characteristics of Lists
* `Ordered Collection:` Lists maintain the insertion order of elements.
* `Allows Duplicates:` Lists can contain duplicate elements.
* `Zero-Based Indexing:` Elements are accessed using index positions, starting from `0`.
* `Dynamic in Size:` Unlike arrays, Lists can grow or shrink dynamically at runtime.

## Common Use Cases of Lists
* `To-Do Lists:` Where the order and occurrence of elements matter.
* `Dynamic Collections:` Shopping carts, user action history, etc., where the data size may vary.
* `Search Results:` Storing multiple results that need sequential access.

## Core Implementations of List Interface
Java provides several implementations of the `List` interface, with **ArrayList** and **LinkedList** being the most widely used. Each has distinct characteristics suited to different use cases.

### ArrayList
An `ArrayList` is a resizable array implementation of the `List` interface. It is particularly suited for situations where **random access** to elements is required.

#### Key Features
* `Backed by a dynamic array:` Expands as elements are added.
* `Fast random access:` Ideal for retrieving elements by index.
* `Slower insertion/removal from the middle:` Shifting elements to make space incurs an overhead.

#### Commonly Used Methods in ArrayList
| Method | Description |
| ----------------|-------|
|     add(element)     |  Adds the element at the end of the list.  |
|     add(index, element)     |  Adds the element at the specified index.  |
|    get(index)    |  Returns the element at the specified index.  |
|     remove(index)      |  Removes the element at the given index.  |
|     set(index, element)     |  Updates the element at the specified index.  |
|     size()     |  Returns the size (number of elements) of the list.  |

#### Example
```
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Creating an ArrayList of Strings
        ArrayList<String> shoppingList = new ArrayList<>();

        // Adding elements
        shoppingList.add("Milk");
        shoppingList.add("Bread");
        shoppingList.add("Eggs");

        System.out.println("Shopping List: " + shoppingList);

        // Removing an element
        shoppingList.remove("Bread");
        System.out.println("After removing Bread: " + shoppingList);

        // Getting an element by index
        System.out.println("First item: " + shoppingList.get(0));

        // Updating an element
        shoppingList.set(1, "Cheese");
        System.out.println("After updating: " + shoppingList);

        // List size
        System.out.println("List size: " + shoppingList.size());
    }
}
```

#### Internal Working of ArrayList
* `Storage:` Uses a dynamically resizing array.
* `Resize Logic:` When capacity is exceeded, `ArrayList` increases its size by 50%, which can lead to performance overhead due to element copying.

#### Time Complexity
* `Access by Index:` O(1)
* `Insertion (end):` O(1) (amortized)
* `Insertion/Removal (middle):` O(n) due to element shifting.

### LinkedList
`LinkedList` is a doubly-linked list implementation of the `List` interface. It’s well-suited for applications that require frequent **insertions and deletions at both ends** of the list.

#### Key Features
* `Doubly-linked nodes:` Each element (node) holds pointers to its previous and next nodes.
* `Efficient insertions/deletions at both ends:` Unlike `ArrayList`, no shifting is required.
* `Slower random access:` Accessing an element by index requires traversal.

#### Commonly Used Methods in LinkedList
| Method | Description |
| ----------------|-------|
|     add(element)     |  Adds the element at the end of the list.  |
|     addFirst(element)     |  Adds the element at the beginning.  |
|    addLast(element)    |  Adds the element at the end.  |
|     removeFirst()      |  Removes the first element.  |
|     removeLast()     |  Removes the last element.  |
|     getFirst()     |  Returns the first element in the list.  |
|     getLast()     |  Returns the last element in the list.  |

#### Example
```
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        // Creating a LinkedList of Strings
        LinkedList<String> tasks = new LinkedList<>();

        // Adding elements
        tasks.add("Finish homework");
        tasks.add("Wash dishes");
        tasks.addFirst("Go for a walk");  // Add at the beginning

        System.out.println("Task List: " + tasks);

        // Removing the last element
        tasks.removeLast();
        System.out.println("After removing last task: " + tasks);

        // Getting the first element
        System.out.println("First task: " + tasks.getFirst());
    }
}
```

#### Internal Working of LinkedList
* `Storage:` Uses nodes, each containing a data field and pointers to previous and next nodes.

#### Time Complexity
* `Access by Index:` O(n)
* `Insertion/Removal at ends:` O(1)
* `Insertion/Removal in the middle:` O(n) (since traversal is required).

## ArrayList vs. LinkedList: When to Use Which?
| Criteria | ArrayList |  LinkedList  |
| ----------------|-------|-----------|
|    Access by Index     |  Fast (O(1))  |  Slow (O(n))  |
|    Insertion at End     |  Fast (O(1))  |  Fast (O(1))  |
|    Insertion at Middle    |  Slow (O(n))  |  Slow (O(n))  |
|    Memory Overhead      |  Lower  |  Higher  |

## Choosing Between ArrayList and LinkedList
###  Use ArrayList when
* You need fast random access to elements.
* Insertions and deletions are infrequent or happen at the end.

### Use LinkedList when
* Frequent insertions and deletions are required at both ends.
* Random access is not critical.

## Conclusion
The `List` interface in Java is a versatile and powerful way to manage ordered collections of elements. **ArrayList** is optimized for **fast access** and is preferred when the order of elements is more critical than insertion/deletion efficiency. **LinkedList**, with its flexible node-based structure, is ideal for **frequent insertions and deletions**.

By understanding the differences between **ArrayList** and **LinkedList** and knowing their internal workings, you can make more informed choices to improve the performance and reliability of your Java applications.
