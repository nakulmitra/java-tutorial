# Java Set Interface: HashSet, LinkedHashSet, and TreeSet
The Set interface in Java is part of the Java Collections Framework and is used to store unique elements. The main implementations of the Set interface are **HashSet**, **LinkedHashSet**, and **TreeSet**. Each implementation has unique features that make them suitable for different use cases. This guide provides a deep dive into these Set types, including their characteristics, use cases, and code examples.

[![](https://markdown-videos-api.jorgenkh.no/youtube/RSN-kkjmBvc)](https://youtu.be/RSN-kkjmBvc)

## What is a Set?
In Java, a Set is a collection that:
* Does not allow duplicate elements
* Does not guarantee the order of elements (though LinkedHashSet and TreeSet provide ordering in specific ways)

Sets are useful in scenarios where we need to ensure that each element in a collection is unique. Common Set operations include adding, removing, and checking the existence of elements.

## Characteristics of Sets in Java
Here are some key characteristics of Sets:
* `Uniqueness:` Sets don’t allow duplicates. If we try to add an element that already exists, it will be ignored.
* `Unordered:` Sets generally don’t maintain any specific order of elements, but LinkedHashSet preserves insertion order, and TreeSet sorts elements in natural order or based on a comparator.
* `Efficient Search:` Sets offer efficient methods for checking the presence of an element, with O(1) complexity for HashSet.

## Set Implementations in Java
Java offers three main implementations of the Set interface:

### HashSet
**HashSet** is a commonly used implementation of the Set interface backed by a **hash table**. HashSet provides **constant time performance (O(1))** for basic operations, like add, remove, and contains, assuming hash functions distribute elements properly across the table.

#### Key Characteristics
* `No guaranteed order:` Elements are stored in no specific order.
* `Allows null:` HashSet permits one null element.
* `Fast lookups:` Offers quick lookups due to hash-based storage.

#### Common Methods in HashSet
* `add(element):` Adds an element to the HashSet.
* `remove(element):` Removes the specified element.
* `contains(element):` Checks if an element exists.
* `isEmpty():` Returns true if the set is empty.
* `size():` Returns the number of elements in the set.

#### Example
```
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<Integer> numbers = new HashSet<>();
        
        numbers.add(1);
        numbers.add(2);
        numbers.add(1);  // Duplicate, will not be added

        System.out.println("HashSet: " + numbers);  // Output: [1, 2]
        System.out.println("Contains 1? " + numbers.contains(1));  // Output: true

        numbers.remove(1);
        System.out.println("After removal: " + numbers);  // Output: [2]
    }
}
```

### LinkedHashSet
**LinkedHashSet** is a variant of HashSet that maintains a **doubly-linked list** of elements, preserving insertion order.

#### Key Characteristics
* `Maintains insertion order:` Elements are returned in the order they were added.
* `Performance slightly slower than HashSet:` Due to maintaining a linked list of entries.
* `Allows null:` Like HashSet, it permits one null element.

#### Example
```
import java.util.LinkedHashSet;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        LinkedHashSet<String> cities = new LinkedHashSet<>();
        
        cities.add("New York");
        cities.add("Los Angeles");
        cities.add("New York");  // Duplicate, will not be added

        System.out.println("LinkedHashSet: " + cities);  // Output: [New York, Los Angeles]
    }
}
```

### TreeSet
**TreeSet** is a Set implementation that uses a **Red-Black Tree** to store elements, automatically sorting them in **ascending order**.

#### Key Characteristics
* `Sorted order:` TreeSet sorts elements based on their natural order or by a provided comparator.
* `Does not allow null:` TreeSet does not support null elements.
* `Performance:` Basic operations like add, remove, and contains have a time complexity of O(log n) due to tree traversal.

#### Example
```
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        TreeSet<Integer> numbers = new TreeSet<>();
        
        numbers.add(5);
        numbers.add(1);
        numbers.add(3);

        System.out.println("TreeSet (Sorted): " + numbers);  // Output: [1, 3, 5]
    }
}
```

### Set Operations in Java
**Sets** are commonly used in mathematical operations such as **union**, **intersection**, and **difference**. Here’s how to implement these with Sets:

#### Union
Combines elements from both sets without duplicates.
```
HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3));
HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5));

set1.addAll(set2);
System.out.println("Union: " + set1);  // Output: [1, 2, 3, 4, 5]
```

#### Intersection
Finds common elements between both sets.
```
HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3));
HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5));

set1.retainAll(set2);
System.out.println("Intersection: " + set1);  // Output: [3]
```

#### Difference
Finds elements in the first set but not in the second.
```
HashSet<Integer> set1 = new HashSet<>(Arrays.asList(1, 2, 3));
HashSet<Integer> set2 = new HashSet<>(Arrays.asList(3, 4, 5));

set1.removeAll(set2);
System.out.println("Difference: " + set1);  // Output: [1, 2]
```

## Choosing the Right Set Implementation
* `HashSet:` Ideal for scenarios where we don’t care about the order of elements and need fast lookups, insertions, and deletions.
* `LinkedHashSet:` Use this when we need to maintain insertion order but also need fast operations.
* `TreeSet:` Choose TreeSet when we need elements to be automatically sorted, such as maintaining a leaderboard or a sorted set of names.

## Conclusion
By understanding how each Set type works and where to apply them, we’ll be able to write more efficient, organized, and maintainable Java code. This knowledge will also help us in scenarios where maintaining unique elements and performing mathematical operations are critical, such as data processing, sorting, and managing collections of unique records.