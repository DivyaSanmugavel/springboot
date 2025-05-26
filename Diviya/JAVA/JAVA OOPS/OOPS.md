
### **ENCAPSULATION:**
---
Restrict the unauthorized usage of attributes
**Encapsulation** is the process of **wrapping data (variables)** and **methods (functions)** that operate on the data into a single unit (class).

1. **Private Access Modifier**
- Fields (variables) are marked as `private` to **restrict direct access**.
- Prevents other classes from changing the data directly.

*2.***Public Getters and Setters**
- Public methods are provided to **read (getters)** and **modify (setters)** the private fields
3. **Data Hiding**
- Internal object details are hidden from the outside world.
- Only necessary information is exposed.
#### Example bank Transactions
```
public class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            System.out.println("Invalid deposit amount!");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Invalid withdrawal attempt!");
        }
    }
}
public class Main {
    public static void main(String[] args) {
    BankAccount account = new BankAccount();
        bank.deposit(5000); 

```

#### Password Example
```
public class User {
    private String password;

    public void setPassword(String pwd) {
        if (pwd.length() >= 8) {
            this.password = pwd;
        } else {
            System.out.println("Password must be at least 8 characters");
        }
    }

    public String getPassword() {
        return "********"; // hiding actual password
    }
}

```
- You **still protect the field** with `private`.
    
- But you **control how it's accessed and modified** using methods.
    
- You can apply **rules**, **validation**, or **custom formatting**.
    
- You **hide internal logic** (how it’s stored or validated).
    
1. **cannot access the attributes and methods from some other class object.
This is what encapsulation really means** — not just restriction, but **controlled, safe access**.
---

### **INHERITENCE**:
**Inheritance** is a mechanism where one class **inherits** the properties (fields) and behaviors (methods) of another class. It promotes **code reusability** and **method overriding**.
The child **inherits** everything from the parent (even if child adds nothing extra).
### Terminologies

| Superclass / Parent class | The class being inherited from                  |
| ------------------------- | ----------------------------------------------- |
| Subclass / Child class    | The class that inherits the superclass          |
| extends keyword           | Used to inherit a class                         |
| IS-A relationship         | Shows that one class is a type of another class |
| super keyword             | Used to refer to immediate parent class         |

### ==**IS A & HAS A== ==RELATIONSHIP==**
## **What is an IS-A** relationship?

"****Is this thing a type of that thing?**"
### Real-life Example:

- A **Dog** is an **Animal** 
    
- A **Car** is a **Vehicle** 
EXAMPLE:
```
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}
```

- `Dog extends Animal` → Dog **is an** Animal
    
-  This is an **IS-A** relationship
    
- It uses `extends` or `implements`
## What is a **HAS-A** relationship?

*"**Does this thing have that thing?**"*
### Real-life Example:

- A **Car** has an **Engine** 
    
- A **Student** has a **Book** 
```
class Engine {
    void start() {
        System.out.println("Engine started");
    }
}

class Car {
    Engine engine = new Engine();  // Car HAS-A Engine

    void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}

```
- Car **has an** Engine object
    
- This is a **HAS-A** relationship
    
- It uses **object creation**, not `extends`
## Simple Summary:

|Feature|IS-A|HAS-A|
|---|---|---|
|Means|One is a type of another|One has something inside|
|Keyword|`extends` or `implements`|Uses **object reference**|
|Example|`Dog is-an Animal`|`Car has-an Engine`|
|Use case|Inheritance (code reuse)|Composition (build complex objects)|
|Object created?|❌ Not required (uses parent methods)|✅ Required (uses other objects)|
## Fill in the blanks

**Q1:**  
If a class **inherits** another class using `extends`, it is an---------------- __________ relationship.

**Q2:**  
If a class contains **an object of another class**, it is a---------------- __________ relationship.

## Types of Inheritance in Java

