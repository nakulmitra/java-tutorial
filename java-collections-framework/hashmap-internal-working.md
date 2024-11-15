# Understanding the Internal Working of HashMap in Java
Java’s `HashMap` is a highly efficient data structure used for storing key-value pairs. It is part of Java’s `java.util` package and is widely used in scenarios requiring fast data access. This document will walk through `HashMap`'s internal architecture, hashing mechanisms, collision handling, resizing, and retrieval process.

[![](https://markdown-videos-api.jorgenkh.no/youtube/PZcgsPyYAgM)](https://youtu.be/PZcgsPyYAgM)

## Overview
In Java, a `HashMap` stores data in key-value pairs. Each key is unique, and it maps to a specific value. Here’s how `HashMap` works at a high level:
* `Hashing:` Each key has a unique hash code that determines where it should be stored in memory.
* `Buckets:` HashMap uses an array-based data structure where each position in the array, known as a bucket, can store multiple entries.
* `Collisions:` When multiple keys map to the same bucket, `HashMap` handles them using chaining (with linked lists) or trees.
* `Resizing:` As entries are added, the HashMap may resize itself to maintain performance.

## Internal Structure of HashMap
## Hashing and Bucket Index Calculation
When a key-value pair is added to a `HashMap`, the following steps occur:
* The key’s `hashCode()` method generates an integer value called a **hash code**.
* This hash code is used to determine the bucket index where the key-value pair will be stored within the internal array of the `HashMap`.

### Code Example: Generating a Hash Code
```
String key = "apple";
int hashCode = key.hashCode();
System.out.println("Hash code for 'apple': " + hashCode);
```

## Bucket Index Calculation
The bucket index is calculated by applying a **bitwise AND** operation to the hash code with the expression `(n - 1)`, where `n` is the current capacity of the `HashMap`. This ensures the index is within the array bounds.
```
int index = hashCode & (capacity - 1); // Example capacity = 16
```

#### Example Calculation
Let’s assume:
* HashMap capacity = 16
* Key’s hash code = 93029210
```
int index = hashCode & (capacity - 1);
System.out.println("Bucket index for key 'apple': " + index);
```

This will generate an index value within the range `[0, 15]`, directing the entry to its appropriate bucket.

## Structure of Buckets and Storage of Entries
Each bucket in `HashMap` holds multiple entries (key-value pairs) using a **linked list** or a **balanced tree** structure.
### Example: Adding Entries to a HashMap
```
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 100);
map.put("banana", 200);
map.put("grape", 300);
```

In this example:
* Assume `"apple"` and `"banana"` both hash to bucket index `6`.
* `"grape"` hashes to bucket index 2.

The resulting structure:
* Bucket[2] -> `("grape", 300)`
* Bucket[6] -> `("apple", 100)` -> `("banana", 200)` (stored in a linked list or tree if needed)

## Collision Handling
Collisions occur when multiple keys hash to the same bucket. `HashMap` uses **Separate Chaining** to handle these collisions.

### Separate Chaining Mechanism
* `Java 7 and Earlier:` Collisions were handled using a simple linked list.
* `Java 8 and Later:` Java optimizes performance by converting the linked list to a **balanced tree** (Red-Black Tree) if a bucket has more than 8 entries.
The tree structure reduces the time complexity of searching within a bucket from **O(n)** to **O(log n)**.

## Retrieving Values from HashMap
The retrieval process is as follows:
* The key’s `hashCode()` is calculated.
* The hash code undergoes the same bitwise operation to find the bucket index.
* If there are multiple entries (due to a collision), the entries are searched one-by-one, or if a tree structure is used, a binary search is performed.

### Example: Retrieving a Value
```
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 100);
int value = map.get("apple"); // Returns 100
```

## HashMap Resizing and Rehashing
The `HashMap` dynamically resizes itself when it reaches a certain threshold. The load factor (default 0.75) determines when resizing occurs. For instance, with an initial capacity of 16, resizing will occur after 12 entries.

### Resizing Process
* `HashMap` doubles its capacity.
* All entries are **rehased** and redistributed into new buckets.

This process ensures performance remains optimal as the number of entries grows.

## Summary: Internal Working of HashMap
| Step | Description |
| ----------------|-------|
|    Hash Code Generation     |  The `hashCode()` method generates a unique integer for each key.  |
|    Index Calculation     |  The hash code is processed to fit within the `HashMap`'s bucket array.  |
|    Entry Storage   |  Each entry is stored in a bucket, possibly with other entries if collisions occur.  |
|    Collision Handling      |  Separate chaining with linked lists or trees (in Java 8+) manages collisions within the same bucket.  |
|    Resizing      |  The HashMap resizes and rehashes all entries when the load factor threshold is exceeded.  |

## Practical Scenarios for Using HashMap
* `Caching and Lookup Tables:` `HashMap` provides O(1) average-time complexity for retrieving cached data.
* `Configuration Properties:` Store application configurations where each setting has a unique key.
* `Counting Frequency:` Track occurrences of elements efficiently.

## Conclusion
Java’s `HashMap` is optimized for efficient data retrieval, and its internal structure supports fast access, collision handling, and resizing. Understanding these mechanisms equips you to use `HashMap` effectively and avoid performance pitfalls in large applications.

[< Previous Tutorial](https://github.com/nakulmitra/java-tutorial/blob/master/java-collections-framework/maps.md) | [Next Tutorial >](https://github.com/nakulmitra/java-tutorial/blob/master/java-collections-framework/iterator-foreach.md)