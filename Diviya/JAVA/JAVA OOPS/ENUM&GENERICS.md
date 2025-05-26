### ==ENUMS==
	An **`enum` (short for "enumeration")** is a special data type in Java that represents a **fixed set of constants**.
- enums are useful for representing fixed sets of values, like days of the week, levels of priority, or directions (north, south, etc.).
Declaration Rules:
- You **must declare constants first** in an enum. Only then you can declare variables, constructors, and methods.

Enum example:
```
import java.util.EnumSet;  
import java.util.Scanner;  
  
public class demo2 {  
 public enum days{;  
  MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY,SUNDAY//defaul these are public static final variables 
  //if we want can also declare expilictly 

    public static final String name="gg";  
  
  
 }  
    public static void main(String[] args) {  
  
  //String d=days.name;  
  days day=days.monday;
System.out.println(d);  
    
    }  
}
```

**Complete** **EXAMPLE** **OF Enum**

```
import java.util.Scanner;  
  
public class demo1 {  
    public enum Status {  
    ACTIVE(1),  
    INACTIVE(0),  
    PENDING(-1);  
  
    private int value;  
  
    // Constructor  
    Status(int value) {  
        this.value = value;  
    }  
  
    public int getValue() {  
        return value;  
    }  
  
    public static Status fromValue(int value) {  
        for (Status status : Status.values()) {  
            if (status.getValue() == value) {  
                return status;  
            }  
        }  
        throw new IllegalArgumentException("Invalid value: " + value);  
    }  
}  
  
    public static void main(String[] args) {  
        // Access individual enum constants and their values  
        Status s1 = Status.ACTIVE;  
        System.out.println("Status: " + s1 + ", Value: " + s1.getValue());  
  
        Status s2 = Status.INACTIVE;  
        System.out.println("Status: " + s2 + ", Value: " + s2.getValue());  
  
        Status s3 = Status.PENDING;  
        System.out.println("Status: " + s3 + ", Value: " + s3.getValue());  
  
        // Using fromValue method  
        Status s4 = Status.fromValue(0);  
        System.out.println("Status from value 0: " + s4);  
//loop  
        for (Status status : Status.values()) {  
            System.out.println("Name: " + status + ", Value: " + status.getValue());  
        }  
        for (Status status : Status.values()) {  
            System.out.println(status);  // prints the constant name (e.g., ACTIVE)  
        }  
  
    }  
}
```

Traffic Signal Enum Example:
```
enum TrafficSignal {
    RED("Stop"),
    YELLOW("Ready"),
    GREEN("Go");

    private final String message;

    TrafficSignal(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }

    public static TrafficSignal fromCode(int code) {
        switch (code) {
            case 1: return RED;
            case 2: return YELLOW;
            case 3: return GREEN;
            default: return null;
        }
    }
}
import java.util.Scanner;

public class DemoEnum {
    public static void main(String[] args) {
        System.out.println("1. RED");
        System.out.println("2. YELLOW");
        System.out.println("3. GREEN");
        System.out.print("Enter a number: ");

        Scanner sc = new Scanner(System.in);
        int code = sc.nextInt();

        TrafficSignal signal = TrafficSignal.fromCode(code);

        if (signal != null) {
            System.out.println("Signal Message: " + signal.getMessage());
        } else {
            System.out.println("No matching signal");
        }
    }
}

```

**Features of enum**

1.    **Type-Safety**: Using an enum helps enforce type safety. For instance, you can’t pass a random String where an enum value is expected.

2.    **Implicit Finality**: Enum constants are implicitly public static final, meaning they can be accessed directly and cannot change.

3.    **Enhanced Readability**: Using meaningful names like NORTH, SOUTH, etc., makes code more readable than using arbitrary constants like 0, 1, etc.

**Rules for Enums**

1.    **Naming**: By convention, enum constants should be in uppercase (e.g., LOW, HIGH).

2.    **Cannot Inherit**: Enums cannot extend other classes because they already extend java.lang.Enum.

3.    **Constructors**: Enum constructors are implicitly private, and they can’t be accessed outside the enum.