|Type|Description|Supported in Java?|
|---|---|---|
|**Single**|One subclass inherits one superclass|✅ Yes|
|**Multilevel**|Class inherits from subclass of another|✅ Yes|
|**Hierarchical**|Multiple classes inherit one superclass|✅ Yes|
|**Multiple**|One class inherits from many classes|❌ Not directly|
|**Hybrid**|Combination of 2+ types|❌ Not directly|
1. **Single Inheritance**
```
class A {
   A()
   {
  System.out.println("parent called by default");
   }
    String name="alpha";
    void show() {
        System.out.println("Hello from A");
    }
}
class B extends A {
B()
{
System.out.println("child cons called after the parent");
}
    void display() {
        System.out.println("Hello from B"+ name);//----->can use variable directly from super class
    }
}

```

CONSTRUCTOR IN INHERTENCE:
- When you create a `Child` object using `new Child()`, the **constructor chain is followed**.
    
- The **parent class constructor is always called first**, even if it's not explicitly written using `super()`, because Java automatically inserts `super()` in the first line of the child constructor.
    
- Then the child class constructor is executed.
---
2.  **Multilevel** **Inheritance***
```
class A {
    void methodA() {}
}
class B extends A {
    void methodB() {emethodA()//can call method directly
    }
}
class C extends B {
    void methodC() {}
}

```

3. **Hierarchical Inheritance**
``` 
class Parent {
    void show() {}
}
class Child1 extends Parent {
    void child1Method() {}
}
class Child2 extends Parent {
    void child2Method() {}
}

```
**Java doesn't support Multiple Inheritance (using classes)**
To avoid **ambiguity** like the _Diamond Problem_. Java allows multiple inheritance using **interfaces**.
### Example using interfaces:

```
interface A {
    void show();
}

interface B {
    void display();
}

class C implements A, B {
    public void show() {}
    public void display() {}
}

```
## `super` Keyword in Inheritance

- **Access parent class constructor**
    
- **Access parent class method or variable**
```
class A {
    int x = 10;
    void show() {
        System.out.println("From A");
    }
}

class B extends A {
    int x = 20;
    void display() {
        System.out.println(super.x);  // Access A's x
        super.show();                // Call A's show()
    }
}

```

| Situation                                 | Need `super`? | Why                         |
| ----------------------------------------- | ------------- | --------------------------- |
| Same **variable** in parent and child     | ✅ Yes         | To access parent’s variable |
| Same **method** in parent and child       | ✅ Yes         | To call parent’s method     |
| Reusing **parent constructor**            | ✅ Yes         | To call parent constructor  |
| Just reusing methods/vars (no name clash) | ❌ No          | You can use them directly   |
- ****Cannot be used in Static Context:**** We cannot use super in a static variable, static method and static block.

---
### **POLYMORPHISM**:

**In Java, method overloading lets you define multiple methods with the same name but different parameter lists, and this applies both within a single class and in subclasses that inherit methods from a superclass.¹⁰⁰¹⁷⁰⁸ Overloaded methods in a subclass are new methods—they neither hide nor override the inherited methods.⁰⁰¹ On the other hand, method overriding requires an exact match in method signature and return type and enables run‑time polymorphism**
## **Compile-Time Polymorphism (Static Binding):**

- **Method Resolution:** Determined during compilation. The compiler selects the appropriate method to invoke based on the method signature and the reference type.​
    
- **Achieved Through:** Method overloading, where multiple methods in the same class share the same name but differ in parameters (number, type, or order).​
    
- **Compiler Checks:** At compile time, the compiler verifies that the method signatures match the method calls, ensuring that the correct method can be invoked based on the reference type.
## Method Overriding in Inheritance

When a subclass provides its own version of a method from the parent class.
```
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}

```

**Key Points:**

- A subclass object includes all accessible methods and fields from its superclass.​
    
- The reference type determines which methods are accessible at compile time.​
    
- The actual object type determines which method implementations are executed at runtime, especially in the case of overridden methods.



### Access Control in Inheritance:

| Modifier  | Same Class | Subclass (Same Package) | Subclass (Different Package) | Other Class |
| --------- | ---------- | ----------------------- | ---------------------------- | ----------- |
| public    | ✅          | ✅                       | ✅                            | ✅           |
| protected | ✅          | ✅                       | ✅                            | ❌           |
| default   | ✅          | ✅                       | ❌                            | ❌           |
| private   | ✅          | ❌                       | ❌                            | ❌           |

