
# **Shallow and Deep copy**
## **INT**(**age**)

- This is an `int` (primitive).
    
- `p2.age = p1.age;` makes a **new copy** of the number.
    
- So `p1.age` and `p2.age` are **two independent values**.
- `p2.age` = `24`  `p2.age` is changed independently `p1.age` still `23`
---

**Deep Copy:**
p1.address ──> Address@1111 ("chennai")
p2.address ──> Address@2222 ("newyork")

**Shallow Copy**:
p1.address  -──┐
              └──> Address@1111 ("newyork" after update)
              ------>Address@1111(SAME)
              |
              |            
   p2.address ─-- |

Think of it like this in memory:
### Before:

```
STRING :  p2.name ---> "kani"   (shared with p1)

```

**After:**
```
STRING :
p2.name ---> "mani"   (new reference to new string)
p1.name ---> "kani"   (unchanged)

```

A single reference **can only point to one object (or string) at a time**.
Example

```
String s = "apple";
s = "banana";

```
Now:

- First, `s` pointed to `"apple"`.
    
- Then it was reassigned to `"banana"`.
    
- So now `s` **no longer points to `"apple"`**.
### What happens to `"apple"`?

If **no other reference** is pointing to `"apple"` anymore, then:

✅ It becomes **eligible for Garbage Collection (GC)**.

🚫 But it is **not immediately deleted**. Java's GC decides **when** to clean it up — usually based on memory pressure or timing.

### Example with Diagram

```
String s1 = "hello";
String s2 = s1;       // Both s1 and s2 → "hello"
s2 = "world";         // Now s2 → "world", s1 still → "hello"

```
#### 🔹 Memory After Reassigning `s2`:
`s1 ---> "hello" s2 ---> "world"`

🔸 `"hello"` is still in memory because `s1` points to it.

Now if we do:

`s1 = null;`
#### 🔹 Memory:

`s1 ---> null   s2 ---> "world"`

Now `"hello"` is no longer referenced by **any** variable.

🗑️ **Now it's eligible for garbage collection.**

```
String s1 = "hello";
String s2 = s1;       // s2 now points to same "hello" as s1
s2 = "world";         // s2 now points to "world"

```

➡️ Yes! Both `s1` and `s2` point to the **same memory location** (e.g., `"hello"` in the string pool).  
✅ So at this moment, **yes, both have the same reference address** (like `0x2344` hypothetically).

```
s2 = "world";
```
➡️ Now, `s2` is re-assigned to point to **a different string object** (`"world"`).  
✅ So **they no longer share the same reference**.

```
s1 ------> "hello"    (e.g., 0x2344)
s2 ------> "world"    (e.g., 0x2488)
```

Both `"hello"` and `"world"` are still in the **string pool**. for s2
No! Even if no variable points to `"hello"`, it **still stays in the string pool**.

The **string pool is managed differently** from normal heap memory.  
➡️ String literals are **interned** — meaning Java keeps them around to optimize memory use.

> Does `"hello"` still exist in the string pool after `s2` is changed?

### ✅ YES — `"hello"` is **still in the string pool**.

#### Why?

In Java, **string literals** like `"hello"` and `"world"` are automatically placed in the **String Pool**, which is a special memory area inside the Heap used to store **reusable immutable strings**.

```
Step 1:
s1 ---> "hello"   (e.g., address 0x2344)
s2 ---> "hello"   (same address as s1)

Step 2 (after s2 = "world")://when new data the refrence will be different
s1 ---> "hello"   (still 0x2344)
s2 ---> "world"   (now points to new address, e.g., 0x2488)

```

## **STRING** (Immutable String literals)
String name = p1.name;
Even though String is an obj

ect, it’s:

Immutable in Java.

Shared references are safe because you can’t modify the content of a string object — any modification creates a new string in memory.

So reusing p1.name is completely safe!

➡ You don’t need to create a new string object explicitly, unless you specifically want to (like using new String(p1.name) which is rare and unnecessary).

---

## **ADDRESS** (mutable Object)

“**An address object will share the same memory unless we create a new object using `new` keyword. Until then, updates will affect both references.**”

why?
In Java, **non-primitive types** like `Address`, `Person`, etc., are **objects**.  
When you assign one object reference to another, **both references point to the same memory** unless a **new object is created**.

DEEP COPY:
new Address(p1.address.city)
- `p1.address.city` and `p2.address.city` now point to **different objects in memory**.
    
- Modifying `p2.address.city = "New York"` won’t affect `p1`

No, you **do not need to explicitly copy** `p1.name` and `p1.age`.

Person p2 = new Person(p1.name, p1.age, new Address(p1.address.city));

Only the `Address` part (which is a mutable object) needs deep copying.

---
## CODE FOR ABOVE EXPLANATION

```
package Cloning;  
class Address{  
    String city;  
    Address(String city)  
    {  
        this.city=city;  
    }  
}  
class Person{  
    String name;  
    int age;  
    Address address;  
    Person(String name,int age,Address address)  
    {  
        this.name=name;  
        this.age=age;  
        this.address=address;  
    }  
}  
public class Cloningss {  
    public static void main(String[] args) {  
  
         Address address=new Address("delhi");  
//         System.out.println( address.city);  
  
        Person p1=new Person("kumar",22,new Address(address.city));  
        p1.address.city="chennai";  
        p1.name="kani";                                               //p1 42353@-->address  
                                                                       //p2 ''   -->address        p1.age=23;  
         Person p2=new Person(p1.name,p1.age,new Address(p1.address.city));  
  
         p2.age=24;  
         p2.name="mani";  
         p2.address.city="newyork";  
  
        System.out.println("person 1: "+p1.name+" "+p1.age+" "+p1.address.city);  
        System.out.println("person 2: "+ p2.address.city+" " +p2.age+" "+p2.name);  
  
        System.out.println( address.city);  
  
    }  
}
```

“Don’t copy the whole address object — just take the `city` value from it, and create a new Address.”

CLONING USING COPY CONSTRUCTOR:
## What is a Copy Constructor?

A **copy constructor** is a special constructor used to **create a new object by copying values from another object** of the same class.
### **example** using **copy constructors** for both `Address` and `Person` classes

```
class Address {
    String city;

    // Regular constructor
    public Address(String city) {
        this.city = city;
    }

    // ✅ Copy constructor
    public Address(Address other) {
        this.city = other.city;
    }
}
class Person {
    String name;
    int age;
    Address address;

    // Regular constructor
    public Person(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    // ✅ Copy constructor (deep copy)
    public Person(Person other) {
        this.name = other.name;           // Copy value (String is immutable)
        this.age = other.age;             // Copy primitive
        this.address = new Address(other.address); // Deep copy using Address's copy constructor
    }
}
public class Main {
    public static void main(String[] args) {
        Address addr1 = new Address("Madurai");
        Person p1 = new Person("Kumar", 22, addr1);

        // ✅ Deep copy using copy constructor
        Person p2 = new Person(p1);

        // Change p1's data
        p1.name = "Kani";
        p1.age = 23;
        p1.address.city = "Chennai";

        // Print to verify deep copy
        System.out.println("p1: " + p1.name + ", " + p1.age + ", " + p1.address.city);
        System.out.println("p2: " + p2.name + ", " + p2.age + ", " + p2.address.city);
    }
}
p1: Kani, 23, Chennai
p2: Kumar, 22, Madurai


```

### When to Use Copy Constructor?

- To **clone** an object with the same data.
    
- When you want a new object with the same values but a different reference.
---
