`Set` Interface
`Set` is part of the **Java Collections Framework**. It **doesn't allow duplicate elements**
```
Set<String> set = new HashSet<>();

set.add("A");         // Add element
set.remove("A");      // Remove element
set.contains("A");    // Check existence
set.size();           // Get number of elements
set.isEmpty();        // Check if set is empty
set.clear();          // Remove all elements
set.iterator();       // Get iterator for loop

```

## 2. Implementations Comparison

| Feature         | `HashSet`            | `LinkedHashSet`                | `TreeSet`                           |
| --------------- | -------------------- | ------------------------------ | ----------------------------------- |
| **Ordering**    | No ordering (random) | Maintains insertion order      | Sorted (natural or custom)          |
| **Duplicates**  | Not allowed          | Not allowed                    | Not allowed                         |
| **Nulls**       | 1 null allowed       | 1 null allowed                 | ❌ Null not allowed                  |
| **Performance** | Fast (O(1) ops)      | Slightly slower than `HashSet` | Slower (O(log n) ops)               |
| **Backed by**   | Hash Table           | Hash Table + Linked List       | Red-Black Tree (self-balancing BST) |
| **Use case**    | Best for search      | Ordered output required        | Sorted data needed                  |

## **HashSet**

Hash Table (buckets):
Index 0:  →  [null]
Index 1:  →  [Orange]
Index 2:  →  [null]
Index 3:  →  [Banana → Grape]
Index 4:  →  [null]

```
Set<Integer> hs = new HashSet<>();
hs.add(10); // stored using hashcode
hs.remove(10); // fast removal using hash lookup

```

No guaranteed order.
### **Internal Storage:**

- Internally uses a `HashMap` (each element is stored as a **key**, with a dummy value).
    
- Elements are placed in **buckets** based on their **hashCode()**.
    
- Each bucket is a list or a tree (after Java 8, if there are many collisions).
### On Removal:

- The item is removed from its **bucket**.
    
- No shifting occurs (no reordering).
    
- HashSet doesn’t maintain order, so shifting is irrelevant.
    

###  Performance:

- Add/Remove/Search: **O(1)** average case
---
## `LinkedHashSet` – **Hash Table + Linked List**

Hash Table:
Index 1:  →  [Orange]
Index 3:  →  [Banana]
Index 5:  →  [Apple]
**No**, it's **not fixed**. The storage **index values (1, 3, 5, etc.) are _not standard_ — they will change** depending on:
The element’s hash code
The hash table's capacity (array size)
Java's internal hashing and compression logic
Insertion Order Linked List:
null ← Orange ↔ Banana ↔ Apple → null


```
Set<String> lhs = new LinkedHashSet<>();
lhs.add("Apple");
lhs.add("Banana");
System.out.println(lhs); // Output: [Apple, Banana]

```

### **Internal Storage:**

- Uses `HashMap` like `HashSet`, but also keeps a **doubly linked list** of entries to maintain insertion order
### On Removal:

- The item is removed from the **hash table** (bucket) AND also from the **linked list**.
    
- Still **no shifting** like arrays — just updating `next` and `prev` pointers.
    

### Memory:

- More memory than `HashSet` because of linked list (extra pointers).
---
## `TreeSet` – **Backed by Red-Black Tree**
       5
     / \
    2   9


```
Set<Integer> ts = new TreeSet<>();
ts.add(5);
ts.add(2);
ts.add(9);
System.out.println(ts); // Output: [2, 5, 9] - Sorted

```

### **Internal Storage:**

- Uses a **self-balancing binary search tree** (Red-Black Tree).
    
- Sorted based on natural ordering or a custom comparator
---
### . **`HashSet` Methods**

`HashSet` is a collection that implements the `Set` interface. It does not maintain the order of elements.

- **`add(E e)`**: Adds an element to the set.
    
- **`remove(Object o)`**: Removes a specific element from the set.
    
- **`clear()`**: Removes all elements from the set.
    
- **`contains(Object o)`**: Checks if the set contains a specific element.
    
- **`size()`**: Returns the number of elements in the set.
    
- **`isEmpty()`**: Returns true if the set is empty.
    
- **`iterator()`**: Returns an iterator to iterate over the elements.
    
- **`toArray()`**: Returns an array containing all the elements of the set.
    
- **`retainAll(Collection<?> c)`**: Retains only the elements that are present in the specified collection.
    
- **`removeAll(Collection<?> c)`**: Removes all elements in the specified collection from the set.
    