---

### **THIS AND SUPER KEYWORDS**
#### `This`
#### 1. **To refer to current class variables**

When **local variable** and **instance variable** have the same name, use `this` to avoid
### 2. To call current class method
### 3. To pass the current object
### 4. To call another constructor in the same class
#### `super`
`super` refers to the **parent (super) class**.
#### 1. **To access parent class variable**
#### 2.**To call parent class method**
### 3.**To call parent class constructor**

|Keyword|Refers to|Used For|
|---|---|---|
|`this`|Current class object|Access current variables/methods|
|`super`|Parent class object|Access parent variables/methods/constructor|

## Benefits of Inheritance

- Code Reusability
    
- Polymorphism support
    
- Easy to manage code structure
    
- Overriding functionality
    
- Promotes hierarchy
## Disadvantages

- Tight coupling between classes
    
- Increases runtime complexity if misused
    
- Harder to maintain in deep inheritance chains
---

### ==Upcasting and Downcasting:==
### **Upcasting (Subclass Object → Superclass Reference)**

**What It Is:**  
Upcasting is the process of treating a subclass object as an instance of its superclass. This is done automatically (implicitly) because every subclass object "is a" superclass object
**Why Use It:**

- **Polymorphism:** It allows you to write more general and reusable code. For example, you can write methods that accept the superclass type and work with any subclass.
    
- **Safety:** Since the subclass always contains all the properties of its superclass, upcasting is safe and does not require explicit casting.
- 🚗 Parent Class: `Transport`
- Represents a general category — bike, car, bus, etc., all fall under this.

```
class Transport {
    String fuelType = "Petrol";

    void move() {
        System.out.println("Transport is moving...");
    }
}

```
🛵 Child Class: `Bike`
```
class Bike extends Transport {
    void kickStart() {
        System.out.println("Bike started with a kick.");
    }
}

```

🚙 Child Class: `Car`
```
class Car extends Transport {
    void startWithKey() {
        System.out.println("Car started with a key.");
    }
}

```
🎯 Upcasting: Treat all specific vehicles as general `Transpor`
```
public class Main {
    public static void main(String[] args) {
        Transport t1 = new Bike();  // Upcasting
        Transport t2 = new Car();   // Upcasting

        t1.move();                 // ✅ Allowed (from Transport)
        System.out.println(t1.fuelType); // ✅ Allowed (from Transport)

        // t1.kickStart();         // ❌ Not allowed (specific to Bike)
        // t2.startWithKey();      // ❌ Not allowed (specific to Car)
    }
}

```
Explanation in Words
> **ransport** is a **general category**, just like a base class. Actual vehicles like `Bike` or `Car` inherit common behavior (like `move()` or `fuelType`) from `Transport`.

When you **upcast**, for example:

Transport t = new Bike();  // Upcasting

- The object is still a `Bike`, but you're **viewing it as a general Transport**.
    
- So you can only access what all transports have in common — like `move()` and `fuelType`.
    
- You **cannot access specific features** like `kickStart()` unless you downcast.

## Final Version of What You Tried to Say:

> “Transport” is a general category, while vehicles like `Bike` and `Car` are specific types. These specific vehicles inherit common attributes and methods from the parent `Transport` class. When we use upcasting (e.g., `Transport t = new Bike()`), we can only access the **common things** defined in the `Transport` class. The unique features of `Bike` or `Car` remain **hidden** unless we downcast — this helps developers **focus only on shared behavior** when it’s not necessary to know the specific type.

when an object of a subclass is created, and a method is overridden in that subclass, the overridden method in the subclass is called at runtime, even if the reference to the object is of the superclass type. This behavior is due to **runtime polymorphism**, also known as **dynamic method dispatch**

**How It Works:**

- **Method Overriding:** Occurs when a subclass provides a specific implementation for a method that is already defined in its superclass.​
    
- **Reference Type vs. Object Type:** While the reference variable might be of the superclass type, the actual object can be of the subclass type.​
    
- **Method Invocation:** At runtime, Java determines the actual type of the object and invokes the corresponding overridden method in the subclass.​
    

