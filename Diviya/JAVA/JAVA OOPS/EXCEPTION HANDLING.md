Exception handling in Java is a powerful mechanism to handle runtime errors, ensuring the smooth flow of the application.
	An **exception** is an event that disrupts the normal flow of a program's execution.
**Types of Exceptions**

- **Unchecked = Optional to handle, but still important.**
    
- **Checked = Must handle, compiler enforces it.**

1.    **Checked Exceptions**:

o   Exceptions that are checked at compile time.

o   Must be declared in a throws clause or handled with try-catch.

o   Examples: IOException, SQLException.

2.    **Unchecked Exceptions**:

o   Exceptions that occur at runtime.

o   Subclasses of RuntimeException.

o   Examples: NullPointerException, ArithmeticException.

3.    **Errors**:

o   Serious problems that an application cannot handle.

Examples: OutOfMemoryError, StackOverflowError.

---
### Exception Hierarchy

Throwable

├── Exception        // You can handle (most of the time)

│   ├── Checked

│   └── Unchecked

└── Error            // You should not handle

**HIERARCHY OVERVIEW**
├── Error (cannot be recovered)

│   ├── OutOfMemoryError

│   ├── StackOverflowError

│   └── VirtualMachineError

├── Exception (can be handled)

│   ├── Checked Exceptions

│   │   ├── IOException

│   │   └── SQLException

│   └── Unchecked Exceptions (RuntimeException)

│       ├── NullPointerException

│       ├── ArithmeticException

│       ├── IndexOutOfBoundsException

│       └── IllegalArgumentException

---
**Keywords in Exception Handling**

**1. try**

The block of code where exceptions may occur.

**2. catch**

Handles exceptions thrown in the try block.

**3. finally**

A block that always executes (optional) even if an exception is thrown (for cleanup)is used for cleanup code.
> To make sure important cleanup code **always runs** — whether an exception happens or not.
### In Short:

- Ensures **resources are closed**
    
- Runs **even if exception or return occurs**
    
- Keeps program **safe and clean**
    

---

📌 **Use `finally` for:**  
Closing files, database connections, releasing locks, resetting variables, or logging — things that **must always happen** at the end.

**4. throw**

Used to explicitly throw an exception.

**5. throws**

Declares exceptions that a method can throw.

---
### 1. **Checked Exceptions**

#### What makes an **unchecked exception** occur?

- **Programming bugs** or **logical mistakes** that the programmer should avoid, but they are not always predictable or external.
    
- **Examples**: Invalid calculations, array bounds errors, null pointer dereferencing, etc.

- Checked at **compile time**.
    
- Must be handled using `try-catch` or declared with `throws`.

    #### What makes a **checked exception** occur?

- **External issues** that are beyond the programmer's control or are part of **normal program execution**.
    
- They are usually conditions that **require handling** to prevent program crashes.
    
- **Examples**: File handling, network issues, database errors, etc.
#### Common Checked Exceptions (with examples):

| Exception                | When it Occurs                              |
| ------------------------ | ------------------------------------------- |
| `IOException`            | Input/output failures (e.g. file not found) |
| `SQLException`           | Database access errors                      |
| `ClassNotFoundException` | Class not found while loading dynamically   |
| `InterruptedException`   | Thread interrupted while sleeping/waiting   |
##### Code Example – Checked Exception (`IOException`)

```
import java.io.*;

public class CheckedExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("data.txt"); // File not found may occur
            BufferedReader br = new BufferedReader(file);
            System.out.println(br.readLine());
        } catch (IOException e) {
            System.out.println("IOException occurred: " + e.getMessage());
        }
    }
}
	
```

2. `SQLException` – Database error (simulated)
```
import java.sql.*;

public class CheckedSQLException {
    public static void main(String[] args) {
        try {
            Connection conn = DriverManager.getConnection("invalid-url");
        } catch (SQLException e) {
            System.out.println("Database error: " + e);
        }
    }
}

```

3. `ClassNotFoundException` – Class not found when using reflection

```
public class CheckedClassNotFound {
    public static void main(String[] args) {
        try {
            Class.forName("com.unknown.MyClass");
        } catch (ClassNotFoundException e) {
            System.out.println("Class not found: " + e);
        }
    }
}

```