4.    **No Instances**: Enum constants are single instances, meaning there are no new instances.

5.    **Methods**: Enums can have methods, but they should serve a purpose specific to that enum.

**Outside a Class:** If the enum is to be used by multiple classes, declare it as a top-level type.

**Inside a Class:** If the enum is closely related to a specific class and not intended for use elsewhere, declare it within that class.

  **Enum constants are instances of their enum class and are typically immutable.**

  **Constructors are used to initialize the state of these constants at the time of their creation.**

  **Setter methods are generally not provided for enum constants due to their immutable nature.**

***Enum constants can be accessed directly inside the enum class without using the class name.
### But Outside the Enum?

Outside the enum, you **must** use:

`TrafficSignal.RED`

Because the constants are public `static final` members of the enum class, so you need the class name to access them.

---
### ENUM OBJECT:

###### Java internally creates enum objects when the class loads.**  
###### You never use `new` — the compiler and JVM do that for you **automatically**.
### Why?

Because **inside the enum**, those constants (like `RED`, `YELLOW`, `GREEN`) are already **in scope** 
just like how you can access a field or method directly inside its own class.

##### **Can I write this explicitly like:**

### public static final TrafficSignal RED = new TrafficSignal("Stop");
Answer:

- ✅ **Yes**, you can write this **manually in a regular class**.
    
- ❌ **No**, you cannot do this inside an `enum` directly — because the compiler **already does it automatically** for you.
## First: Recap of Your Core Doubts

| ❓ Doubt                                                 | ✅ Explanation                                                                                   |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Is `RED` a variable or object?**                      | It's a `public static final` reference variable pointing to a singleton object created by Java. |
| **Why no `new` keyword with enums?**                    | Java automatically creates enum objects during class loading. You never write `new` for enums.  |
| **Are enum variables static?**                          | ✅ Yes — constants like `RED`, `YELLOW` are `public static final`.                               |
| **Can we access instance methods like `getMessage()`?** | ✅ Yes, because they are called on pre-created enum objects.                                     |
| **Can we write `public static final` ourselves?**       | ✅ Yes, in a normal class (not enum) to simulate enum behavior manually.                         |
| **Do non-enum classes create objects automatically?**   | ❌ No — you need to use `new` in normal classes. Enums are special.                              |
## What You **Can** Do in Enums

| ✅ Allowed in Enums             | 📝 Notes                                                                             |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| Define constructors            | ✅ Private or package-private only (implicitly private).                              |
| Define fields                  | ✅ Like `private final String message;`                                               |
| Define methods                 | ✅ Instance methods, static methods, even abstract methods (but must be implemented). |
| Implement interfaces           | ✅ Enums can implement interfaces (e.g., `Comparable`, custom interfaces).            |
| Override methods per constant  | ✅ You can override a method differently for each constant.                           |
| Use in `switch-case`           | ✅ Very useful with switch statements.                                                |
| Use `values()` and `valueOf()` | ✅ Provided automatically by Java.                                                    |
| Enum with parameters           | ✅ Can define values like `RED("Stop")`.                                              |


---

## What You _Cannot_ Do Inside Enums in Java

| ❌ Not Allowed in Enums                                                        | ❓ Why / Notes                                                                                    |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| ❌ Use `new` to create enum objects                                            | Enum objects are **created automatically** by Java.                                              |
| ❌ Extend another class                                                        | Enums **already extend `java.lang.Enum`** implicitly. You can't extend other classes.            |
| ❌ Use multiple constructors in objects                                        | You **can overload constructors**, but each enum constant must call one specific constructor.    |
| ❌ Instantiate using `new` keyword outside                                     | Cannot write `TrafficSignal signal = new TrafficSignal()` — not allowed.                         |
| ❌ Use `extends` (inheritance)                                                 | Java enums **cannot extend** other classes.                                                      |
| ❌ Enums as inner classes inside methods                                       | You **cannot declare enum inside a method**. But you _can_ declare an enum inside another class. |
| ❌ Enum constants with duplicate names                                         | Enum constants must be **unique** in name. You can't repeat like `RED, RED`.                     |
| ❌ Abstract enums with unimplemented methods (without overriding in constants) | If enum has `abstract` methods, **each constant must override** it.                              |