**Example:**

```
class Transport {
    void move() {
        System.out.println("Transport is moving...");
    }
}

class Bike extends Transport {
    @Override
    void move() {
        System.out.println("Bike is moving...");
    }
}

public class Test {
    public static void main(String[] args) {
        Transport myTransport = new Bike(); // Upcasting
        myTransport.move(); // Outputs: Bike is moving...
    }
}

```



In this example:

1. A `Bike` object is created and assigned to a `Transport` reference (`myTransport`).​
    
2. The `move()` method is called on `myTransport`.​
    
3. At runtime, Java determines that `myTransport` refers to a `Bike` object and invokes the `move()` method defined in the `Bike` class.​
    

**Key Points:**

- **Dynamic Method Dispatch:** This mechanism allows Java to invoke the correct method implementation at runtime based on the actual object type, enabling flexibility and extensibility in code.​
    
- **Polymorphism:** Method overriding facilitates polymorphism, allowing a superclass reference to point to subclass objects and invoke the appropriate overridden methods.​
    
- **Compile-Time vs. Runtime Behavior:** While the compiler checks for method existence and accessibility based on the reference type, the actual method that gets executed is determined at runtime based on the object's type.
> ---
>
### **DOWNCASTING**
**downcasting** refers to the process of converting a reference of a superclass type back to a reference of its subclass type. This is typically done when you have an object that was upcasted earlier and you need to access subclass-specific methods or attributes that are not available through the superclass reference.​
**Key Points:**

- **Explicit Casting Required:** Unlike upcasting (which is implicit), downcasting requires explicit casting using parentheses
    
- **Risk of `ClassCastException`:** If the object being downcasted is not actually an instance of the target subclass, a `ClassCastException` will be thrown at runtime.​
    
- **Use of `instanceof` Operator:** To avoid `ClassCastException`, it's common practice to use the `instanceof` operator to check the actual type of the object before performing downcasting.

```
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

public class TestDowncasting {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // Upcasting
        if (myAnimal instanceof Dog) {
            Dog myDog = (Dog) myAnimal; // Downcasting
            myDog.bark(); // Outputs: Dog barks
        } else {
            System.out.println("Downcasting not possible");
        }
    }
}

```

---
## What is **Abstraction** in Java?

> **Abstraction** means **hiding unnecessary details** and showing **only essential features** to the user.
- **Car**: When you drive a car, you only need the **steering, brakes, and accelerator** — you don't need to know how the engine works inside.
    
- That’s **abstraction**: show **only what’s needed**, hide the complexity.
There are **2 ways** to achieve abstraction in Java:

| Way                | How much abstraction? | Example          |
| ------------------ | --------------------- | ---------------- |
| **Abstract class** | Partial abstraction   | `abstract class` |
| **Interface**      | Full abstraction      | `interface`      |
## Abstract Class (Partial Abstraction)

- Can have **abstract methods** (no body) 
    
- Can also have **normal methods** (with body) 
    
- Can have **variables** (fields) 
    
- Can have **constructors** 
    
- Can extend only **one class**
- class must be with abstract keyword
## Interface (Full Abstraction)

In Java, **interfaces can only extend other interfaces**.

- **All methods are abstract by default** (till Java 7).
    
- From Java 8, interfaces can also have:
    
    - **default methods** 
        
    - **static methods** 
        
- No constructors 
    
- **No method body** (except default/static)
    
- Can extend **multiple interfaces** 
-
```
abstract class Vehicle {
    abstract void start();
    void fuel() {
        System.out.println("Add fuel");
    }
}

interface Electric {
    void charge(); // abstract by default
}

class Tesla extends Vehicle implements Electric {
    void start() {
        System.out.println("Start Tesla silently");
    }

    public void charge() {
        System.out.println("Charging battery");
    }
}

```


**Multiple Inheritance Using Interfaces:**

