
### LAMBDA

A **lambda expression** is a short block of code that takes in parameters and returns a value.  
It’s used to **implement a functional interface** (one abstract method) in a cleaner, simpler way.
- **Lambda** is just a nickname or shorthand.
    
- The full term is **"lambda expression"**, which is the actual **syntax and feature** introduced in Java 8.

- **"Lambda"** = the concept or shorthand
    
- **"Lambda Expression"** = the actual code syntax used to write it
syntax
```
	(parameters) -> { body }
```

##### **What** **is a Functional Interface**?
A **Functional Interface** in Java is an interface that has **only one abstract method**.  
Java 8 introduced this concept to enable **Lambda Expressions**.
must implement by using lambda or anonymous class
**`Runnable` is a functional interface** in Java!
###  Why is it called “Functional”?

Because it represents a **single functionality** (or behavior) that can be implemented using a **lambda expression**.

```
@FunctionalInterface
interface Greet {
    void sayHello();
}

public class Demo {
    public static void main(String[] args) {
        Greet g = () -> System.out.println("Hello from Lambda!");
        g.sayHello();
    }
}

```

with parameter
```
@FunctionalInterface
interface Add {
    int sum(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        Add adder = (a, b) -> a + b;
        System.out.println(adder.sum(5, 10));  // Output: 15
    }
}

```


##  **Anonymous Inner Class**

An **anonymous inner class** is a class **without a name** that is defined and used in a **single line** (especially to implement interfaces or abstract classes).

```
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Running task");
    }
};
r.run();

```
### **Inner Class (Basic Concept)**

An **inner class** is a class defined **inside another class**.

```
class Outer {
    class Inner {
        void show() {
            System.out.println("Hello from Inner Class");
        }
    }
}
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
inner.show();


```

**STATIC CLASS**
```
package Lambda;

import java.util.function.*;

public class FunctionalInterfaceDemo {

    public static class outer {
        public static class inner {
            public void demo() {
                System.out.println("hii");
            }
        }
    }

    public static void main(String[] args) {
        FunctionalInterfaceDemo.outer.inner obj = new FunctionalInterfaceDemo.outer.inner();
        obj.demo();
    }
}

```

**Non-static Inner Class**

```
public class FunctionalInterfaceDemo {

    public class outer {
        public class inner {
            public void demo() {
                System.out.println("hii");
            }
        }
    }

    public static void main(String[] args) {
        FunctionalInterfaceDemo outerDemo = new FunctionalInterfaceDemo();
        outer out = outerDemo.new outer();
        outer.inner inn = out.new inner();

        inn.demo();
    }
}

```

**Local Inner Class (Defined Inside a Method)**
```
public class Outer {
    void display() {
        class LocalInner {
            void msg() {
                System.out.println("Local inner class in method");
            }
        }

        LocalInner local = new LocalInner();
        local.msg();
    }

    public static void main(String[] args) {
        new Outer().display();
    }
}

```

## **Static Inner Class (Access without Outer Object)**

```
class Outer {
    static int x = 50;

    static class Inner {
        void show() {
            System.out.println("Outer static x = " + x);
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Outer.Inner inner = new Outer.Inner();  // 👈 no need for outer object
        inner.show(); // Output: Outer static x = 50
    }
}

```

**Using Static Nested Classes (Simpler Syntax)**

```
package Lambda;

public class FunctionalInterfaceDemo {

    static class Outer {
        static class Inner {
            public void demo() {
                System.out.println("hii from static inner class");
            }
        }
    }

    public static void main(String[] args) {
        Outer.Inner inn = new Outer.Inner(); // no need for outer object
        inn.demo();
    }
}

```
**OTHER WAYS NON STATIC** 

```
package Lambda;

public class FunctionalInterfaceDemo {

    class outer {
        public class inner {
            public void demo() {
                System.out.println("hii");
            }
        }
    }

    public static void main(String[] args) {
        FunctionalInterfaceDemo outerClass = new FunctionalInterfaceDemo();     // Step 1
        outer out = outerClass.new outer();                                     // Step 2
        outer.inner inn = out.new inner();                                      // Step 3
        inn.demo();  // Output: hii
    }
}

```