### ENUM IMPLEMENTS INTERFACE:

```
// Interface that defines the action method
interface SignalAction {
    String action();
}

// Enum implementing the interface
enum TrafficSignal implements SignalAction {
    RED("Stop") {
        public String action() {
            return "Wait.";
        }
    },
    GREEN("Go") {
        public String action() {
            return "Proceed.";
        }
    },
    YELLOW("Ready") {
        public String action() {
            return "Slow.";
        }
    };

    private final String message;

    TrafficSignal(String msg) {
        this.message = msg;
    }

    public String getMessage() {
        return message;
    }
}

// Main class to use the enum and interface
public class DemoEnumWithInterface {
    public static void main(String[] args) {
        for (TrafficSignal signal : TrafficSignal.values()) {
            System.out.println("Signal: " + signal);
            System.out.println("Message: " + signal.getMessage());
            System.out.println("Action: " + signal.action());
            System.out.println("-----------");
        }
    }
}

```


---
## Example of a Feature-Rich Enum

```
import java.util.Scanner;

enum Signal {
    RED("Stop") {
        public String action() {
            return "Wait at the signal.";
        }
    },
    GREEN("Go") {
        public String action() {
            return "Proceed.";
        }
    },
    YELLOW("Ready") {
        public String action() {
            return "Slow down.";
        }
    };

    private final String message;

    Signal(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }

    // Abstract method - must be implemented by all enum constants
    public abstract String action();
}

public class TrafficDemo {
    public static void main(String[] args) {
        System.out.println("1. RED");
        System.out.println("2. YELLOW");
        System.out.println("3. GREEN");
        System.out.print("Enter a number (1-3): ");

        Scanner sc = new Scanner(System.in);
        int input = sc.nextInt();
        Signal selectedSignal = null;

        switch (input) {
            case 1: selectedSignal = Signal.RED; break;
            case 2: selectedSignal = Signal.YELLOW; break;
            case 3: selectedSignal = Signal.GREEN; break;
            default:
                System.out.println("Invalid input.");
                return;
        }

        System.out.println("Signal: " + selectedSignal);
        System.out.println("Message: " + selectedSignal.getMessage());
        System.out.println("Action: " + selectedSignal.action());
    }
}


```



---
PROBLEM 1:
```
import java.util.EnumSet;

// Step 1: Define the enum
enum Permission {
    READ,
    WRITE,
    DELETE,
    EXECUTE
}

// Step 2: Role class with EnumSet
class Role {
    private String roleName;
    private EnumSet<Permission> permissions;

    public Role(String roleName, EnumSet<Permission> permissions) {
        this.roleName = roleName;
        this.permissions = permissions;
    }

    public String getRoleName() {
        return roleName;
    }

    public boolean hasPermission(Permission permission) {
        return permissions.contains(permission);
    }

    public void displayPermissions() {
        System.out.println("Permissions for role " + roleName + ": " + permissions);
    }
}

// Step 3: User class with role
class User {
    private String userName;
    private Role role;

    public User(String userName, Role role) {
        this.userName = userName;
        this.role = role;
    }

    public void checkAccess(Permission permission) {
        System.out.println(userName + " has " + permission + " permission? " + role.hasPermission(permission));
    }

    public void showDetails() {
        System.out.println("User: " + userName + ", Role: " + role.getRoleName());
        role.displayPermissions();
    }
}

// Step 4: Main class
public class UserAccessSystem {
    public static void main(String[] args) {
        // Create roles
        Role admin = new Role("Admin", EnumSet.of(Permission.READ, Permission.WRITE, Permission.DELETE, Permission.EXECUTE));
        Role editor = new Role("Editor", EnumSet.of(Permission.READ, Permission.WRITE));
        Role viewer = new Role("Viewer", EnumSet.of(Permission.READ));

        // Create users
        User u1 = new User("Alice", admin);
        User u2 = new User("Bob", editor);
        User u3 = new User("Charlie", viewer);

        // Display details
        u1.showDetails();
        u2.showDetails();
        u3.showDetails();

        System.out.println();

        // Check permissions
        u1.checkAccess(Permission.DELETE);   // true
        u2.checkAccess(Permission.DELETE);   // false
        u3.checkAccess(Permission.READ);     // true
        u3.checkAccess(Permission.WRITE);    // false
    }
}

```

