In Java, a **collection** is a framework that provides a standardized way to store, retrieve, and manipulate groups of objects. It is part of the Java Collections Framework found in the `java.util` package
**Definition and Purpose****
Group of Objects**:  
A collection is an object that groups multiple elements into a single unit. These elements are typically objects (not primitives), and collections make it easier to manage and process large amounts of data
### **Core Interfaces and Classes**
**The `Collection` Interface**:  
This is the root interface in the collections hierarchy. It declares the basic operations that all collections support, such as insertion, deletion, and iteration.
- **Subinterfaces of `Collection`**:
    
    - **`List`**: An ordered collection that allows duplicate elements (e.g., `ArrayList`, `LinkedList`).
        
    - **`Set`**: A collection that does not allow duplicate elements (e.g., `HashSet`, `TreeSet`).
        
    - **`Queue`**: Typically used to hold elements prior to processing (e.g., `LinkedList` when used as a queue, `PriorityQueue`).
        
- **Other Related Interfaces**:  
    Although **maps** (like `HashMap` and `TreeMap`) are part of the Collections Framework, they do not extend the `Collection` interface because they store key-value pairs rather than single elements.
    ### Example Without Using Generics
```
import java.util.ArrayList;
import java.util.List;

public class RawTypeExample {
    public static void main(String[] args) {
        // Create a raw type list (without generics)
        List rawList = new ArrayList();

        // Add elements to the list (different types can be added)
        rawList.add("Hello");
        rawList.add("World");
        rawList.add(100); // Accidentally adding an Integer

        // Iterate over the list and cast each element to String
        for (Object obj : rawList) {
            // This cast assumes every element is a String
            // At runtime, when the cast encounters an Integer, a ClassCastException will be thrown
            String str = (String) obj;
            System.out.println(str);
        }
    }
}
//for integer type
 int sum = 0;
        for (Object obj : rawList) {
            // We need to cast each element to Integer
            // When it reaches the string "30", a ClassCastException will be thrown at runtime.
            Integer number = (Integer) obj;
            sum += number;
        }
        System.out.println("Sum: " + sum);
    }
```
### What Difficulties Does This Code Illustrate?

1. **No Compile-Time Safety:**  
    The raw list (`List rawList = new ArrayList();`) allows you to add any type of object. The compiler won’t catch mistakes like adding an `Integer` when you expect only `String` objects.
    
2. **Risk of Runtime Errors:**  
    When iterating over the list, the code assumes all elements are of type `String`. The cast `(String) obj` will fail for any element that isn’t a `String` (e.g., the integer `100`), causing a `ClassCastException`.
    
3. **Extra Work with Casting:**  
    Every time you retrieve an element, you must explicitly cast it to the expected type, which makes the code more verbose and error-prone.
    ### Example With Generics


```
     //after add
     for (String str : stringList) {
            System.out.println(str);
        }
    
    int sum = 0;
        for (Integer number : intList) {
            sum += number;
        }
        System.out.println("Sum: " + sum); /
```

Java Collections Framework Hierarchy Diagram
                   +-----------------+
                   |    Iterable     |   <-- Root interface; supports for-each loops.
                   +-----------------+
                           |
                           v
                   +-----------------+
                   |   Collection    |   <-- Base interface for most collections.
                   +-----------------+
                           |
       +-------------------+---------------------+
       |                             |                     |
      v                   v                     v
   +---------+        +-----------+        +-------------+
   |  List    |                |   Set       |           |     Queue     |
   +---------+        +-----------+        +-------------+
       |                   |                     |
       |                   |                     +----------------------+
       |                   |                     |                                  |
       v                   v                     v                      v
+--------------+   +----------------+   +----------------+      +----------------+
| ArrayList    |      | HashSet              |      | PriorityQueue|      | Deque               |
| LinkedList   |    | LinkedHashSet    |   +----------------+      +----------------+
| Vector       |      | TreeSet                |                                     | (e.g., ArrayDeque)
| Stack        |       |                             |                                                  |
+--------------+   +----------------+                                                  |
                                                    |
                                                    v
                                             +--------------+
                                               |  LinkedList  |
                                            +--------------+

         (Note: Some classes appear in multiple roles; for example, LinkedList implements both List and Deque.)

                   +-------------------+
                   |       Map       |   <-- Not a subtype of Collection; stores key-value pairs.
                   +-------------------+
                           |
         +-----------------+-----------------+
         |                                   |
         v                                   v
   +---------------+                                            +-------------------+
   | SortedMap     |                                              |  HashMap,           |
   | (NavigableMap)|                                           |  LinkedHashMap |
   +---------------+                                            +-------------------+
           |
           v
       +---------+
       | TreeMap |
       +---------+


## Explanation of Major Components

### 1. **Iterable Interface**

- **Role:**  
    The root interface that represents a collection of elements which can be iterated over.
    
- **Key Method:**  
    `iterator()`—returns an `Iterator` over elements.
    
### 2. **Collection Interface**

- **Role:**  
    The primary interface that represents a group of objects (known as elements). Most other collection interfaces (except `Map`) extend this interface.
    