### 2. **`LinkedHashSet` Methods**

`LinkedHashSet` is similar to `HashSet` but maintains the insertion order of elements.

- above hashtable methods will apply to this also.
    

### 3. **`TreeSet` Methods**

`TreeSet` is a NavigableSet implementation that is sorted according to the natural ordering of its elements or by a comparator provided at set creation.

- **`add(E e)`**: Adds an element to the set while maintaining the order.
    
- **`remove(Object o)`**: Removes a specific element from the set.
    
- **`clear()`**: Clears the set.
    
- **`contains(Object o)`**: Checks if the set contains a specific element.
    
- **`size()`**: Returns the number of elements in the set.
    
- **`isEmpty()`**: Returns true if the set is empty.
    
- **`first()`**: Returns the first (lowest) element.
    
- **`last()`**: Returns the last (highest) element.
    
- **`headSet(E toElement)`**: Returns all elements less than the specified element.
    
- **`tailSet(E fromElement)`**: Returns all elements greater than or equal to the specified element.
    
- **`ceiling(E e)`**: Returns the least element greater than or equal to the specified element.
    
- **`floor(E e)`**: Returns the greatest element less than or equal to the specified element.
    
- **`higher(E e)`**: Returns the least element strictly greater than the specified element.
    
- **`lower(E e)`**: Returns the greatest element strictly less than the specified element.
---
### **Map Interface – Behavior**

- Stores **key-value pairs**.
    
- **Keys are unique**; values can be duplicate.
    
- You can **add, update, remove**, and **search** using keys.

| Method Signature              | Description                                 |
| ----------------------------- | ------------------------------------------- |
| `put(K key, V value)`         | Adds or updates a key-value pair            |
| `get(Object key)`             | Returns value for the given key             |
| `remove(Object key)`          | Removes the entry with the given key        |
| `containsKey(Object key)`     | Checks if the map contains a specific key   |
| `containsValue(Object value)` | Checks if the map contains a specific value |
| `keySet()`                    | Returns a `Set` of all keys                 |
| `values()`                    | Returns a `Collection` of all values        |
| `entrySet()`                  | Returns a `Set<Map.Entry<K, V>>`            |
| `isEmpty()`                   | Returns `true` if map has no entries        |
| `size()`                      | Returns the number of key-value pairs       |
| `clear()`                     | Removes all entries from the map            |

```
Map<String, Integer> map = new HashMap<>();
map.put("apple", 10);
map.put("banana", 20);
map.put("cherry", 30);

```

   Map Reference (map) ─────────┐
                               ▼
       ┌─────────────┐
       │ HashMap Obj │
       └─────────────┘
             │
             ▼
       Buckets (based on hashCode)
     ┌─────────────────────────────────────────────┐
     │ Index 0   → null                            │
     │ Index 1   → Entry("banana", 20)             │
     │ Index 2   → null                            │
     │ Index 3   → Entry("apple", 10)              │
     │ Index 4   → Entry("cherry", 30)             │
     │ ...                                         │
     └─────────────────────────────────────────────┘
Memory View (internally stored as buckets in `HashMap`) not maintain order


### `LinkedHashMap` – Maintains Insertion Order

- ✅ Inherits from `HashMap`
- it fast and ordered
    
- ✅ Internally keeps a **doubly linked list** connecting all entries **in insertion order**
    
- ✅ Same bucket-based hash table as `HashMap`
"apple" ⇄ "banana" ⇄ "cherry"

Map Reference ─────────┐
                       ▼
       ┌─────────────────────┐
       │ LinkedHashMap Obj   │
       └─────────────────────┘
                │
                ▼
        Hash Buckets (like HashMap)
     ┌─────────────────────────────────────────────┐
     │ Index 1 → Entry("banana", 20, prev, next)   │
     │ Index 3 → Entry("apple", 10, prev, next)    │
     │ Index 4 → Entry("cherry", 30, prev, next)   │
     └─────────────────────────────────────────────┘
                       ↓
       Doubly Linked List (preserves order)
   **LinkedHashMap = HashMap + Doubly Linked List**

---
### `TreeMap` – Sorted Order (by Key)

- ✅ Does **not** use hash buckets
    
- ✅ Uses a **Red-Black Tree** (self-balancing binary search tree)
    
- ✅ Maintains **sorted order** of keys (natural order or comparator)


	          "banana" (20)
         /           \
   "apple"(10)     "cherry"(30)