**1.PROBLEM QUESTION USING INNER CLASS**
```
public class College {

    // Outer class variable
    private String collegeName = "ABC College";

    // Outer class method
    public void displayCollegeInfo() {
        System.out.println("College Name: " + collegeName);
    }

    // Inner class
    class Student {
        private String studentName;

        // Constructor
        public Student(String name) {
            this.studentName = name;
        }

        // Inner class method
        public void displayStudentInfo() {
            // Accessing outer class variable
            System.out.println("Student Name: " + studentName);
            System.out.println("Belongs to: " + collegeName); // Access outer variable directly
        }

        // Getter to show how outer can access inner data
        public String getStudentName() {
            return studentName;
        }
    }

    // Method to show how outer class accesses inner class
    public void accessStudentInfo() {
        Student s = new Student("John");
        System.out.println("Accessing student from outer: " + s.getStudentName());
    }

    // Main method
    public static void main(String[] args) {
        // Step 1: Create outer class object
        College college = new College();

        // Step 2: Display college info
        college.displayCollegeInfo();

        // Step 3: Create inner class object (using outer object)
        College.Student student = college.new Student("Alice");

        // Step 4: Display student info
        student.displayStudentInfo();

        // Step 5: Outer class accessing inner class variable
        college.accessStudentInfo();
    }
}

```
---
### Built-in Functional Interfaces 
(from `java.util.function)

```
import java.util.function.Consumer;
import java.util.function.Supplier;
import java.util.function.Function;
import java.util.function.BiFunction;
import java.util.function.Predicate;

public class FunctionalInterfaceDemo {

    public static void main(String[] args) {

        // 1. Consumer<T>: Takes input and returns nothing
        
        Consumer<String> consumer = msg -> System.out.println("Consumer received: " + msg);
        consumer.accept("Hello from Consumer!");

        // 2. Supplier<T>: Takes nothing and returns something
        
        Supplier<String> supplier = () -> "Hello from Supplier!";
        System.out.println("Supplier provided: " + supplier.get());

        // 3. Function<T, R>: Takes input and returns something
        
        Function<String, Integer> function = str -> str.length();
        
        System.out.println("Function result (length): " + function.apply("Lambda"));

        // 4. BiFunction<T, U, R>: Takes 2 inputs and returns something
        
        BiFunction<Integer, Integer, Integer> biFunction = (a, b) -> a + b;
        System.out.println("BiFunction result (sum): " + biFunction.apply(5, 15));

        // 5. Predicate<T>: Takes input and returns boolean
        
        Predicate<String> predicate = str -> str.startsWith("L");
        System.out.println("Predicate result (starts with 'L'): " + predicate.test("Lambda"));
    }
}

```

CONSUMER:
- There’s only **one parameter**
    
- The parameter type is **inferred**
    
- No parentheses are **needed**

---

### **TASK:**
### **Banking App Task Breakdown**:

#### 1. **Create Account** (using `Supplier`)

- Use the `Supplier` interface to generate random bank account details (like account number or OTP).
    

#### 2. **Validate Account Balance** (using `Predicate`)

- Use the `Predicate` interface to check if the account balance is sufficient to perform a transaction.
    

#### 3. **Transaction Processing** (using `BiFunction`)

- Use the `BiFunction` interface to process a transaction, which will take two inputs (sender account and recipient account) and return a transaction receipt.
    

#### 4. **Log Account Activity** (using `Consumer`)

- Use the `Consumer` interface to log activity whenever an action is performed (e.g., withdrawal, deposit, transfer).
    

#### 5. **Convert Transaction Details to Receipt** (using `Function`)

- Use the `Function` interface to convert transaction details (input) into a receipt (output).

```
import java.util.*;
import java.util.function.*;

public class BankingApp {

    // Bank account class to hold account details
    static class Account {
        String accountNumber;
        double balance;

        Account(String accountNumber, double balance) {
            this.accountNumber = accountNumber;
            this.balance = balance;
        }
    }

    // 1. Supplier to generate a random account number
    static Supplier<String> generateAccountNumber = () -> "ACC" + new Random().nextInt(1000);

    // 2. Predicate to validate if the account has sufficient funds
    static Predicate<Account> hasSufficientFunds = account -> account.balance > 0;

    // 3. BiFunction to process a transaction and generate a receipt
    static BiFunction<Account, Account, String> processTransaction = (sender, receiver) -> {
        if (sender.balance > 0) {
            sender.balance -= 100;  // Deduct 100 from sender
            receiver.balance += 100;  // Add 100 to receiver
            return "Transaction successful! Sent 100 from " + sender.accountNumber + " to " + receiver.accountNumber;
        } else {
            return "Transaction failed: Insufficient funds";
        }
    };

    // 4. Consumer to log account activities
    static Consumer<String> logActivity = activity -> System.out.println("Log: " + activity);

    // 5. Function to convert transaction details to a receipt
    static Function<String, String> createReceipt = transactionDetails -> 
        "Receipt: " + transactionDetails + " - " + new Date().toString();

    public static void main(String[] args) {

        // Creating accounts
        Account sender = new Account(generateAccountNumber.get(), 500);
        Account receiver = new Account(generateAccountNumber.get(), 200);

        // 1. Generating Account Numbers using Supplier
        System.out.println("Sender Account: " + sender.accountNumber);
        System.out.println("Receiver Account: " + receiver.accountNumber);

        // 2. Checking account balance before transaction using Predicate
        System.out.println("Sender has sufficient funds: " + hasSufficientFunds.test(sender));

        // 3. Processing Transaction using BiFunction
        String transactionDetails = processTransaction.apply(sender, receiver);
        System.out.println(transactionDetails);

        // 4. Logging the transaction using Consumer
        logActivity.accept(transactionDetails);

        // 5. Creating a Receipt using Function
        String receipt = createReceipt.apply(transactionDetails);
        System.out.println(receipt);
    }
}

```

### **Explanation of Each Functional Interface Use**:

1. **Supplier** (`generateAccountNumber`):
    
    - Generates a random account number when creating a new account.
        
2. **Predicate** (`hasSufficientFunds`):
    
    - Checks if the sender account has enough balance to perform the transaction.
        
3. **BiFunction** (`processTransaction`):
    
    - Takes two accounts (sender and receiver) and processes a transaction, transferring 100 units from the sender to the receiver.
        
4. **Consumer** (`logActivity`):
    
    - Logs the transaction details after processing.
        
5. **Function** (`createReceipt`):
    
    - Converts the transaction details into a receipt format that includes a timestamp.
---
## STREAM API:

What is Java Stream API?
The **Stream API** (introduced in Java 8) is used to **process collections of data** (like `List`, `Set`, etc.) in a **functional style**. It allows for **declarative**, **clean**, and **efficient** operations on data.
## Why use Stream API?

- To perform **complex data operations** (filtering, mapping, reducing, etc.) in a **concise** and **readable** way.
    
- To **chain multiple operations** together.
    
- To support **parallel processing** easily.

---

### 🔷 Java Stream Pipeline Diagram

+--------+      +-------------------+        +------------------+        +--------------------+
| Source | --> | Intermediate Op 1 | --> | Intermediate Op2 | --> | Terminal Operation |
+--------+      +-------------------+        +------------------+        +--------------------+
    |                      |                                       |                                                      |
    v                     v                                      v                                                     v
[List, Set,      filter(), map(),           sorted(), distinct()                      collect(), 
 array, etc.]     limit(), skip(), etc.                                                    forEach(),count()


```
List<String> names = List.of("John", "Alice", "Bob");

List<String> result = names.stream()                     // Source
    .filter(name -> name.startsWith("A"))                // Intermediate
    .map(String::toUpperCase)                            // Intermediate
    .collect(Collectors.toList());                       // Terminal

System.out.println(result); // Output: [ALICE]

```

## Types of Streams

- **Sequential Stream** – processed in a single thread.
    
- **Parallel Stream** – processed in multiple threads (use `.parallelStream()`).
- This comes under **Stream execution behavior**, not the methods (`map()`, `collect()`, etc.) themselves.
### 1. **Sequential Stream** (Default)

- This is what you’ve been using in all examples so far.
    
- **Processed in a single thread**, one element at a time, in the order of the stream.
    
```
List<String> names = List.of("Alice", "Bob", "Charlie");

names.stream()  // default: sequential
    .map(name -> name.toUpperCase())
    .forEach(System.out::println);

```
### 2. **Parallel Stream**

- Executes operations **in parallel using multiple threads**.
    
- Can improve performance for **large data sets** and CPU-heavy operations.
    
- You use `.parallelStream()` or `.stream().parallel()`.
    
```
names.parallelStream()
    .map(name -> {
        System.out.println(Thread.currentThread().getName() + " - " + name);
        return name.toUpperCase();
    })
    .forEach(System.out::println);

```
Output may be **unordered**, and processed by different threads.
## Stream is NOT a data structure

- It **does not store data**.
    
- It **does not modify the source**.
    
- "Stream is used only once"(Once you perform a **terminal operation** on a stream, the stream is **consumed** (closed). You **cannot reuse it again**.)
- ### Think of a Stream like a water pipe:

- Water flows through once.
    
- Once it reaches the end (terminal operation), the water is gone.
    
- You can’t "re-flow" the same water.
EXAMPLE:
```
Stream<String> stream = Stream.of("A", "B", "C");

stream.forEach(System.out::println);  // ✅ Terminal operation: works fine

stream.forEach(System.out::println);  // ❌ ERROR: Stream has already been operated upon or closed
//- Java throws an `IllegalStateException` if you try to use it again.

```

### Solution:

If you want to use it again, **create a new stream** from the source:

```
List<String> data = List.of("A", "B", "C");

data.stream().forEach(System.out::println);     // First use
data.stream().map(String::toLowerCase).toList(); // Second use (new stream)

```

Common Stream Methods (Overview)

| Method       | Type         | Purpose                      |                                                                                                                                 |
| ------------ | ------------ | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `filter()`   | Intermediate | Filters based on a condition |                                                                                                                                 |
| `map()`      | Intermediate | Transforms each element      |                                                                                                                                 |
| `flatMap()`  | Intermediate | Flattens nested structures   |                                                                                                                                 |
| `sorted()`   | Intermediate | Sorts the stream             |                                                                                                                                 |
| `limit()`    | Intermediate | Limits the number of results |                                                                                                                                 |
| `distinct()` | Intermediate | Removes duplicates           | - **Order is preserved**: the first occurrence is kept.<br>- `.distinct()` only removes **exact matches** based on `.equals()`. |



Example with Full Pipeline
```
List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6);

