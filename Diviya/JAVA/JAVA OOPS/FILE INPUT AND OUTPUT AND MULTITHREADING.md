**What is File I/O?**

- **File I/O** means **File Input/Output**.
    
- It is the process of **reading from** or **writing to** files on your computer **using code**.
**In Java**, a **Stream** is basically a **class** (or more correctly, an **abstract class**).
Stream = A way to move data from one place to another.
It’s like **taking data** from a **source** (file, memory, network) and **bringing it** into your **program** OR **sending it** from your program to somewhere else.
Real work is done by **child classes** like `FileInputStream`, `FileReader`, `BufferedReader`, etc.

- **Stream** is **the idea of data flow**.
    
- Then you have **specific classes** to handle **specific types of data**:
    
    - **InputStream/OutputStream** → **bytes**
        
    - **Reader/Writer** → **characters**
        
    - **ObjectInputStream/ObjectOutputStream** → **objects**


             Stream (abstract concept)
                        |
   -------------------------------------------------
   |                                                                      |
Byte Streams (binary)                                     Character Streams (text)
   |                                                                           |
InputStream / OutputStream                          Reader / Writer
   |                                                                            |
FileInputStream / FileOutputStream                    FileReader / FileWriter
ObjectInputStream / ObjectOutputStream


- `InputStream` and `OutputStream` = Deal with **Bytes** (images, audio).
    
- `Reader` and `Writer` = Deal with **Characters** (text).
    
- `ObjectInputStream` and `ObjectOutputStream` = Deal with **Objects** (serialization)
### **1.What is Character Stream?**

- It deals with **characters** (`char` data), **not bytes**.
    
- Used for reading/writing **text files** (like `.txt`).
    
- **Character Stream** understands **Unicode**, so it is good for text (English, Hindi, Chinese, etc.).
### **1.FILE READER**
If you use **FileReader** for **reading**, and the file does NOT exist ➔  it will throw **FileNotFoundException**!

```
try {  
    FileReader fr=new FileReader("demo1.text");  
    BufferedReader br=new BufferedReader(fr);  
    int data;  
    while ((data= br.read())!=-1)  
    {  
        System.out.print((char)data);  
    }  
    fr.close();  
    br.close();  
}  
catch (Exception e)  
{  
    System.out.println(e.getMessage());  
}
```

### **2.FILE WRITER**
- **If file exists** ➔ It **writes** into it.
    
    - If you gave `true` ➔ It **appends** at the end.
        
    - If you did **not** give `true` ➔ It **overwrites** (old content gone).
        
- **If file does NOT exist** ➔ It **automatically creates a new file** and **writes**!
    

 **You don't need to create the file manually when writing!**
```
try {  
            FileWriter fw = new FileWriter("demo1.text",true); // NO append mode (overwrites)  
            BufferedWriter bw = new BufferedWriter(fw);  
            bw.append("oiii");  
//            bw.newLine();  
            bw.write("flowers");  
//            bw.append("fruits");  
//            bw.flush();  
//            bw.write("append");  
//  
//            fw.append(":");  
            bw.close();  
            fw.close();  
            FileReader fr=new FileReader("demo1.text");  
            BufferedReader br=new BufferedReader(fr);  
  
            int data;  
            while ((data= br.read())!=-1)  
            {  
  
                System.out.print((char)data);  
            }  
            fr.close();  
            br.close();  
  
        }  
        catch (Exception e)  
        {  
            System.out.println(e.getMessage());  
        }
```

---

### **2.What is Byte Stream?**

- It deals with **raw bytes** (`byte` data).
    
- Used for reading/writing **binary files** (like images, videos, PDFs).
    
- **Byte Stream** does **not** understand text, only raw data.
- copying a photo file (`.jpg`) or a music file (`.mp3`).

#### **EXAMPLE:**