4. `InterruptedException` – Thread interruption
```
public class CheckedInterrupted {
    public static void main(String[] args) {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println("Thread interrupted: " + e);
        }
    }
}

```

---
### **Unchecked Exceptions (Optional to handle, but important)**

1. `ArithmeticException` – Divide by zero
```
public class UncheckedArithmetic {
    public static void main(String[] args) {
        int a = 10, b = 0;
        int result = a / b; // Runtime crash
    }
}

```
2. `NullPointerException` – Accessing null object
```
public class UncheckedNull {
    public static void main(String[] args) {
        String s = null;
        System.out.println(s.length()); // NullPointerException
    }
}

```


3. `ArrayIndexOutOfBoundsException` – Invalid array index

```
public class UncheckedArray {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        System.out.println(arr[5]); // Index 5 doesn't exist
    }
}

```
4. `NumberFormatException` – Invalid string to number conversion
```
public class UncheckedNumberFormat {
    public static void main(String[] args) {
        String value = "abc";
        int num = Integer.parseInt(value); // Error
    }
}

```

5. `IllegalArgumentException` – Invalid method argument
```
public class UncheckedIllegalArgument {
    public static void main(String[] args) {
        Thread t = new Thread();
        t.setPriority(11); // Invalid priority > 10
    }
}

```

6. `IllegalStateException` – Calling a method at the wrong time
```
import java.util.*;

public class UncheckedIllegalState {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        Iterator<String> it = list.iterator();
        it.remove(); // Illegal because next() not called
    }
}

```

- Yes, you **can and should handle unchecked exceptions** in real-world apps.
    
- Just because the compiler doesn’t force you, doesn’t mean you should ignore them.
    
-  Handle them to prevent crashes and ensure better user experience.
---

## `finally` block
Used to write **code that must always run**, whether or not an exception occurred.
### When to use:

- To **close files**, **release resources**, **cleanup**, etc.
```
public class FinallyExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Caught: " + e);
        } finally {
            System.out.println("This will always execute.");
        }
    }
}

```

### 1. `throw` keyword

Used to **explicitly throw an exception** (usually inside a method or block)
**Where to use**: Inside a method or a code block when you want to **manually trigger an exception**.
```
throw new ExceptionType("message");

```

```
public class ThrowExample {
    public static void main(String[] args) {
        int age = 15;
        if (age < 18) {
            throw new ArithmeticException("Not eligible to vote");
        }
    }
}
```
*The program will stop here and print the error.

###  2. `throws` keyword

Used in the **method signature** to declare that a method **might throw** an exception.
- **Purpose**: You use `throws` to **declare that a method might throw an exception**. You **don’t throw** the exception immediately but **declare that the method could throw it** in the future.
    
- **Where to use**: In the **method signature**, when you call methods that might throw **checked exceptions** (like `IOException`).

```
public void method() throws IOException, SQLException

```

```
import java.io.*;

public class ThrowsExample {
    public static void main(String[] args) throws IOException {
        checkFile();  // Compiler forces us to handle or declare this
    }

    public static void checkFile() throws IOException {
        FileReader fr = new FileReader("file.txt");  // May throw FileNotFoundException
    }
}

```
## Tip:

- Use `throw` when you want to **throw an exception manually**.
    
- Use `throws` to **declare** that a method _might_ throw a checked exception.
    
- For **unchecked exceptions**, `throws` is optional — use it only if you want to be explicit.

---
## **Errors in Java (like `OutOfMemoryError`, `StackOverflowError`) should NOT be handled in most cases.**

### Why?

Errors represent **serious issues related to the JVM or system**, such as:

- Memory is exhausted (`OutOfMemoryError`)
    
- Stack is full due to recursion (`StackOverflowError`)
    
- System resources are broken (`InternalError`, `VirtualMachineError`)
    

These are **not caused by bugs in your code logic**, and most of the time, **you cannot recover** from them safely

1. `OutOfMemoryError`
```
public class ErrorOutOfMemory {
    public static void main(String[] args) {
        int[] bigArray = new int[Integer.MAX_VALUE]; // May crash JVM
    }
}

```