List<Integer> evenSquares = numbers.stream()
    .filter(n -> n % 2 == 0)      // [2, 4, 6]
    .map(n -> n * n)              // [4, 16, 36]
    .collect(Collectors.toList()); // [4, 16, 36]

```

---
**1. sorted()**
**2.Terminal operations** 
**3.map() vs flatMap()** 
**4.joining()** 
**5.collect()**

### 1.**Sorted**:
### Purpose:

To **sort the elements** in a stream based on natural order or custom rules.
```
stream.sorted();                       // natural order (e.g., a-z, 1-9)
stream.sorted(Comparator);            // custom order

```

1. Natural Sorting (Alphabetical / Numerical)
```
List<String> names = List.of("John", "Alice", "Bob");

List<String> sorted = names.stream()
    .sorted() // sorts in alphabetical order
    .collect(Collectors.toList());

System.out.println(sorted); // Output: [Alice, Bob, John]


2. Custom Sorting (Reverse Order)

List<String> names = List.of("John", "Alice", "Bob");

List<String> reversed = names.stream()
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());

System.out.println(reversed); // Output: [John, Bob, Alice]

3. Sorting by Length of Strings
List<String> names = List.of("John", "Alice", "Bob");

List<String> byLength = names.stream()
    .sorted(Comparator.comparing(String::length))
    .collect(Collectors.toList());