- Insertions follow binary tree logic.
    
- Searching is **O(log n)** (better than linear in worst-case HashMap).
    
- **No buckets, no linked list** — pure tree structure.
- TreeMap doesn’t allow `null` keys because it needs to **compare** keys to sort them. You can’t compare `null` with a `String`.

```
TreeMap<Integer, String> map = new TreeMap<>((a, b) -> b - a); // Descending order

map.put(3, "Banana");
map.put(1, "Apple");
map.put(2, "Mango");

System.out.println(map); // Output: {3=Banana, 2=Mango, 1=Apple}

```

```
TreeMap<String, String> map = new TreeMap<>((a, b) -> b.compareTo(a));

map.put("banana", "yellow");
map.put("apple", "red");
map.put("cherry", "dark red");

System.out.println(map);

```



| Lambda Expression          | Resulting Order | Works With                                 |
| -------------------------- | --------------- | ------------------------------------------ |
| `(a, b) -> a - b`          | Ascending       | Primitives like `int` or wrapper `Integer` |
| `(a, b) -> b - a`          | Descending      | Same                                       |
| `(a, b) -> a.compareTo(b)` | Ascending       | Objects (`String`, `Integer`, etc.)        |
| `(a, b) -> b.compareTo(a)` | Descending      | Objects (`String`, etc.)                   |


---
## QUEUE

[Front] A ← B ← C ← D [Rear]

A **queue** is a linear data structure that follows the **First-In, First-Out (FIFO)** principle.Think of it like a line at a ticket counter: the person who arrives first is served first.
### Key Operations:

- **Enqueue**: Add an element to the end (rear) of the queue.
    
- **Dequeue**: Remove the element from the front (head) of the queue.
    
- **Peek**: View the element at the front without removing it.

| Method       | Description                                            | Removes and returns the head element       |
| ------------ | ------------------------------------------------------ | ------------------------------------------ |
| `add(E e)`   | Inserts element, throws on capacity issues             | will throw an exception if full            |
| `offer(E e)` | Inserts element, returns false on failure              | will just return `false` if full           |
| `remove()`   | Removes and returns head, throws if empty,             | Throws **NoSuchElementException** if empty |
| `poll()`     | Removes and returns head, returns null if empty,       | Returns `null` if the queue is empty       |
| `element()`  | Retrieves head without removing, throws if empty,      | same like remove                           |
| `peek()`     | Retrieves head without removing, returns null if empty | Returns `null` if the queue is empty       |

**only bounded queues like `ArrayBlockingQueue` show a difference** between `add()` and `offer()`.
```
import java.util.Queue;
import java.util.concurrent.ArrayBlockingQueue;

public class QueueExample {
    public static void main(String[] args) {
        // Bounded queue with capacity 2
        Queue<Integer> boundedQueue = new ArrayBlockingQueue<>(2);

        // Add 2 elements
        boundedQueue.add(1);
        boundedQueue.add(2);

        // Try to add a 3rd element using add() - this will throw an exception
        try {
            boundedQueue.add(3);  // ❌ This will throw IllegalStateException
        } catch (IllegalStateException e) {
            System.out.println("add() failed: " + e.getMessage());
        }

        // Try to add a 3rd element using offer() - this will return false
        boolean offerResult = boundedQueue.offer(3);  // ✅ Safe
        System.out.println("offer() result: " + offerResult);
    }
}

```

### Why `LinkedList` and `PriorityQueue` don't have fixed size?

- `LinkedList` and `PriorityQueue` grow dynamically — they are backed by structures that **expand as needed**, so there's no "full" state.
    
- So, whether you use `add()` or `offer()`, both will insert the element successfully, unless **memory runs out** (rare in normal use).
## `PriorityQueue` for Priority‑Based Ordering

The **`PriorityQueue<E>`** class implements `Queue<E>` using a **binary heap**, ordering elements by natural order or a supplied `Comparator` [Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html?utm_source=chatgpt.com). Its `poll()` and `offer()` operations run in **O(log n)** time due to heap adjustments, need to handle null otherwise will latter throw exception


```
import java.util.PriorityQueue;
import java.util.Queue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        Queue<Integer> pq = new PriorityQueue<>();

        pq.offer(30);  // O(log n)
        pq.offer(10);
        pq.offer(20);

        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // prints 10, then 20, then 30
        }
    }
}
	

```


You can supply a custom `Comparator` to change priority, e.g. descending order:

```
Queue<Integer> desc = new PriorityQueue<>((a, b) -> b - a);
desc.offer(5); desc.offer(1); desc.offer(3);
System.out.println(desc.poll()); // prints 5 (highest first)

```
## `LinkedList` as a FIFO Queue

> **LinkedList-specific methods will NOT be directly accessible** if you declare it as `Queue<Integer> queue = new LinkedList<>();`.Because you declared it as a **`Queue` reference**, the compiler only allows **methods defined in the `Queue` interface**, not the extra methods in `LinkedList`

The **`LinkedList<E>`** class implements both `List<E>` and `Deque<E>`, the latter extending `Queue<E>`, allowing it to be used directly as a **FIFO** queue [Oracle Docs](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html?utm_source=chatgpt.com)[Oracle Docs](https://docs.oracle.com/javase/tutorial/collections/implementations/queue.html?utm_source=chatgpt.com). Internally, it maintains a **doubly‑linked list**, so insertion at the tail (`offer`) and removal from the head (`poll`) both run in **O(1)** time


```
import java.util.LinkedList;
import java.util.Queue;

public class FifoLinkedListExample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();

        queue.offer("first");   // O(1): insert at tail
        queue.offer("second");
        queue.offer("third");

        System.out.println(queue.peek()); // "first" — inspect head without removal
        System.out.println(queue.poll()); // "first" — remove head
        System.out.println(queue.poll()); // "second"
        System.out.println(queue);       // [third] — remaining in insertion order
    }
}

```



Unlike `Stack` (LIFO), `LinkedList` preserves insertion order, making it ideal for tasks like breadth‑first search or request scheduling

---
### What Is a Utility Class?

A **utility class** in Java is a class that contains static methods and is not meant to be instantiated. These classes provide common functionalities that can be reused across different parts of an application. For example, the `java.util.Collections` class offers static methods to operate on or return collections.​

### Utility Classes for Different Collection Interfaces

#### 1. **`List` Interface**

- **Utility Class**: `java.util.Collections`​
    
- **Common Methods**:
    
    - `sort(List<T> list)`
        
    - `reverse(List<?> list)`
        
    - `shuffle(List<?> list)`
        
    - `binarySearch(List<? extends Comparable<? super T>> list, T key)`​
```
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
  Collections.sort(names);

```
#### 2. **`Set` Interface**

- **Utility Class**: `java.util.Collections`​
    
- **Common Methods**:
    
    - `unmodifiableSet(Set<? extends T> s)`
        
    - `synchronizedSet(Set<T> s)`
        
    - `singleton(T o)`​

```
  Set<String> set = new HashSet<>();
  Set<String> unmodifiableSet = Collections.unmodifiableSet(set);

```

#### 3. **`Map` Interface**

- **Utility Class**: `java.util.Collections`​
    
- **Common Methods**:
    
    - `unmodifiableMap(Map<? extends K, ? extends V> m)`
        
    - `synchronizedMap(Map<K, V> m)`
        
    - `singletonMap(K key, V value)`
```
  Map<String, Integer> map = new HashMap<>();
  Map<String, Integer> synchronizedMap = Collections.synchronizedMap(map);

```

#### 4. **`Queue` Interface**

- **Utility Class**: `java.util.Collections`​
    
- **Common Methods**:
    
    - `asLifoQueue(Deque<T> deque)`
        
    - `synchronizedCollection(Collection<T> c)`
```
  Deque<String> deque = new ArrayDeque<>();
  Queue<String> lifoQueue = Collections.asLifoQueue(deque);

```

## ITERATOR


`Iterator` is an **interface** defined in the `java.util` package. It provides methods to traverse a collection, such as `hasNext()`, `next()`, and `remove()`.\

```
import java.util.*;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        Iterator<String> iterator = names.iterator();//method call

        while (iterator.hasNext()) {
            String name = iterator.next();
            System.out.println(name);
        }
    }
}

```

- when you call `names.iterator()`, you're obtaining an **Iterator** to traverse the elements of the `names` list.|
  
- **`hasNext()`**: Checks if there are more elements to iterate over.​
    
- **`next()`**: Returns the next element in the iteration.

Simple analogy:
public String getName() {
    return "Alice";
}
you could call it like this
String name = obj.getName();

- `obj.getName()` calls the method.
    
- `String name = ...` stores the returned value in a variable.

Same exact idea with:

`Iterator<String> iterator = names.iterator();`