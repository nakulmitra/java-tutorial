# Introduction to Maps in Java
A **Map** in Java is a part of the Java Collections Framework and is designed to store data in **key-value pairs**. This data structure is extremely useful when you need a mapping between a unique key and a value, such as usernames and passwords, or employee IDs and names. Unlike other collections (e.g., List, Set), a Map does not allow duplicate keys but allows duplicate values.

## Key Characteristics of Maps
* `Key-Value Pair Storage:` Each entry in a Map is a pair consisting of a unique key and a value associated with that key.
* `No Duplicate Keys:` Each key must be unique; attempting to insert a duplicate key will overwrite the existing value.
* `Efficient Lookups:` Maps provide efficient methods to look up a value based on its key.

## Common Use Cases of Maps
* `Phone Directories:` Mapping names to phone numbers.
* `Product Catalogs:` Storing product IDs as keys and product details as values.
* `Configuration Settings:` Mapping setting names to their values in configuration files.

## Types of Maps in Java
Java provides three primary implementations of the Map interface: **HashMap**, **LinkedHashMap**, and **TreeMap**. Each has its own characteristics and use cases.

### HashMap
`HashMap` is a widely used implementation of the Map interface. It provides constant-time performance for basic operations like **insertion**, **deletion**, and **retrieval**, assuming there are no hash collisions.

* `Order of Elements:` HashMap does not maintain any order of its elements.
* `Performance:` Offers O(1) performance for `put`, `get`, and `remove` operations due to hashing.
* `Null Handling:` HashMap allows one `null` key and multiple `null` values.

#### How HashMap Works Internally
Internally, HashMap is implemented using an array of buckets. Each bucket holds a linked list or tree structure (from Java 8 onwards) to manage hash collisions. When a key-value pair is added, HashMap calculates a **hash code** for the key to determine the correct bucket.

* `Collision Handling:` If two keys have the same hash code, their values are stored in a linked list or tree structure within that bucket.
* `Dynamic Resizing:` When the map reaches a load factor threshold (default is 0.75), HashMap increases its capacity to reduce collisions.

#### Code Example
```
import java.util.HashMap;

public class HashMapDemo {
    public static void main(String[] args) {
        HashMap<String, String> phoneBook = new HashMap<>();
        phoneBook.put("Nakul", "123-456-7890");
        phoneBook.put("Harika", "987-654-3210");
        phoneBook.put("Janet", "012-345-6789");
        phoneBook.put("Nakul", "111-222-3333");  // Overwrites previous value for "Nakul"

        System.out.println("Phone Book: " + phoneBook);
        System.out.println("Harika's number: " + phoneBook.get("Harika"));
    }
}
```

#### In this example
* `Insertion:` Using the put() method.
* `Retrieval:` Using get() by passing the key.
* `Duplicate Handling:` The key "Nakul" is overwritten with a new value.

#### When to Use HashMap
Use HashMap when the order of elements is not important, and you need **fast insertion, deletion, and access**.

### LinkedHashMap
`LinkedHashMap` is similar to HashMap but with one key difference: it maintains the **insertion order** of elements.

* `Order of Elements:` LinkedHashMap maintains the insertion order, meaning elements will be returned in the order they were added.
* `Performance:` Slightly slower than HashMap due to the additional overhead of maintaining the linked list.
* `Null Handling:` Like HashMap, it allows one null key and multiple null values.

#### How LinkedHashMap Works Internally
LinkedHashMap inherits from HashMap but uses a **doubly linked list** to maintain the order of entries. Each entry stores references to the **next and previous entries**, making it possible to traverse the map in insertion order.

#### Code Example
```
import java.util.LinkedHashMap;

public class LinkedHashMapDemo {
    public static void main(String[] args) {
        LinkedHashMap<String, Integer> productPrices = new LinkedHashMap<>();
        productPrices.put("Laptop", 1000);
        productPrices.put("Smartphone", 700);
        productPrices.put("Tablet", 400);

        System.out.println("Product Prices in insertion order: " + productPrices);
    }
}
```

#### Explanation
* `Insertion Order:` Elements are stored and displayed in the order they were added.
* `Order-sensitive Operations:` LinkedHashMap is useful when you want a map with predictable iteration order.

#### When to Use LinkedHashMap
Use LinkedHashMap when you need fast access to elements while also maintaining **insertion order**.

### TreeMap
`TreeMap` is an implementation of the Map interface that stores keys in **sorted order**. By default, it uses **natural ordering** for sorting, but a custom comparator can be provided for different sorting criteria.

* `Order of Elements:` TreeMap sorts entries by the key’s natural ordering or by a custom comparator.
* `Performance:` Operations like `put()`, `get()`, and `remove()` are O(log n) due to the underlying Red-Black Tree structure.
* `Null Handling:` TreeMap does not allow `null` keys (throws `NullPointerException` if attempted) but allows `null` values.

#### How TreeMap Works Internally
TreeMap is implemented using a **Red-Black Tree**. Each entry is a node in the tree, and keys are arranged based on a sorting order. This allows fast in-order traversal, ensuring that the keys are always in sorted order.

#### Code Example
```
import java.util.TreeMap;

public class TreeMapDemo {
    public static void main(String[] args) {
        TreeMap<String, Integer> scores = new TreeMap<>();
        scores.put("Janet", 85);
        scores.put("Harika", 90);
        scores.put("Nakul", 75);

        System.out.println("Scores in sorted order: " + scores);
    }
}
```

#### Explanation
* `Sorted Order:` Elements are automatically sorted based on the keys.
* `Sorting by Comparator:` TreeMap is especially useful when the natural ordering of keys or a custom ordering is required.

#### When to Use TreeMap
Use TreeMap when you need a **sorted collection** of elements or require a specific ordering for the keys.

## Summary Comparison: HashMap, LinkedHashMap, and TreeMap
| Feature | HashMap | LinkedHashMap |  TreeMap  |
| ----------------|-------|-------|-----------|
|    Ordering     |  No guaranteed order  |  Insertion order  |  Sorted by keys |
|    Performance     |  O(1) for basic operations  |  Slightly slower than HashMap  |  O(log n) for basic operations  |
|    Null Keys   |  Allowed  |  Allowed  |  Not allowed  |
|    Use Case      |  Fast access with no order  |  Order-sensitive collections  |  Sorted key-value pairs  |

## Conclusion
Maps in Java offer a versatile way to store data as key-value pairs, each serving unique requirements. Here’s a recap:
* Use **HashMap** for fast access without caring about element order.
* Use **LinkedHashMap** when insertion order matters.
* Use **TreeMap** when you need a sorted collection of keys.

This understanding is crucial for implementing efficient, organized, and readable Java applications, especially when working with large datasets.