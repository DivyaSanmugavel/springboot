#### **What are Methods?**
A method in Java is a block of code that performs a specific task and only runs when it is called.
- Methods are reusable blocks of code that perform specific tasks.
- They allow **modularity**, **reusability**, and better code organization.
- A method can be declared once and called multiple times, reducing code duplication.
### **Where Can Methods Be Used?**
**Methods are the foundation of any code in Java** because they are the primary way to structure behavior in a program. Almost every piece of logic or functionality in Java is written inside a method

### **. Why Are Methods Essential in Java?**

- In Java, **all executable code must be inside a method.**
- Even the entry point of a Java application, `public static void main(String[] args)`, is a method.
- Methods act as containers for logic, making it easier to organize, reuse, and maintain code.
###  **Benefits of Using Methods**

- **Reusability**: Write once, use many times.
- **Modularity**: Break down large programs into smaller, manageable parts.
- **Readability**: Easier to read and understand.
- **Testing**: You can test individual methods independently.
- **Maintenance**: Changes can be made to specific methods without affecting the rest of the code.
 access modifire returnType methodName(parameters) {
    // method body
}

## Method Parameters

Methods can have zero or more parameters:

```
void greet() {
    System.out.println("Hello!");
}

void greetWithName(String name) {
    System.out.println("Hello, " + name + "!");
}

```