```
import java.io.FileInputStream;  
import java.io.FileOutputStream;  
  
//copying data from one file to another file  
public class Bytestreams {  
    public static void main(String[] args) {  
try {  
    FileInputStream input = new FileInputStream("image.jpg"); // Read file  
    FileOutputStream output = new FileOutputStream("sea.jpg"); // Write file  
  
    int data;  
    while ((data = input.read()) != -1) {  
         output.write(data); // Write byte by byte  
        System.out.println(data); 
    }  
    input.close();  
    output.close();  
}  
  
catch (Exception e)  
{  
    System.out.println(e.getMessage());  
}  
  
            }  
        }
```

Each byte can store a value between 0 to 255.Numerical values represent the binary data (like images, audio, etc.) as numbers in the range from 0 to 255 
- **0-255**: These numbers represent **colors** in images or **patterns** in a binary file.
    
- In an **image**: Each byte might represent a **color pixel value** in an image.
    
- In a **text file**: These numbers are the ASCII or Unicode values for the characters (like "A" = 65, "B" = 66).
### **`-1` means**:

- There are **no more bytes to read** from the file.
    
- It's a **special value** indicating **end-of-file** (EOF).it's just a **signal** that there are **no more bytes** to read.

---
#### **3.What is Serialization?**

- **Serialization** means **converting a Java object into a stream of bytes**, so that you can:
    
    - Save it into a file
        
    - Send it over a network
        
    - Store it somewhere temporarily
        
- **Deserialization** is the reverse: **converting bytes back into an object**.
Example:

- Suppose you have a `Student` object with name and age.
    
- Serialization will turn that object into bytes and save it into a file.
    
- Later you can **restore** (deserialize) it back to a real `Student` object.

- **FileInputStream**: Reads raw bytes from a file (works with any data type).
    
- **ObjectInputStream**: Converts those raw bytes into a Java object (only works with serialized objects)
#### EXAMPLE:
```
package Opps;  
import java.io.*;  
  
public class Students implements Serializable{  
    String name;int age;  
  Students(String name,int age)  
  {  
      this.name=name;  
      this.age=age;  
  }  
  
public String toString()  
{  
    return name+" "+age;  
}  
  
    public static void main(String[] args) {  
Students stu=new Students("kumar",44);  
  
try{  
    FileOutputStream fi=new FileOutputStream("obj.text");  
    ObjectOutputStream write=new ObjectOutputStream(fi);  
    write.writeObject(stu);  
    write.close();  
  
}  
catch (Exception e)  
{  
    System.out.println(e.getMessage());  
}  
try {  
    FileInputStream fi=new FileInputStream("obj.text");  
    ObjectInputStream read=new ObjectInputStream(fi);  
//    Students stu1=(Students) read.readObject();  
    System.out.println(read.readObject());  
    read.close();  
}  
catch (Exception e)  
{  
    System.out.println(e.getMessage());  
}  
    }  
}
```

### `implements Serializable`

- Without `Serializable`, **Java doesn’t know** how to save the object to a file.
    
- `Serializable` is just a **marker interface** (no methods inside).
    
- It tells Java:
    
    > "This class can be safely converted into a stream of bytes."
    

**Without it → `NotSerializableException` error happens**

### `FileOutputStream`

- This **opens a file** to write _binary_ data.
    
- If the file (`obj.text`) does not exist, it **creates** it.
### `write.writeObject(stu);`

- Saves the **whole object** (Student: kumar, 44) into the file.
    
- Converts object → byte stream → writes into `obj.text`.

---

### (6) `ObjectOutputStream`

- **Wraps** the FileOutputStream.
    
- Gives you **easy methods** like `.writeObject(object)` to directly serialize any object.

**Students stu1=(Students) read.readObject();** 

- `readObject()` returns type `Object`
    
- `Object` is a **superclass** of all Java classes
    
- Java is **statically typed**, so it **does not allow automatic downcasting**

### **Serialization** means:  
**Converting a Java object into a sequence of bytes**  
**Saving that bytes into a file, network, or database**

**Why?**  
Because Java objects exist only **inside RAM** (memory).  
If you want to **store** them permanently (disk, send to another computer, etc.),  
you need to **convert** them into a format that can be saved — that's **Serialization**!