#### **question for above problem**
##### Design a system that manages access permissions for different user roles in a software application. Each role can have multiple permissions like READ, WRITE, DELETE, EXECUTE, etc. Use enum to represent permissions, EnumSet to handle multiple permissions, and OOP principles to represent Users and Roles."

---
explore the capabilities of Java **enum constants**

### **Act as Objects**

**Explanation:**  
Each enum constant is an instance of its enum type, behaving like an object.

```
enum Color {
    RED, GREEN, BLUE;
}

Color c = Color.RED;
System.out.println(c); // Output: RED

```

### **Call Methods**

**Explanation:**  
Enum constants can invoke methods defined within the enum.
```
enum Color {
    RED;

    public String getMessage() {
        return "Stop";
    }
}

System.out.println(Color.RED.getMessage()); // Output: Stop

```

### **Override Methods**

**Explanation:**  
Enum constants can override methods, allowing each to have distinct behavior.

```
enum Color {
    RED {
        @Override
        public void paint() {
            System.out.println("Painting red");
        }
    },
    GREEN {
        @Override
        public void paint() {
            System.out.println("Painting green");
        }
    };

    public abstract void paint();
}

Color.RED.paint();   // Output: Painting red
Color.GREEN.paint(); // Output: Painting green

```

### **Are Static Final**

**Explanation:**  
Enum constants are implicitly `public static final`, ensuring they are immutable and globally accessible.

```
enum Color {
    RED, GREEN, BLUE;
}

// Attempting to reassign will result in a compilation error
// Color.RED = Color.GREEN; // Error: cannot assign a value to final variable 'RED'

```

### **Hold Data**

**Explanation:**  
Enum constants can have associated data through fields and constructors.

```
enum Color {
    RED("Stop"), GREEN("Go");

    private final String message;

    Color(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}

System.out.println(Color.RED.getMessage()); // Output: Stop

```

### **Use in switch-case**

**Explanation:**  
Enums integrate seamlessly with switch statements for control flow.

```
enum Color {
    RED, GREEN, BLUE;
}

Color color = Color.RED;

switch (color) {
    case RED:
        System.out.println("Stop");
        break;
    case GREEN:
        System.out.println("Go");
        break;
    case BLUE:
        System.out.println("Calm");
        break;
}

```

### **Use in EnumSet / EnumMap**

**Explanation:**  
Java provides specialized collections for enums: `EnumSet` and `EnumMap`.

```
import java.util.EnumSet;

enum Color {
    RED, GREEN, BLUE;
}

EnumSet<Color> primaryColors = EnumSet.of(Color.RED, Color.BLUE);
System.out.println(primaryColors); // Output: [RED, BLUE]

```

### **Access Utility Methods**

**Explanation:**  
Enums come with built-in methods like `values()`, `name()`, and `ordinal()`.

```
enum Color {
    RED, GREEN, BLUE;
}

for (Color color : Color.values()) {
    System.out.println("Name: " + color.name() + ", Ordinal: " + color.ordinal());
}

```
---

#### **ENUMSET**
### `enum` is also a **special class** in Java.

But it’s handled differently by the **Java compiler and JVM**, which allows certain optimizations and features like `EnumSet`.
### **So** **why does `EnumSet` work only with enums?**

#### 📌 1. **`EnumSet` is a special collection designed only for enums.**

- It's a highly optimized set implementation.
    
- It works **only** with enums for performance reasons — it uses bitwise operations internally.
    