Multiple inheritance with interfaces enables a class to implement more than one interface, thereby inheriting the abstract methods of all the interfaces.
```
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying.");
    }

    @Override
    public void swim() {
        System.out.println("Duck is swimming.");
    }
}

public class TestMultipleInheritance {
    public static void main(String[] args) {
        Duck duck = new Duck();
        duck.fly();   // Outputs: Duck is flying.
        duck.swim();  // Outputs: Duck is swimming.
    }
}

```
**Hybrid Inheritance Using Interfaces:**

Hybrid inheritance is a combination of two or more types of inheritance. In Java, this can be achieved by combining class inheritance (single inheritance) and interface implementation (multiple inheritance).
```
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

interface Canine {
    void bark();
}

interface Feline {
    void meow();
}

class Dog extends Animal implements Canine {
    @Override
    public void bark() {
        System.out.println("Dog barks.");
    }
}

class Cat extends Animal implements Feline {
    @Override
    public void meow() {
        System.out.println("Cat meows.");
    }
}

public class TestHybridInheritance {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();   // Inherited from Animal class
        dog.bark();  // Implemented from Canine interface

        Cat cat = new Cat();
        cat.eat();   // Inherited from Animal class
        cat.meow();  // Implemented from Feline interface
    }
}

```

- `Animal` is a superclass with a method `eat()`.​
    
- `Canine` and `Feline` are interfaces with methods `bark()` and `meow()`, respectively.​
    
- The `Dog` class extends `Animal` and implements `Canine`, inheriting the `eat()` method and implementing the `bark()` method.​
    
- The `Cat` class extends `Animal` and implements `Feline`, inheriting the `eat()` method and implementing the `meow()` method.​
    

This structure combines single inheritance (from the `Animal` class) and multiple inheritance (through interfaces `Canine` and `Feline`), exemplifying hybrid inheritance.

### **situations** **to avoid**
**Conflicting Method Signatures with Different Return Types:**

- If two interfaces declare methods with the same name and parameter list but different return types, a class cannot implement both interfaces simultaneously. This results in a compilation error due to the ambiguity
- ``
```
interface InterfaceA {
    int calculate();
}

interface InterfaceB {
    double calculate();
}

public class MyClass implements InterfaceA, InterfaceB {
    // Compilation error: Duplicate methods with different return types
}

```
**2.Default Method Conflicts:**

- With Java 8 and above, interfaces can have default methods. If a class implements multiple interfaces that contain default methods with the same signature, the compiler will report an error unless the class provides its own implementation to resolve the conflict.
```

```interface InterfaceA {
    default void display() {
        System.out.println("InterfaceA display");
    }
}

interface InterfaceB {
    default void display() {
        System.out.println("InterfaceB display");
    }
}

public class MyClass implements InterfaceA, InterfaceB {
    // Compilation error: display() is ambiguous
}

```
Resolution:
```
public class MyClass implements InterfaceA, InterfaceB {
    @Override
    public void display() {
        // Custom implementation or specify which interface's method to use
        InterfaceA.super.display();
    }
}

```
**Diamond Problem:**

- This occurs when a class inherits from two interfaces that both inherit from a common ancestor interface containing a default method. The implementing class must override the method to avoid ambiguity.
```
interface Parent {
    default void show() {
        System.out.println("Parent show");
    }
}

interface ChildA extends Parent {}

interface ChildB extends Parent {}

public class MyClass implements ChildA, ChildB {
    // Compilation error: show() is ambiguous
}

```
Resolution:
```
public class MyClass implements ChildA, ChildB {
    @Override
    public void show() {
        // Custom implementation or specify which interface's method to use
        ChildA.super.show();
    }
}

```

**Inheriting Conflicting Constants or Fields:**

- If multiple interfaces declare constants or fields with the same name, referencing them in the implementing class without specifying the interface leads to ambiguity.​
    
    _Example:

```
interface InterfaceA {
    int VALUE = 10;
}

interface InterfaceB {
    int VALUE = 20;
}

public class MyClass implements InterfaceA, InterfaceB {
    public void printValue() {
        System.out.println(VALUE); // Compilation error: ambiguous reference
    }
}

```

Resolution:
```
public class MyClass implements InterfaceA, InterfaceB {
    public void printValue() {
        System.out.println(InterfaceA.VALUE); // Specify the interface
    }
}