Real Life Example
Suppose you have this Java object in memory:
```
Students s = new Students("Kumar", 44);

Students object
┌─────────────┐
│ name = Kumar│
│ age = 44    │
└─────────────┘
```
But **memory is temporary**!  
If you turn off your computer ➔ it disappears!

So you **Serialize** it ➔ convert to bytes ➔ save to file like `obj.text`.

Bytes might look like:
```
1011010110100110110101101010.... (binary data)
```
This binary data can now be:

- Stored permanently in a file
    
- Sent over the internet
    
- Saved in a database
    
- Loaded back later

---

## BufferedReader and BufferedWriter

They are **normal Java classes** (not abstract, not interface).  
You can **create objects** of them.
Both are inside the **`java.io`** package.

```
import java.io.BufferedReader;
import java.io.BufferedWriter;

```

**Important:**

- Both can **throw `IOException`**, so **you must use try-catch or throw** exception.

|Name|Meaning|
|---|---|
|BufferedReader|**Reads** text **faster** from a source (like a file)|
|BufferedWriter|**Writes** text **faster** to a destination (like a file)|

**"Buffered"** means **they use a temporary memory (buffer)** to make reading/writing **faster**.

When you use **FileReader** or **FileWriter**:

- It reads/writes **one character at a time** → **slow**.
    

When you use **BufferedReader** or **BufferedWriter**:

- It reads/writes **many characters at once** (using a buffer) → **fast**.
    
- `BufferedReader` reads **line by line** (not one character by one character).
    
- It is **faster** and **easier** to work with.

- `BufferedWriter` **writes big chunks** of text at once.
    
- **newLine()** method adds a line break easily.

**Buffer** = small temporary memory in RAM

- ***only for character stream not use in bytestream.**


| Method       | Definition                                                 | FileReader/Writer                      | BufferedReader/Writer |
| ------------ | ---------------------------------------------------------- | -------------------------------------- | --------------------- |
| `read()`     | Reads one character at a time (returns int)                | Both                                   | Both                  |
| `readLine()` | Reads one full line as a String                            | Not                                    | Only                  |
| `write()`    | Writes a character, char array, or string                  | Both                                   | Both                  |
| `newLine()`  | Writes a platform-specific newline (`\n` or `\r\n`)        | Not                                    | Only                  |
| `flush()`    | Forces all buffered data to be written immediately         | Not                                    | Only                  |
| `close()`    | Closes the stream and releases resources                   | Both                                   | Both                  |
| `append()`   | Adds content to the end of the file instead of overwriting | Only in `FileWriter` (via constructor) | Depends on FileWriter |
### Important Notes:

- `FileWriter` **controls** the append behavior using this constructor:
```
new FileWriter("file.txt", true); // true = append mode

```

- `BufferedWriter` **does not** have its own `append` mode — it **depends** on the `FileWriter` you give it.
    
- `BufferedWriter` **has** an `append()` method (inherited from Writer class), but **whether it truly appends** depends on **how you created FileWriter**.

Suppose `"demo.txt"` already has:
```
Hello World
```
You run this:
**`FileWriter` itself does not have an "append" mode by default**.

- When you create a `FileWriter` using `new FileWriter("demo.txt")`, it **does not append**, and it will **overwrite** the file.

### **So, to enable append mode in `FileWriter`**, you need to pass `true` as the second argument:
```
FileWriter fw = new FileWriter("demo.txt", true);//this won't over
fw.write("New Line");
fw.close();

```
Result inside file:
```
Hello WorldNew Line
(it adds at the end without deleting "Hello World").**If file is already created and you want to append, you MUST pass `true`**.
```
---

### APPEND AND WRITE

- `append()` _intention_ is to **add** data.
    
- `write()` _intention_ is to **write** data (either overwrite or append based on mode).
    