2. `StackOverflowError`
```
public class ErrorStackOverflow {
    public static void recursive() {
        recursive(); // Infinite recursion
    }

    public static void main(String[] args) {
        recursive();
    }
}

```

Even though you **can catch** `Error`, it's not recommended because:

- It doesn't fix the underlying problem.
    
- It may leave the application in an unstable state.
### **Imagine this situation:**

"*It may leave the application in an unstable state"
**Suppose your program catches a `StackOverflowError` or `OutOfMemoryError`, and it doesn't crash. Now you might think: "Nice, I caught the error! Let’s continue."**

**BUT...**

- **The JVM memory might be corrupted.**
    
- **Important data might be lost or half-written.**
    
- **Threads might be stuck or terminated.**
    
- **Some resources (like database connections or files) might be in a broken state.**
    
- **Future code might throw unexpected exceptions or behave randomly.**
    

**This condition is called an unstable state, where:**

- **You can't trust the program to behave correctly anymore.**
    
- **The safest option is usually to shut it down gracefully.**

## When might you catch `Error`?

 **Rarely**, and only for **logging, testing, or cleanup purposes**, like:

---
### CUSTOM EXCEPTION;
What is a Custom Exception in Java?
A **custom exception** is an exception that **you define yourself** by creating a new class that **extends `Exception` or `RuntimeException`**.

It’s useful when:

- You want to give **more meaningful error messages**.
    
- You want to handle **specific business logic errors**.
    
- Built-in exceptions like `IOException`, `NullPointerException` don’t fit your situation.
### How to Create a Custom Exception

#### Checked Custom Exception (extends `Exception`)
```
class AgeNotValidException extends Exception {
    public AgeNotValidException(String message) {
        super(message);
    }
}

```
Unchecked Custom Exception (extends `RuntimeException`)
```
class MyRuntimeError extends RuntimeException {
    public MyRuntimeError(String message) {
        super(message);
    }
}

```
Example: Custom Checked Exception in Action
```
class AgeNotValidException extends Exception {
    public AgeNotValidException(String msg) {
        super(msg);
    }
}

public class VoterCheck {
    public static void checkAge(int age) throws AgeNotValidException {
        if (age < 18) {
            throw new AgeNotValidException("You must be 18+ to vote!");
        } else {
            System.out.println("You are eligible to vote.");
        }
    }

    public static void main(String[] args) {
        try {
            checkAge(16);
        } catch (AgeNotValidException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

```

## Checked vs Unchecked Custom Exceptions

```
// Checked Custom Exception (must be handled)
class MyCheckedException extends Exception {
    public MyCheckedException(String msg) {
        super(msg);
    }
}

// Unchecked Custom Exception (optional to handle)
class MyUncheckedException extends RuntimeException {
    public MyUncheckedException(String msg) {
        super(msg);
    }
}

public class ExceptionTest {

    // Method that throws checked exception
    public static void throwChecked() throws MyCheckedException {
        throw new MyCheckedException("This is a CHECKED exception");
    }

    // Method that throws unchecked exception
    public static void throwUnchecked() {
        throw new MyUncheckedException("This is an UNCHECKED exception");
    }

    public static void main(String[] args) {
        // ✅ Checked Exception must be caught or declared
        try {
            throwChecked();
        } catch (MyCheckedException e) {
            System.out.println("Caught Checked: " + e.getMessage());
        }

        // ❌ Unchecked Exception is optional to catch
        try {
            throwUnchecked();
        } catch (MyUncheckedException e) {
            System.out.println("Caught Unchecked: " + e.getMessage());
        }

        System.out.println("Program continued after exceptions");
    }
}

```

---
THE QUESTION WHY DON'T USE IF ELSE INSTEAD OF EXCEPTION

| Feature                     | Using `if-else` + print | Using Exception Handling |
| --------------------------- | ----------------------- | ------------------------ |
| Good for small programs     | ✅                       | ❌ Overhead               |
| Scales for large programs   | ❌                       | ✅                        |
| Reusable error handling     | ❌                       | ✅                        |
| Cleaner separation of logic | ❌                       | ✅                        |
| Supports custom error types | ❌                       | ✅                        |
| Can stop invalid flow early | ❌                       | ✅                        |