- You **cannot** use `EnumSet` with normal classes or objects.
Internally, it uses bit vectors to represent elements, making operations like `add`, `remove`, and `contains` extremely efficient. All elements in an `EnumSet` must be of the same enum type.
### Advantages of `EnumSet`

- **Performance**: Operations are faster than with other `Set` implementations like `HashSet`, especially when dealing with enums.​[Stack Overflow+1Oracle Documentation+1](https://stackoverflow.com/questions/11825009/what-does-enumset-really-mean?utm_source=chatgpt.com)
    
- **Type Safety**: Ensures that only enum constants of the specified type can be added.​
    
- **Memory Efficiency**: Internally uses bit vectors, making it more memory-efficient
### Thread Safety

`EnumSet` is not synchronized. If multiple threads access an `EnumSet` concurrently and at least one of the threads modifies it, it must be synchronized externally. This is typically done by synchronizing on some object that naturally encapsulates the `EnumSet`.

```
public static void main(String[] args) {

        // Creating an EnumSet with specific days

        EnumSet<Day> weekend = EnumSet.of(Day.SATURDAY, Day.SUNDAY);

        System.out.println("Weekend days: " + weekend);

        // Creating an EnumSet with all days

        EnumSet<Day> allDays = EnumSet.allOf(Day.class);

        System.out.println("All days: " + allDays);

        // Creating an empty EnumSet

        EnumSet<Day> noDays = EnumSet.noneOf(Day.class);

        System.out.println("No days: " + noDays);

        // Creating an EnumSet with a range of days

        EnumSet<Day> midWeek = EnumSet.range(Day.TUESDAY, Day.THURSDAY);

        System.out.println("Midweek days: " + midWeek);

        // Creating an EnumSet with the complement of another EnumSet

        EnumSet<Day> weekdays = EnumSet.complementOf(weekend);

        System.out.println("Weekdays: " + weekdays);

    }

}
```

## ==GENERICS==

## **What is Generics in Java?**

**Generics** means writing **code that works with any data type**, without rewriting it again and again.
Generics = write once, use for any data type, safely and without casting.
this will hold one type at compile time 
- when you define a generic class like `Cage<T>`, the type parameter `T` is declared at the class level. This means that all methods within the class can use `T` directly without needing to declare it again.
## What is `<T>` in Java?

###  It’s a **Generic Type Parameter**

`<T>` tells Java that you're writing **generic code**, and `T` stands for a **placeholder type**. The actual type will be **decided later** (at runtime or when the method/class is used).

| Type                   | Can be auto-boxed? |
| ---------------------- | ------------------ |
| `int → Integer`        | ✅ Yes              |
| `int[] → Integer[]`    | ❌ No               |
| `char → Character`     | ✅ Yes              |
| `char[] → Character[]` | ❌ No               |

- Generics (`<T>`) don’t work with primitives like `int`, `double`, etc.
    
- Use wrapper classes (`Integer`, `Double`) or overload the method for primitive types.
### **Option 1: Use Wrapper Class (`Integer[]` instead of `int[]`)**

```
public class demo1 {
    public <T> void display(T[] elemt) {
        for (int i = 0; i < elemt.length; i++) {
            System.out.println(elemt[i]);
        }
    }

    public static void main(String[] args) {
        demo1 d = new demo1();
        Integer ar[] = {1, 2, 3}; // Use Integer instead of int
        String arr[] = {"h", "i"};
        d.display(ar);
        d.display(arr);
    }
}

```
### **Option 2: Overload method to handle primitives**

If you want to support both primitive and generic types, you can overload the `display()` method:
seperately write a method to int data

---
THIS WILL WORK:


```
public class demo1 {
    public <T> void display(T elemt) {
        System.out.println(elemt);
    }

    public static void main(String[] args) {
        demo1 d = new demo1();
        int t = 66;
        String g = "go";
        d.display(t);  // Line A
        d.display(g);  // Line B
    }
}

```

- **Java auto-boxes primitive types** like `int`, `double`, `char` when passed to a method expecting an object.
    
    - In line `d.display(t);`, `int t = 66` is **auto-boxed** to `Integer`, which is an object.
        
    - So, `T` becomes `Integer`.
        
- `String` is already a reference type, so it's passed directly.
- ### Type Inference:

Java can infer the type `T` at **compile-time** based on the argument:

- `d.display(66);` → becomes `display<Integer>(66);`
    
- `d.display("go");` → becomes `display<String>("go");`
    

This works perfectly fine because `T` is inferred based on the actual argument type, and since you're passing **individual values** (not arrays), **boxing takes care of the primitive-to-object conversion**.

## **Generic Interfaces**

You can create **interfaces** that work with any data type. This is useful for defining **common behavior** that applies to different types.

```
public interface Storage<T> {
    void add(T item);
    T get();
}
public class BoxStorage implements Storage<String> {
    private String item;

    @Override
    public void add(String item) {
        this.item = item;
    }

    @Override
    public String get() {
        return item;
    }
}

```


## **Generic Interfaces with Multiple Type Parameters**

You can create interfaces with **multiple generics** (e.g., `<T, U>`).

```
public interface Pair<K, V> {
    K getKey();
    V getValue();
}
public class SimplePair implements Pair<Integer, String> {
    private Integer key;
    private String value;

    @Override
    public Integer getKey() {
        return key;
    }

    @Override
    public String getValue() {
        return value;
    }
}

```

## **Generic Collections**

Generics are **heavily used in Java collections** like `List`, `Set`, `Map`, etc., to define the type of objects the collection will hold.

```
List<String> list = new ArrayList<>();
list.add("Hello");
list.add("World");

```
### Usage:

- **Where to Use:** In **collections** to ensure that only a specific type of object is stored.
## **Generic Constructors**

You can define **generic constructors** within a class that works with different data types. This allows you to create **instances** of a class that can hold different types of data.

### Example:
```
public class Pair<T, U> {
    private T first;
    private U second;

    // Generic constructor
    public Pair(T first, U second) {
        this.first = first;
        this.second = second;
    }

    // Getters for both values
    public T getFirst() {
        return first;
    }

    public U getSecond() {
        return second;
    }

    public static void main(String[] args) {
        // Creating a Pair of Integer and String
        Pair<Integer, String> pair1 = new Pair<>(1, "Apple");
        System.out.println("First: " + pair1.getFirst() + ", Second: " + pair1.getSecond());

        // Creating a Pair of Double and Boolean
        Pair<Double, Boolean> pair2 = new Pair<>(3.14, true);
        System.out.println("First: " + pair2.getFirst() + ", Second: " + pair2.getSecond());
    }
}

```

## **Bounded Generics**

**Bounded generics** allow you to specify a **restriction** on the types that a generic can accept. You can restrict the type to a subclass or class that extends another class or implements an interface.
```
public class BoundedGenerics {

    // Only accepts subclasses of Number (e.g., Integer, Double)
    public <T extends Number> void printNumber(T number) {
        System.out.println("The number is: " + number);
    }

    public static void main(String[] args) {
        BoundedGenerics bg = new BoundedGenerics();
        
        // Works with Integer
        bg.printNumber(5);    // Output: The number is: 5
        
        // Works with Double
        bg.printNumber(3.14); // Output: The number is: 3.14
        
        // Uncommenting the following line will cause a compile-time error:
        // bg.printNumber("Hello");  // Error: String does not extend Number
    }
}

```

### Explanation:

- **Bounded Type Parameter**: `<T extends Number>` restricts the type `T` to any subclass of `Number` (like `Integer`, `Double`, etc.).
    
- **Use case**: Useful when you want to **limit the acceptable types** for your generic method to a specific class or its subclasses, ensuring you only work with numeric types in this case.
    

---

##  **Wildcard Generics (`?`)**

The **wildcard `?`** represents an unknown type. This is useful when you want to work with a collection or method that can accept **any type**, but you don't need to know or care about the specific type. It's often used in **read-only** operations.
```
import java.util.*;

public class WildcardGenerics {

    // A method that accepts a List of any type (Wildcards)
    public void printList(List<?> list) {
        for (Object item : list) {
            System.out.println(item);
        }
    }

    public static void main(String[] args) {
        WildcardGenerics wg = new WildcardGenerics();
        
        // List of Strings
        List<String> stringList = Arrays.asList("Apple", "Banana", "Cherry");
        wg.printList(stringList);  // Output: Apple, Banana, Cherry
        
        // List of Integers
        List<Integer> intList = Arrays.asList(1, 2, 3);
        wg.printList(intList);  // Output: 1, 2, 3
    }
}

```
### Explanation:

- **Wildcard `?`**: In `List<?>`, the `?` means the list can contain any type (but not a primitive type like `int`). We don't care what the specific type is — we just want to **process** the elements without modifying them it return a type is unknown in compile time.
    
- **Use case**: Wildcards are **ideal for read-only operations** when you don’t need to know the exact type. You might use this in methods that simply print out or iterate over data.
### Quick Comparison

- **T (or E, K, V, etc.):**
    
    - **Definition:** A named type parameter.
        
    - **Usage:** You must provide a specific type when using the class or method.
        
    - **Example:** `Box<String>` means T is String.
        
- **Wildcard (?):**
    
    - **Definition:** Represents an unknown type.
        
    - **Usage:** Used when you want to accept any type without specifying it.
        
    - **Example:** `List<?>` can be a list of any type.
---
## Return multiple data type values in one method

#### Problem:
Java methods can **only return one value**.
#### Solution:

To return **multiple values**, we wrap them in a class like `Pair<T, V>`.

So this lets you return:

- Two values of different types
    
- Clean and structured access to both values
```
class  pair<T,V>  
{  
    T first;  
    V second;  
    pair(T val1,V val2)  
    {  
        this.first=val1;  
        this.second=val2;  
    }  
}  
class gen<T, V> {  
    private T val1;  
    private V val2;  
  
    public void set(T val1, V val2) {  
        this.val1 = val1;  
        this.val2 = val2;  
    }  
  
    public pair<T, V> getval() {  
        return new pair<>(val1, val2);  
    }  
}  
public class generic {  
    public static void main(String[] args) {  
        gen<String, Integer> gen1 = new gen<>();
          
        gen1.set("YES", 88);  
  
        pair<String, Integer> result = gen1.getval(); 
         
        System.out.println(result.first);  // YES  
        System.out.println(result.second); // 88  
  
    }  
}
```
## **Where** **This Pattern is Used in Real Life**:
#### **When you want to return multiple values from a method**

Example: Returning both **status and data** from an API method

```
pair<Boolean, String> response = fetchUser();
if (response.first) {
    System.out.println("Success: " + response.second);
} else {
    System.out.println("Failed to fetch user.");
}

```
#### 2. **Working with key-value data**

Even though Java has `Map.Entry`, if you want your own custom structure with better naming or behavior, you might use a custom pair.

```
pair<String, Integer> user = new pair<>("John", 25);
System.out.println(user.first);  // John
System.out.println(user.second); // 25

```
#### 3. **Algorithms and data structures**

In **graph problems**, **coordinate tracking**, or **DP solutions**, this is very common.
```
pair<Integer, Integer> point = new pair<>(3, 5); // x=3, y=5

```

**Where Can You Use Generics?**

| **Area**                     | **Use Case**                                                                    |
| ---------------------------- | ------------------------------------------------------------------------------- |
| **Classes**                  | Create **type-safe classes** for working with different types (e.g., `Box<T>`). |
| **Methods**                  | Create **generic methods** that work with different types (e.g., `print(T)`).   |
| **Interfaces**               | Define common behaviors for any type (e.g., `Storage<T>`).                      |
| **Collections**              | Store **specific types of objects** in collections (e.g., `List<Integer>`).     |
| **Bounded Generics**         | Restrict types to a specific class or interface (e.g., `T extends Number`).     |
| **Wildcards (`?`)**          | Accept any type in a collection but without caring about the type.              |
| **Multiple Type Parameters** | Handle **multiple related types** (e.g., `Pair<T, U>`).                         |