- **In real file behavior**, **both are same** depending on `true` (append mode) or **default** (overwrite mode).
### FLUSH()
| Program Line | Code              | What happens internally                                                         |
| ------------ | ----------------- | ------------------------------------------------------------------------------- |
| 1            | `write("Hello")`  | "Hello" stored in memory (buffer)                                               |
| 2            | `write("World")`  | "World" added to memory (buffer)                                                |
| 3            | `flush()`         | All memory content ("HelloWorld") **immediately written** into file             |
| 4            | `write("hi")`     | "hi" stored again in memory (new buffer data)                                   |
| 5            | `write("helloo")` | "helloo" also stored in memory                                                  |
| 6            | `close()`         | `flush()` happens automatically → remaining "hihelloo" is **written into file** |

When you write without flushing:

- Data is **executed** but **kept inside memory**.
    
- Not yet saved into the file.
    

 When you `flush()`:

- **Push** all waiting data **immediately** into the file.
---
### **MULTITHRADING**

### What is a Thread?

A **thread** is a small part of a program that runs **independently**. Every Java program has at least one thread — the **main thread**.

Think of a thread as a **worker** that does one task.

```
public class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }

    public static void main(String[] args) {
        MyThread t = new MyThread(); // create thread
        t.start(); // start thread
    }
}
```

### What is Multithreading in Java?

**Multithreading** means running **multiple threads at the same time**. It helps your program do **many tasks together**.

**Multithreading** is the process of running **two or more threads simultaneously** within a single program to perform **multiple tasks at the same time**
Multithreading allows a program to perform **multiple operations independently and concurrently**.
Example: You are watching a video (main task) and downloading a file (background thread) at the same time.

#### Example:

- One thread plays music.
    
- Another thread downloads a file.
    
- Another thread shows a timer.
    

All run **at the same time**, making the app faster and smoother.
    

Without multithreading, all tasks would happen **one after another** (sequentially). With multithreading, you can:

- Download the data in one thread
    
- Animate the loading in another
    
- Keep the UI responsive in the main thread
You can create threads in Java using:

1. `extends Thread`
    
2. `implements Runnable`
    
3. `ExecutorService` (modern approach)

| Concept                                                                 | Purpose                                          |
| ----------------------------------------------------------------------- | ------------------------------------------------ |
| `Runnable`                                                              | Represents a task to run in a thread             |
| `run()` method                                                          | Defines what the thread will do                  |
| `Thread` object                                                         | Represents a thread of execution                 |
| `start()` method                                                        | Starts the new thread and runs `run()` inside it |

| Concept                  | Simple Explanation                                                                              |
| ------------------------ | ----------------------------------------------------------------------------------------------- |
| **Thread class**         | A built-in class in Java used to create threads.                                                |
| **Runnable interface**   | An interface that helps create threads by implementing the `run()` method.                      |
| **run()**                | Code inside this method runs in the new thread.                                                 |
| **start()**              | Starts the thread and runs the `run()` method in a new thread (not immediately, but scheduled). |
| **sleep(ms)**            | Pauses the thread for some milliseconds.                                                        |
| **join()**               | Tells one thread to wait for another to finish before continuing.                               |
| **isAlive()**            | Checks if the thread is still running.                                                          |
| **getName(), setName()** | Get or change the thread’s name.                                                                |
| **Thread priority**      | Controls which thread gets more attention from the CPU. (not always reliable)                   |

the `start()` method is defined in the `Thread` class in Java.

Multithreading in Java is built around two main interfaces/classes:

- `java.lang.Thread`
    
- `java.lang.Runnable` (functional interface)

You can create threads by:

- **Extending `Thread` class** and overriding `run()`
    
- **Implementing `Runnable`** and passing it to a `Thread` object
A **thread** is a small, independent unit of a program that can run **at the same time** as other threads

**Why Do We Need `Runnable` to Implement Threads?**
1. Java Doesn't Support Multiple Inheritance
2. If you extend `Thread`, you **can't extend any other class**:
```
class MyThread extends Thread {
    // Now you can't extend any other class
}
```

But if you use `Runnable`, you’re free to extend another class:

```
class MyTask extends SomeOtherClass implements Runnable {
    public void run() {
        System.out.println("Running task...");
    }
}

```
More flexible.

---
### **What is Synchronization?**

**Synchronization** is a technique used in Java to **control access to shared resources** by multiple threads.

Imagine two people trying to write on the same whiteboard at the same time. Without rules, their messages may overwrite each other. Synchronization acts like a rule that allows **only one person at a time** to use the whiteboard — avoiding confusion and data loss.

### Why Do We Need It?

When multiple threads **read and write** to the **same variable or object**, there's a risk of:

- **Data inconsistency**
    
- **Race conditions** (two threads changing the value at the same time, leading to unpredictable results)
    

Synchronization **prevents these problems** by making sure only one thread can access the critical section at a time.

```
class Counter {  
    private int count = 0;  
  
    public synchronized void increment() {  
        count++;  
    }  
  
    public int getCount()  
    {  
        return count;  
    }  
}  
  
class CounterTask implements Runnable  
{  
    private Counter counter;  
  
    public CounterTask(Counter counter)  
    {  
        this.counter = counter;  
    }  
  
    @Override  
    public void run() {  
        for (int i = 0; i < 1000; i++)  
        {  
            counter.increment(); // Increment the shared counter  
        }  
    }  
}  
  
public class SynchronizationExample {  
    public static void main(String[] args) {  
        Counter counter = new Counter(); // Shared resource  
  
        Thread thread1 = new Thread(new CounterTask(counter));  
        Thread thread2 = new Thread(new CounterTask(counter));  
  
        // Start threads  
        thread1.start();  
        thread2.start();  
  
        // Wait for threads to finish  
        try {  
            thread1.join();  
            thread2.join();  
        } catch (InterruptedException e) {  
            e.printStackTrace();  
        }  
  
        // Print the final count  
        System.out.println("Final Count: " + counter.getCount());  
    }  
}
```

The **`join()` method** is used to make **one thread wait for the completion of another**.
When you call `thread.join()`, the **current thread (main thread)** will pause and **wait for that thread to finish its execution** before continuing.
1. You start both threads (`thread1` and `thread2`) — they begin running in **parallel**.
    
2. Without `join()`, the `main` thread **won’t wait** for them to finish. So it might print the final count **before** the threads are done updating it!
    
3. With `join()`, the `main` thread **pauses** at each `join()` call:
    
    - Waits for `thread1` to finish
        
    - Then waits for `thread2` to finish
        
    - Only then prints the final count
    
**(IMPORTANT NOTICE)**
This **starts two separate threads**, which run **concurrently** (i.e., _multithreading is achieved_).

These threads **both increment the shared `Counter` object**. So:

- ✅ **Yes, multithreading is achieved.**
    
- ✅ The threads **run in parallel**.
    
- ❌ `synchronized` doesn’t stop multithreading — it just **controls access** to shared resources **one thread at a time**.
---
## **Simple Java Multithreading Task: Traffic Signal Simulation**

### **What is the task?**

You are building a small program that **simulates a traffic signal system** (like the one at road intersections).

There are 3 lights:

- **Red** → Wait for 3 seconds
    
- **Green** → Wait for 2 seconds
    
- **Yellow** → Wait for 1 second
    

Each light turns ON one after another.

You have to **repeat this process for 3 cycles**.

We will use **multithreading** to simulate each signal as a separate task.

```
Cycle 1:
Red Signal ON
(wait 3 seconds)
Green Signal ON
(wait 2 seconds)
Yellow Signal ON
(wait 1 second)

Cycle 2:
Red Signal ON
(wait 3 seconds)
Green Signal ON
(wait 2 seconds)
Yellow Signal ON
(wait 1 second)

Cycle 3:
Red Signal ON
(wait 3 seconds)
Green Signal ON
(wait 2 seconds)
Yellow Signal ON
(wait 1 second)

```

> The output will be printed slowly due to `Thread.sleep()` delays — like a real signal changing one after another.