System.out.println(byLength); // Output: [Bob, John, Alice]

4.Sorting Numbers
List<Integer> nums = List.of(5, 2, 9, 1);

List<Integer> sortedNums = nums.stream()
    .sorted()
    .collect(Collectors.toList());

System.out.println(sortedNums); // Output: [1, 2, 5, 9]
5.distinct
List<String>remove=word.stream().distinct().toList();  
        System.out.println(remove);
  6.limit
        String limit=word.stream().limit(3).collect(Collectors.joining(","));  
        System.out.println(limit);  

```

---
### 2.**Terminal Operations** in Java Streams

### What are Terminal Operations?

Terminal operations **end** a stream pipeline and **return a result** or **produce a side-effect**.

 After a terminal operation, the stream is **consumed** and **can’t be used again**.
	
| Method        | Description                               | Example Use                    |
| ------------- | ----------------------------------------- | ------------------------------ |
| `collect()`   | Collects elements into a List, Set, etc.  | `collect(Collectors.toList())` |
| `forEach()`   | Performs action on each element           | `forEach(System.out::println)` |
| `count()`     | Counts elements in the stream             | `count()`                      |
| `findFirst()` | Gets the first element (Optional)         | `findFirst()`                  |
| `anyMatch()`  | Returns `true` if **any** element matches | `anyMatch(x -> x > 10)`        |
| `allMatch()`  | Returns `true` if **all** match           | `allMatch(x -> x > 10)`        |
| `noneMatch()` | Returns `true` if **none** match          | `noneMatch(x -> x > 10)`       |
| `reduce()`    | Combines elements into a single value     | `reduce((a, b) -> a + b)`      |
| `toArray()`   | Converts stream to array                  | `toArray(String[]::new)`       |
==IMPLEMENTING OPERATIONS==

```
1. `forEach()` – Just prints or does some action
List<String> names = List.of("A", "B", "C");