```

---

### **CONSTRUCTOR:**

### 1. **Constructor Overloading: Gives Flexibility**

Constructor overloading allows you to provide **different ways to create an object** based on available information.

OVERLOADING:
Example of **Constructor Overloading** (Without Chaining):
```
class Student {
    String name;
    int age;

    Student() {
        name = "Default";
        age = 18;
    }

    Student(String name) {
        this.name = name;
        age = 18;
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " - " + age);
    }
}
new Student ();                    // default user
new Student ("Alice");             // only name
new Student ("Alice", 25);         // name + age

```
Here we have **overloaded constructors** — same name (`Student`) but different parameters.

### 2. **Constructor Chaining: Avoids Code Duplication**

Chaining avoids writing the same logic again and again inside every constructor.

#### ❌ Without Chaining:


```
User(String name) {
    this.name = name;
    this.age = 18;
}

User(String name, int age) {
    this.name = name;
    this.age = age;
}

```

You're repeating `this.name = name;` in both places.
### Example of **Constructor Chaining** (With Overloading):

```
class Student {
    String name;
    int age;

    Student() {
        this("Default", 18); // Chaining to 2-arg constructor
    }

    Student(String name) {
        this(name, 18); // Chaining to 2-arg constructor
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    void display() {
        System.out.println(name + " - " + age);
    }
}

```

So instead of repeating code, you **reuse** logic by chaining one constructor to another. It's **cleaner, easier to maintain**, and reduces bugs.

## **What is the use of `this()` in constructor chaining?**

`this()` is used to call another constructor in the **same class**. It helps:

- Centralize object creation logic.
    
- Reduce duplicate code.
    
- Improve maintainability.
    

> ⚠️ `this()` must be the **first statement** in the constructor.

---
#### **Implement** both constructor overloading and chaining

## **Problem**: A user can order pizza in 3 ways:

1. Default order (regular size, cheese topping)
    
2. Choose size only
    
3. Choose size and topping

- Customers can:
    
    - Order a **default pizza** 🍕
        
    - Choose **size** (Small, Regular, Large)
        
    - Choose **size + topping**
        
    - Choose **size + topping + extra cheese**
        

  Each size has a base price:

- Small → ₹150
    
- Regular → ₹200
    
- Large → ₹250  

    Extra cheese costs ₹50 more.

We’ll implement:

- **Overloading** = different ways to order
    
- **Chaining** = avoid repeating code
	
```
package constructorss;

public class Pizza {
    String size;
    String topping;
    boolean extraCheese;
    int price;

    // Constructor with all options
    Pizza(String size, String topping, boolean extraCheese) {
        this.size = size;
        this.topping = topping;
        this.extraCheese = extraCheese;
        calculatePrice();
    }

    // Constructor: size + topping (no extra cheese)
    Pizza(String size, String topping) {
        this(size, topping, false); // constructor chaining
    }

    // Constructor: only size (defaults topping & no cheese)
    Pizza(String size) {
        this(size, "Cheese", false);
    }

    // Default pizza
    Pizza() {
        this("Regular", "Cheese", false);
    }

    void calculatePrice() {
        switch (size.toLowerCase()) {
            case "small": price = 150; break;
            case "regular": price = 200; break;
            case "large": price = 250; break;
            default: price = 200;
        }

        if (extraCheese) {
            price += 50;
        }
    }

    public void orderSummary() {
        System.out.println("🍕 Your Pizza Order:");
        System.out.println("- Size    : " + size);
        System.out.println("- Topping : " + topping);
        System.out.println("- Extra Cheese: " + (extraCheese ? "Yes" : "No"));
        System.out.println("- Total Price: ₹" + price);
        System.out.println("--------------------------------");
    }

    public static void main(String[] args) {
        Pizza order1 = new Pizza();  // default
        Pizza order2 = new Pizza("Large", "Veggie");  // with topping
        Pizza order3 = new Pizza("Small", "Paneer", true); // with cheese
        Pizza order4 = new Pizza("Regular");  // size only

        order1.orderSummary();
        order2.orderSummary();
        order3.orderSummary();
        order4.orderSummary();
    }
}

```