- **Key Operations:**  
	    Methods like `add()`, `remove()`, `contains()`, `size()`, and `clear()`.
    

### 3. **List Interface**

- **Role:**  
    An ordered collection (also known as a sequence) that can contain duplicate elements.
    
- **Implementations:**
    
    - **ArrayList:** A resizable array implementation.
        
    - **LinkedList:** A doubly-linked list implementation (also implements `Deque` for queue operations).
        
    - **Vector:** A synchronized resizable array (legacy, less commonly used now).
        
    - **Stack:** A subclass of `Vector` that implements a last-in, first-out (LIFO) stack.
        
- **Key Features:**  
    Positional access (using an index), ordered iteration.
    

### 4. **Set Interface**

- **Role:**  
    A collection that cannot contain duplicate elements.
    
- **Subinterfaces:**
    
    - **SortedSet:** Maintains its elements in ascending order.
        
    - **NavigableSet:** Extends `SortedSet` with navigation methods (e.g., `lower()`, `floor()`, `ceiling()`, `higher()`).
        
- **Implementations:**
    
    - **HashSet:** Backed by a hash table; offers constant-time performance.
        
    - **LinkedHashSet:** Maintains insertion order using a linked list.
        
    - **TreeSet:** Implements `NavigableSet`, maintains a sorted order (uses a tree structure).
        

### 5. **Queue Interface**

- **Role:**  
    Designed for holding elements prior to processing (typically in a FIFO—first-in, first-out—manner).
    
- **Subinterfaces/Implementations:**
    
    - **PriorityQueue:** Orders its elements according to their natural ordering or by a provided comparator.
        
    - **Deque (Double-Ended Queue):** Supports element insertion and removal at both ends (e.g., `ArrayDeque`, `LinkedList` when used as a deque).
        

### 6. **Iterator and ListIterator**

- **Iterator:**  
    Provides methods to iterate over elements in a collection, such as `hasNext()`, `next()`, and `remove()`.
    
- **ListIterator:**  
    An extension of `Iterator` for lists, allowing bidirectional traversal and modification of the list during iteration.
    

### 7. **Map Interface**

- **Role:**  
    Represents a collection that maps keys to values; keys are unique.
    
- **Note:**  
    `Map` does not extend the `Collection` interface because it handles pairs of objects (key and value) rather than individual elements.
    
- **Subinterfaces:**
    
    - **SortedMap:** Maintains its keys in ascending order.
        
    - **NavigableMap:** Extends `SortedMap` with navigation methods.
        
- **Implementations:**
    
    - **HashMap:** Provides constant-time performance for basic operations.
        
    - **LinkedHashMap:** Maintains insertion order.
        
    - **TreeMap:** Implements `NavigableMap` and sorts its keys.
- simple example that shows how to implement the `Iterable` interface. This example creates a custom generic class `MyCollection` that holds an array of elements. The class implements the `Iterable` interface by providing an implementation of the `iterator()` method that returns an `Iterator` over its elements.
```
import java.util.Iterator;

public class MyCollection<T> implements Iterable<T> {
    // Array to store elements
    private T[] items;
    // Number of elements in the collection
    private int size;

    // Constructor accepting an array of items
    public MyCollection(T[] items) {
        this.items = items;
        this.size = items.length;
    }

    // Implementation of the iterator() method from the Iterable interface
    @Override
    public Iterator<T> iterator() {
        return new MyIterator();
    }

    // Private inner class that implements the Iterator interface
    private class MyIterator implements Iterator<T> {
        private int index = 0; // Current index for iteration

        // Returns true if there are more elements to iterate over
        @Override
        public boolean hasNext() {
            return index < size;
        }

        // Returns the next element in the collection
        @Override
        public T next() {
            return items[index++];
        }

        // Optional remove() operation is not supported in this example
        @Override
        public void remove() {
            throw new UnsupportedOperationException("Remove not supported.");
        }
    }

    // Main method to demonstrate iteration using the enhanced for-loop (for-each)
    public static void main(String[] args) {
        // Creating an array of Integer values
        Integer[] numbers = {1, 2, 3, 4, 5};
        // Creating an instance of MyCollection with the Integer array
        MyCollection<Integer> collection = new MyCollection<>(numbers);

        // Using the enhanced for-loop to iterate over the collection
        for (Integer number : collection) {
            System.out.println(number);
        }
    }
}

```

The `Collection` interface defines general-purpose methods such as `add()`, `remove()`, `contains()`, `size()`, and `clear()`, which are common to all collections. However, different types of collections have unique characteristics and behaviors that necessitate additional methods:
### **Collection**

- **Role**: The root interface of the collection hierarchy. It represents a group of objects, known as elements.
    
- **Key Methods**:
    
    - `add(E e)` – Adds an element to the collection.
        
    - `remove(Object o)` – Removes a single instance of the specified element.
        
    - `contains(Object o)` – Returns `true` if the collection contains the specified element.
        
    - `size()` – Returns the number of elements in the collection.
        
    - `clear()` – Removes all elements from the collection