names.stream()
     .forEach(System.out::println);//is a **method reference**

2. `count()` – Counts how many elements
long count = names.stream().count();  // Output: 3

3. `collect()` – Most commonly used to get result
List<String> result = names.stream()
    .collect(Collectors.toList());

4.`findFirst()`, `anyMatch()`

Optional<String> first = names.stream().findFirst(); // A
boolean hasA = names.stream().anyMatch(n -> n.equals("A")); // true

```
### count:
**counts the number of elements** in the list using streams.

- `.count()` is a **terminal operation** that returns the **number of elements** in the stream.
    
- It returns a `long` value (not `int`) because a list can potentially have **more elements than an `int` can hold**, especially for big data processing.
#### anyMatch:-->just like a loop
n -> n.equals("A")) this declaration
for (Integer n : list) {
    if (n == 1) {
        // do something
    }

---
## `map()` vs `flatMap()` in Java Streams

Both are **intermediate operations**, but they behave differently when working with nested data like Lists of Lists.

### 1. `map()`

- Transforms each element **one-to-one**.
    
- The result is still **structured the same** (no flattening).
    

📌 Think: “**Map each item to something else**.”

```
List<String> names = List.of("alice", "bob");

List<String> upper = names.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());

System.out.println(upper); // [ALICE, BOB]

2.Mapping to list (without flattening):

List<String> words = List.of("hello", "world");

List<List<String>> mapped = words.stream()
    .map(word -> List.of(word.split("")))
    .collect(Collectors.toList());

System.out.println(mapped);
// Output: [[h, e, l, l, o], [w, o, r, l, d]]


```

map:
words = [
    ["h", "e", "l", "l", "o"],
    ["w", "o", "r", "l", "d"]
]
`List<List<String>>` → A list where **each item is a list of characters**.
### 2. `flatMap()`

- Transforms **and flattens** the result (one-to-many).
    
- Turns a stream of collections into **one flat stream**.
    

📌 Think: “**Map + Flatten** in one step.”
Example – flatten words into single letters

```
List<String> words = List.of("hello", "world");

List<String> result = words.stream()
    .flatMap(word -> Arrays.stream(word.split("")))
    .collect(Collectors.toList());

System.out.println(result);
// Output: [h, e, l, l, o, w, o, r, l, d]

Working with nested lists:

List<List<Integer>> listOfLists = List.of(
    List.of(1, 2),
    List.of(3, 4)
);

List<Integer> flatList = listOfLists.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());

System.out.println(flatList); // [1, 2, 3, 4]


```
Arrays.stream(...):
- `.split("")` gives you a `String[]` (an array of strings).
    
- We need a **Stream**, so we convert the array into a stream using:
### Practice Question:

You have a list of sentences:

`List<String> sentences = List.of("Java is fun", "Streams are powerful");`

✅ Task 1: Using **`map()`**, split each sentence into words.  
✅ Task 2: Using **`flatMap()`**, get **all words** in a single list.


### Expected Outputs:

#### Task 1 (using `map()`):

```
[
  [Java, is, fun],
  [Streams, are, powerful]
]
 Task 2 (using `flatMap()`):