## Java `List` Interface and Its Implementations

The `List` interface represents an ordered collection that can contain duplicate elements. It provides positional access and insertion of elements.​

. Methods Specific to the List Interface

| Method                  | Purpose                              |
| ----------------------- | ------------------------------------ |
| `add(int index, E e)`   | Add element at a specific index      |
| `get(int index)`        | Retrieve element at a specific index |
| `set(int index, E e)`   | Replace element at a specific index  |
| `remove(int index)`     | Remove element at a specific index   |
| `indexOf(Object o)`     | Get first index of the element       |
| `lastIndexOf(Object o)` | Get last index of the element        |
| `subList(from, to)`     | Get a portion (sub-list) of the list |

### 1. **ArrayList**

Special Methods(`ArrayList` only)

| Method                | Purpose                     |
| --------------------- | --------------------------- |
| `ensureCapacity(int)` | Manually increases capacity |
| `trimToSize()`        | Shrinks internal array      |



- **Structure**: Backed by a dynamic array (`Object[]`).
    
- **Insertion**:
    
    - Appending at the end is fast (amortized constant time).
        
    - Inserting at a specific index requires shifting subsequent elements.
        
- **Use Case**: When frequent random access and minimal insertions/deletions in the middle are needed.​
    

**Diagram**:

`[0] [1] [2] [3] [4]
		   A    B      C      D     E  `

**Code Example**:

```
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A"); // Appends at index 0
        list.add("B"); // Appends at index 1
        list.add(1, "C"); // Inserts at index 1, shifts "B" to index 2
        System.out.println(list); // Output: [A, C, B]
    }
}

```



---

### 2. **LinkedList**

`LinkedList` only (from Deque):

| Method                           | Purpose                |
| -------------------------------- | ---------------------- |
| `addFirst(e)` / `addLast(e)`     | Add to front/back      |
| `getFirst()` / `getLast()`       | Get front/back         |
| `removeFirst()` / `removeLast()` | Remove front/back      |
| `push(e)` / `pop()`              | Stack-style operations |

- **Structure**: Doubly-linked list; each node contains data and references to previous and next nodes.
    
- **Insertion**:
    
    - Efficient insertions and deletions at both ends.
        
    - Inserting in the middle requires traversal to the desired position.
        
- **Use Case**: When frequent insertions and deletions are needed, especially at the beginning or end.​
    

**Diagram**:

`null <- [A] <-> [B] <-> [C] -> null`

**Code Example**:
```
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("A"); // Adds at the end
        list.addFirst("B"); // Adds at the beginning
        list.addLast("C"); // Adds at the end
        System.out.println(list); // Output: [B, A, C]
    }
}

```



---

### 3. **Vector**

`Vector` only:

| Method             | Purpose                |
| ------------------ | ---------------------- |
| `addElement(e)`    | Add to end (old style) |
| `removeElement(e)` | Remove by value        |
| `capacity()`       | Current array capacity |
| `elements()`       | Returns Enumeration    |

- **Structure**: Similar to `ArrayList` but synchronized.not recommended for new project
    
- **Insertion**:
    
    - Thread-safe operations.
        
    - Appending at the end is efficient; inserting elsewhere requires shifting elements.
        
- **Use Case**: When thread-safe operations are required without external synchronization.​
    

**Diagram**:

`[0] [1] [2] 
  X       Y     Z`

**Code Example**:

```
import java.util.Vector;

public class VectorExample {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("X"); // Appends at index 0
        vector.add("Y"); // Appends at index 1
        vector.insertElementAt("Z", 1); // Inserts at index 1, shifts "Y" to index 2
        System.out.println(vector); // Output: [X, Z, Y]
    }
}

```

- **Flexibility and Abstraction**:
    
    - Declaring the variable as `List<String>` promotes programming to an interface, allowing you to switch between different `List` implementations (like `LinkedList`, `Vector`, etc.) without changing the variable's type.
        
    - Declaring it as `ArrayList<String>` ties your code to a specific implementation, reducing flexibility.​
**Access to Implementation-Specific Methods**:

- With `List<String> list`, you can only access methods defined in the `List` interface.
    
- With `ArrayList<String> list`, you can access all methods specific to `ArrayList`, such as `trimToSize()` and `ensureCapacity()`.


STACK ONLY:

| Method             | Purpose                                   |
| ------------------ | ----------------------------------------- |
| `push(e)`          | Add to top                                |
| `pop()`            | Remove from top                           |
| `peek()`           | Look at top                               |
| `empty()`          | Checks if stack is empty                  |
| `search(Object o)` | Returns position from top (1-based index) |

## STACK:

Stack<String> stack = new Stack<>();

stack.push("A");
stack.push("B");
stack.push("C");
The insertion order is:

"A" → inserted first → bottom

"B" → inserted second → middle

"C" → inserted last → top

 So the **Insertion Order** is:

`A → B → C`

But since Stack is **LIFO**, if you start popping:

📦 Stack content (internally stored like a list):

Bottom → [A, B, C] ← Top