`[Java, is, fun, Streams, are, powerful]`
```
---
### `joining()` – Concatenating Strings in Stream
### What is `joining()`?
is a **terminal operation** in Java Streams

It’s a **collector** used with `collect()` to **join strings** from a stream into a single string.

  You must use it with: `Collectors.joining()`
Basic Syntax:
```
Collectors.joining()                // No separator
Collectors.joining(", ")            // With separator
Collectors.joining(", ", "[", "]")  // With prefix + suffix

```

```
Example 1: Simple Join
List<String> names = List.of("Alice", "Bob", "Charlie");

String result = names.stream()
    .collect(Collectors.joining());

System.out.println(result);  // Output: AliceBobCharlie

Example 2: Join with Separator
String result = names.stream()
    .collect(Collectors.joining(", "));

System.out.println(result);  // Output: Alice, Bob, Charlie

Example 3: Separator + Prefix + Suffix
String result = names.stream()
    .collect(Collectors.joining(", ", "[", "]"));

System.out.println(result);  // Output: [Alice, Bob, Charlie]

Real-life Use Case:
List<String> csvFields = List.of("John", "Doe", "28");

String csv = csvFields.stream()
    .collect(Collectors.joining(","));

System.out.println(csv);  // Output: John,Doe,28


```

---
### ****`collect()` – The Most Common Terminal Operation
### What is `collect()`?

It is a **terminal operation** used to **gather the stream elements into a collection or summary result**.

> It's part of `java.util.stream.Collectors` utility class.
> 
> SYNTAX:
```
stream.collect(Collector)

```

Most Common Collectors

| Collector                                   | Description                                | Example Output               |
| ------------------------------------------- | ------------------------------------------ | ---------------------------- |
| `Collectors.toList()`                       | Collects into a `List`                     | `[a, b, c]`                  |
| `Collectors.toSet()`                        | Collects into a `Set` (removes duplicates) | `[a, b, c]`                  |
| `Collectors.toMap()`                        | Collects into a `Map`                      | `{key1=value1, key2=value2}` |
| `Collectors.joining()`                      | Concatenates strings                       | `a, b, c`                    |
| `Collectors.counting()`                     | Counts elements                            | `5`                          |
| `Collectors.groupingBy()`                   | Groups by a field                          | `{A=[...], B=[...]}`         |
| `Collectors.partitioningBy()`               | Partitions by condition (true/false)       | `{true=[...], false=[...]}`  |
| `Collectors.summarizingInt()` / Double/Long | Summary stats (count, min, max, etc.)      | `IntSummaryStatistics`       |
```
1.TO LIST
List<String> names = List.of("Alice", "Bob", "Charlie");

List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());

System.out.println(result); // [Alice]
2: To Set
Set<String> set = names.stream()
    .collect(Collectors.toSet());
3: To Map
Map<String, Integer> nameLengths = names.stream()
    .collect(Collectors.toMap(
        name -> name,                // key
        name -> name.length()        // value
    ));

System.out.println(nameLengths); // {Alice=5, Bob=3, Charlie=7}

4: Grouping
List<String> words = List.of("ant", "bat", "apple", "ball");

Map<Character, List<String>> grouped = words.stream()
    .collect(Collectors.groupingBy(word -> word.charAt(0)));

System.out.println(grouped);
// {a=[ant, apple], b=[bat, ball]}

5: Partitioning (true/false)
List<Integer> nums = List.of(1, 2, 3, 4, 5, 6);

Map<Boolean, List<Integer>> partitioned = nums.stream()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));

System.out.println(partitioned);
// {false=[1, 3, 5], true=[2, 4, 6]}

```

---
## Practice Challenge: Real-World Stream Task

### Scenario:

You have a list of `Employee` objects with fields: `name`, `department`, and `salary`.

```
class Employee {
    String name;
    String department;
    int salary;

    // constructor + getters
}

```

And the data:

```
List<Employee> employees = List.of(
    new Employee("Alice", "IT", 5000),
    new Employee("Bob", "HR", 4000),
    new Employee("Charlie", "IT", 6000),
    new Employee("David", "Sales", 3000),
    new Employee("Eve", "HR", 4500)
);

```

### Tasks to Perform Using Streams:

1. Get a list of names of employees in the "IT" department.
    
2. Calculate the total salary of all employees.
    
3. Get a map of department to list of employee names (`Map<String, List<String>>`)
    
4. Get a comma-separated string of all employee names sorted alphabetically.
    
5. Partition employees based on salary > 4500.