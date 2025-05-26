# Spring Framework
---

## 1. What is Spring?

**Spring** is a powerful, lightweight framework for Java. It simplifies Java development by providing comprehensive infrastructure support for developing Java applications. Spring allows developers to build robust, maintainable, and scalable enterprise applications.

**Who Founded Spring?**

The Spring Framework was created by Rod Johnson. He released the first version along with his book, "Expert One-on-One J2EE Design and Development," in 2003.

---
## What Is the Need for Spring?

Before Spring, Java Enterprise Edition (JEE) development was complex, heavy, and difficult to maintain. Developers had to deal with:
- Complex configurations (especially with EJBs)
- Tight coupling between components(- If you create an object of one class directly inside another class using `new`, the two classes are tightly coupled.)
- Difficult unit testing(****Unit testing**** is the process of testing the smallest parts of your code)
- Boilerplate code for transactions, security, and database access

**Spring was developed to solve these problems:**
- It simplifies Java application development by using dependency injection and aspect-oriented programming.
- It avoids heavy, container-dependent EJBs.
- It promotes loose coupling, easier testing, and better modularity.
- It provides a consistent way to manage business objects and their dependencies.

---

## What Does Spring Alone Contain?

The core Spring Framework provides:

### 1. **Inversion of Control (IoC) Container**
   - Manages the lifecycle and configuration of application objects (beans).
   - Supports Dependency Injection for loose coupling.

### 2. **Aspect-Oriented Programming (AOP)**
	 
- **AOP** is a way to **add extra behavior (like logging, security, or transaction management)** to your code **without changing the original code**.
> **AOP (Aspect-Oriented Programming)** means writing repeated/common code (like logging, login checking, etc.) in a **separate file (aspect class)** and letting Spring automatically call it **whenever and wherever it's needed**, without you writing it again and again."
### 3. **Data Access Integration**
   - Simplifies database operations using JDBC templates.
   - Integrates with popular ORM frameworks (Hibernate, JPA).

### 4. **Transaction Management**
   - Provides a consistent programming model for transaction management across different resources.

### 5. **Model-View-Controller (MVC) Web Framework**
   - Simplifies web application development with a flexible MVC architecture.

### 6. **Testing Support**

| Type of Testing         | What it Tests                           | Tools/Spring Support                                |
| ----------------------- | --------------------------------------- | --------------------------------------------------- |
| **Unit Testing**        | Testing individual classes/methods      | `@SpringBootTest`, `@MockBean`, JUnit, Mockito      |
| **Integration Testing** | Testing components together with Spring | `@SpringBootTest`, `@Transactional`, `@DataJpaTest` |
| **Web Layer Testing**   | Test controllers without full app       | `@WebMvcTest`, `MockMvc`                            |
| **Data Layer Testing**  | Test JPA Repositories, DB layer         | `@DataJpaTest`, embedded DB like H2                 |
| **Security Testing**    | Test login, roles, access control       | `@WithMockUser`, Spring Security Test               |
   

---

## 2. Inversion of Control (IoC)

- **Definition:** IoC is a design principle in which the control of object creation and their dependencies is transferred from the program to a container or framework.
- **In Spring:** The Spring IoC container manages the lifecycle and configuration of application objects (beans).

**Example:**
```java
public class HelloWorld {
    public void sayHello() {
        System.out.println("Hello, Spring IoC!");
    }
}
```
*The container (not the developer) creates and manages `HelloWorld` objects.*

IOC Container

The **IoC Container** is the core of the Spring Framework. It creates, configures, and manages beans.

**Types of Containers:**
	1.**BeanFactory:** 
	  Basic container, lazy initialization(- - beans are created only when requested (`getBean()`).) (e.g., mobile or small apps).can use this.
	   
	 2 **ApplicationContext:**
    Advanced, supports internationalization, event-propagation, etc.
    
    **`ApplicationContext` is a sub-interface of `BeanFactory`**
    
**`ApplicationContext` inherits all capabilities of `BeanFactory`**, plus adds more features.
- That means: **when you use `ApplicationContext`, bean creation is still managed through the `BeanFactory` interface**, but with additional behavior.
-**When to use**:
- For **web**, **enterprise**, or **production-level** applications.
 
**Example:**

# IoC Container vs. Plain Java Object Management

## What is an IoC Container?

- **IoC Container** (like in Spring) is a special object that creates, manages, and wires together your application’s objects (called “beans”) for you.
- It is a core part of the Spring Framework.


## How is Object Management Done in Plain Java?

In standard Java, you create and connect objects manually:

```java
Engine engine = new Engine();
Car car = new Car(engine);
```
- **You** are responsible for creating objects (`new Engine()`) and connecting them (`new Car(engine)`).
- If you need a different type of engine, you must change your code everywhere it is used.

## How Does the IoC Container Manage Objects?

With Spring’s IoC Container:

1. **You define your objects (beans) and their relationships in configuration** (XML, annotations, or Java config).
2. **Spring creates and connects them for you.** You just ask Spring for the object you need.

**Example (using annotations):**
```java
@Component
public class Engine {}

@Component
public class Car {
    private final Engine engine;
    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

**Spring Boot Application:**
```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext ctx = SpringApplication.run(MyApp.class, args);
        Car car = ctx.getBean(Car.class); // Spring gives you a ready-to-use Car
    }
}
```

- **Spring** creates the `Engine` and `Car` objects and injects the `Engine` into the `Car`.
- You **don’t use `new`** to create objects yourself.

## Key Differences (Table)

| Plain Java                        | IoC Container (Spring)          |
|-----------------------------------|---------------------------------|
| You create objects with `new`     | Spring creates objects for you  |
| You manage dependencies manually  | Spring connects dependencies    |
| Hard to change object types       | Easy to swap implementations    |
| Difficult to test in isolation    | Easier unit testing             |
| Tight coupling                    | Loose coupling                  |

## Why is IoC Container Useful?

- **Loose Coupling:** Your code does not depend on concrete classes; it depends on interfaces. Spring wires the right implementation.
- **Easier Configuration:** Change behavior/configuration without changing the code.
- **Better Testing:** You can easily swap real dependencies with mocks for testing.

## When you start a **Spring Boot** project, and you **don’t choose any container explicitly**:

>  **Spring Boot automatically uses `ApplicationContext` under the hood.**


---

## 3. Spring Bean & Its Scope

### What is a Spring Bean?
A **Spring Bean** is an object that is instantiated, assembled, and managed by the Spring IoC container.

### Bean Scopes:
- **singleton** (default): One instance per Spring IoC container.
- **prototype**: New instance each time requested.
- **request**: One instance per HTTP request (web only).
- **session**: One instance per HTTP session (web only).
- **application**: One instance per ServletContext (web only).
- **websocket**: One per WebSocket.

**Example:**
```java
@Component
@Scope("prototype")
public class ExampleBean {}
```
# Spring Bean & Its Scope: Simple Explanation

## What is a Spring Bean?

A **Spring Bean** is just a Java object that is created, managed, and “looked after” by the Spring Framework’s IoC container.  
You don’t need to create it with `new` keyword—Spring does that for you based on your configuration.

---

## What is Bean Scope?

**Bean scope** defines how many instances of a bean Spring will create, and how long those instances will “live”.  
It answers the question: **“How many objects of this class should Spring create, and when?”**

---

## Common Bean Scopes

| Scope Name     | What It Means (Simple)                                            | Where Used      |
|----------------|-------------------------------------------------------------------|-----------------|
| singleton      | Only one object is made for the whole application (default)       | Everywhere      |
| prototype      | A new object is created every time you ask Spring for it          | Everywhere      |
| request        | One object per HTTP request (web app only)                        | Web apps        |
| session        | One object per HTTP session (web app only)                        | Web apps        |
| application    | One object per web application (per ServletContext, web only)     | Web apps        |
| websocket      | One object per WebSocket connection                               | WebSocket apps  |

---

### **Singleton**
- Spring creates **only one instance (object)** of the bean per Spring container.
    
- That same **one object** is reused **everywhere you inject or retrieve it**.
    
- You can use **different variable names**, but they all **refer to the same object** (same memory reference).
    
```
@Component
public class MyService {
    public int count = 0;
}

@RestController
public class MyController {

    @Autowired
    private MyService a;

    @Autowired
    private MyService b;

    @GetMapping("/test")
    public String test() {
        a.count++;
        return "a: " + a.count + ", b: " + b.count;
    }
}

```
Even though `a` and `b` are **different variables**, both point to the **same object**.

---
## 2. **prototype**

> A **new object is created every time** it's requested from the container.

### 🔹 Code:

```
@Component
@Scope("prototype")
public class MyPrototypeService {
    public int count = 0;
}
MyPrototypeService a = context.getBean(MyPrototypeService.class);
MyPrototypeService b = context.getBean(MyPrototypeService.class);

```
###  Behavior:

- `a` and `b` are **two different objects**.
    
```
a.count = 10;
System.out.println(b.count);  // prints 0 (unaffected)

```
 Meaning:

- New object every time.
    
- Not shared.
    
- Useful when you want **independent state** in every instance.
    

> ❗ Note: In `@Autowired`, you must use `@Scope("prototype")` with a proxy or manually call `getBean()` to get a new instance.

**why `@Autowired` with `@Scope("prototype")` without a proxy or manual `getBean()` won't work as expected**.

		1## Scenario: A Tool Factory Producing Tools

### Your Goal:

You want to create a **ToolService** that uses a new `Tool` object every time it performs a task.

### PROBLEM:

```
@Component
@Scope("prototype")  // tells Spring: create new Tool every time it's requested
public class Tool {
    public Tool() {
        System.out.println("Tool instance created: " + this);
    }

    public void use() {
        System.out.println("Using tool: " + this);
    }
}
 ==create tool service==
@Component
public class ToolService {

    @Autowired
    private Tool tool;

    public void performTask() {
        System.out.println("Performing task with: " + tool);
        tool.use();
    }
}
==main==
@SpringBootApplication
public class MyApp {

    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(MyApp.class, args);

        ToolService service = context.getBean(ToolService.class);
        service.performTask(); // 1st call
        service.performTask(); // 2nd call
    }
}
Unexpected Behavior
Tool instance created: Tool@1a2b3c
Performing task with: Tool@1a2b3c
Using tool: Tool@1a2b3c

Performing task with: Tool@1a2b3c
Using tool: Tool@1a2b3c
	
```

	Even though you marked `Tool` as `prototype`, the same object is used every time.
## Why?

Because `@Autowired` injected the **Tool object only once** — when the `ToolService` was created.
Use ObjectFactory to get new instances
### SOLLUTION:
```
@Component
public class ToolService {

    @Autowired
    private ObjectFactory<Tool> toolFactory;//predefined interface

    public void performTask() {
        Tool tool = toolFactory.getObject();  // get a new Tool each time
        System.out.println("Performing task with: " + tool);
        tool.use();
    }
}
==another way 2==
@Component
@Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)//“Use **CGLIB (class-based)** proxying, so I don’t need to implement an interface.”
public class Tool {
    ...
}

Now Spring injects a **proxy object** into `ToolService`, which internally creates a **new Tool instance on each method call**.

output
Tool instance created: Tool@1a2b3c
Performing task with: Tool@1a2b3c
Using tool: Tool@1a2b3c

Tool instance created: Tool@4d5e6f
Performing task with: Tool@4d5e6f
Using tool: Tool@4d5e6f
> Now you're getting a **fresh Tool** every time — as expected for `@Scope("prototype")`.
```

> **The class that is being injected (i.e., the dependency)** — **must** be the one annotated with `@Scope("prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)`.

PROXY BEHAVIOR:
```
tool.use();  // <- this calls the proxy

```
### What happens internally:

1. `tool` is **not the actual Tool object**, but a **smart proxy**.
    
2. When you call `tool.use()`, the **proxy goes to the IoC container** (Spring’s bean factory).
    
3. It says:
    
    > “Hey Spring, give me a new `Tool` bean!”
    
4. Spring creates a **fresh new instance** of the `Tool` class (since it's prototype).
    
5. The **method call is passed to this new Tool instance**.
    
6. After that, the new instance is discarded unless you store it somewhere.

```
tool.use()  -->  [Proxy]
                 |
                 --> Spring Container (IoC)
                       |
                       --> creates new Tool()
                             |
                             --> calls use() on that new Tool

```
When to use:

- You're using `@Scope("prototype")` or any non-singleton scope
    
- And you want Spring to inject that bean into a **singleton bean**
    
- And your class does **not implement an interface**

**Since `Worker` is prototype,Since Tool is also prototype,  so no need of proxy**

---

## In Summary

- **Spring Beans** are objects managed by Spring.
- **Scope** controls how many bean instances exist and when they are created.
- The most common scopes are `singleton` (one object for all) and `prototype` (new object every time).

---

## 4. Dependency Injection (DI) & Its Types

**Dependency Injection** is a technique where the Spring IoC container injects dependencies into a bean.

### Types of DI in Spring:
- **Constructor Injection**
- **Setter Injection**
- **Field Injection** (not recommended for testing)

**Example: Constructor Injection**
```java
@Component
public class Car {
    private Engine engine;
    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

**Example: Setter Injection**
```java
@Component
public class Car {
    private Engine engine;
    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```

---

## 5. Getter and Setter Methods

**Getters** and **setters** are methods used to read and update the values of private fields.

**Example:**
```java
public class Person {
    private String name;
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```
*Spring uses setters for setter-based injection.*

---

## 6. Autowiring

**Autowiring** allows Spring to resolve and inject collaborating beans automatically.

**Types of Autowiring:**
- **byType**
- **byName**
- **constructor**
- **@Autowired annotation**

**Example:**
```java
@Component
public class Employee {
    @Autowired
    private Address address;
}
```

---



```java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
HelloWorld obj = (HelloWorld) context.getBean("helloWorld");
```

---

## 8. Modules in Spring Framework

- **Spring Core:** Provides IoC and DI.
- **Spring AOP:** Aspect-Oriented Programming.
- **Spring Data Access/Integration:** JDBC, ORM, JMS.
- **Spring Web:** Web MVC, Web WebSocket.
- **Spring Security:** Authentication and authorization.
- **Spring Test:** Testing support.

---

## 9. Maven Tool

**Maven** is a build automation and project management tool for Java projects.
- Downloads the libraries your project needs.
- Compiles your code.
- Runs tests.
- Packages your code (for example, into a JAR file).
### What Maven does automatically:

- **Downloads dependencies** (the libraries your project needs, as listed in `pom.xml`)
- **Runs plugins** for tasks like compiling code, running tests, packaging your application, etc.
- **Handles the project build process** with simple commands (like `mvn compile`, `mvn test`, `mvn package`)

### What you need to do manually:

- Create or edit your `pom.xml` to add dependencies and plugins you want.
- Run Maven commands in the terminal (like `mvn install`).
---
**JAR**
- Maven takes all your Java files, compiles them, and puts them together into one single file called a **JAR file**.
- It’s like a ZIP file that bundles together all your compiled `.class` files (your Java code), resources (like images, libraries, configuration files), and sometimes even other libraries your program needs.
- #### **The main reasons for using a JAR file:**

1. **Easy to Share and Distribute:**  
    Instead of sending many separate files, you just send one JAR file. This makes installing or sharing your program much simpler.
    
2. **Easy to Run:**  
    If your JAR is set up as an “executable JAR,” you can run your whole Java app with a single command:
    
    Code
    
    ```
    java -jar myapp.jar
    ```
    
3. **Consistency:**  
    All the files your program needs are packaged together, so there’s less chance something is missing.
    
4. **Organization:**  
    Keeps your project neat and tidy by combining everything into one file.
Maven will:

- **Compile** all your Java source files.
- **Bundle** the compiled files (and resources) into a single **JAR file**.
---

### 9.1. pom.xml

`pom.xml` (Project Object Model) file contains the configuration for Maven project.
## **What is pom.xml?**

- **pom.xml** is a special file in every Maven project.
- “POM” stands for **Project Object Model**.
- It’s written in XML format.

## **What does pom.xml do?**

It tells Maven:

- The project’s details (like name, version, description).
- What libraries (dependencies) your project needs.
- What plugins to use for building, testing, packaging, etc.
- How to build your project (build settings).

## **Why is pom.xml needed?**

- It helps automate the process of downloading libraries, compiling code, running tests, and packaging your app.
- It keeps all project configuration in one place so everyone working on the project uses the same setup.

**Example:**
```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>spring-demo</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```
**pom.xml is the “instruction manual” for Maven about your project.**

**what is xml?**
**XML** stands for **eXtensible Markup Language**.
- XML is a way to store and share data in a structured, readable format using tags.
- It looks similar to HTML, but it is used for data, not for displaying web pages.
- - Commonly used for configuration files (like `pom.xml` in Maven), data exchange between systems, and more.
- , **XML is a language for marking up and organizing data—not for writing programs.**

---
## **DEPENDENCY**
### **In normal Java (without Maven/Gradle):**

- If you want to use an external library, you:
    1. **Download the JAR file** for that library from the internet.
    2. **Add it to your project’s classpath** (in your IDE or via command line).
    3. **Import** the classes/packages in your code using `import` statements.

**This process is manual**—you have to find, download, and add each library yourself.  
If your project needs updates or more libraries, you repeat the steps.  
If you work in a team, everyone must do this setup the same way, or the project won’t work.

---

### **With Maven (and dependencies in pom.xml):**

- You **declare dependencies in `pom.xml`**—just write the library’s name and version.
- **Maven automatically downloads** all the required JARs for you (and their dependencies too!).
- If you work with others, they just run Maven and everything is set up—no manual downloads.

---

### **Why use dependencies (in Maven)?**

- **Automation:** No manual downloads; Maven handles everything.
- **Consistency:** Everyone on your team gets the same libraries and versions.
- **Easy updates:** Change the version in `pom.xml`, Maven updates it for you.
- **Transitive dependencies:** If your library depends on other libraries, Maven also fetches those automatically.
### 9.2. Dependencies

- **Dependencies** are external libraries or tools that your project needs in order to work.
- For example, if your Java program needs to connect to a database, you might use a library (dependency) that handles database connections.
**Example:**
```xml
<dependencies>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.23</version>
  </dependency>
</dependencies>
```

## **Why do you need to learn about dependencies?**

- Modern software is rarely built from scratch.  
    We often use code written by others (libraries) to save time and avoid “reinventing the wheel.”
- Understanding dependencies helps you:
    - Use powerful features someone else already built.
    - Solve problems faster.
    - Keep your code clean and organized.
## **What major role do dependencies play?**

1. **Add Functionality:**  
    They let you add features (like logging, networking, or database access) without writing all the code yourself.
    
2. **Save Time:**  
    You can focus on your project’s logic instead of low-level details.
    
3. **Maintainability:**  
    Using standard libraries makes your code easier to maintain and update.
    
4. **Collaboration:**  
    Teams can use the same dependencies, so everyone’s code works the same way.

---

### 9.3. Plugins

Plugins **Maven plugins are like tools** add additional build capability to Maven (compiling, packaging, etc).
## What do Maven plugins do?

- By default, Maven can do basic tasks (like compiling code and packaging it).
- **Plugins** allow Maven to do more:
    - Compile your Java code
    - Run your tests
    - Package your code into a JAR or WAR
    - Generate documentation
    - Check code style
    - And much more!
## How do they work?

- You tell Maven which plugins to use in your `pom.xml` file.
- Each plugin can have different goals (for example, `compile`, `test`, `package`).
**Example:**
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.10.1</version>
      <configuration>
        <source>17</source>
        <target>17</target>
      </configuration>
    </plugin>
  </plugins>
</build>
```

---

### 9.4. Common Maven Commands

| Command               | Use                                        |
| --------------------- | ------------------------------------------ |
| `mvn clean`           | Cleans the `target` directory              |
| `mvn compile`         | Compiles the source code                   |
| `mvn test`            | Runs tests                                 |
| `mvn package`         | Packages code into a JAR/WAR               |
| `mvn install`         | Installs JAR/WAR to local Maven repository |
| `mvn dependency:tree` | Shows dependency tree                      |

---

## Practical Example: Simple Spring Project with Maven

### 1. pom.xml

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>spring-demo</artifactId>
  <version>1.0-SNAPSHOT</version>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.3.23</version>
    </dependency>
  </dependencies>
</project>
```

### 2. Java Classes

**Engine.java**
```java
public class Engine {
    public void start() {
        System.out.println("Engine started!");
    }
}
```

**Car.java**
```java
public class Car {
    private Engine engine;
    public Car(Engine engine) {
        this.engine = engine;
    }
    public void drive() {
        engine.start();
        System.out.println("Car is driving!");
    }
}
```

**AppConfig.java**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {
    @Bean
    public Engine engine() {
        return new Engine();
    }
    @Bean
    public Car car() {
        return new Car(engine());
    }
}
```

**Main.java**
```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
        Car car = ctx.getBean(Car.class);
        car.drive();
    }
}
```
**Run:**
```shell
mvn compile
mvn exec:java -Dexec.mainClass="com.example.Main"
```

---

## **What is Aspect-Oriented Programming (AOP)?**

- **AOP** is a programming technique that allows you to add extra behavior (like logging, security, transactions) to your code without modifying the actual business logic.
- These extra behaviors are called **cross-cutting concerns** because they affect multiple parts of your application.

---
###  **Spring Beans: Bean Lifecycle and Configuration**

- **Spring Bean:**  
    An object that is managed by the Spring IoC (Inversion of Control) container.  
    You define these beans in your configuration (using `@Bean`, `@Component`, or XML).
- **Bean Lifecycle:**  
    The steps a bean goes through from creation to destruction:
    1. Instantiation (object is created)
    2. Populate properties (dependencies are set)
    3. Initialization (custom init methods can run)
    4. Use (bean is used in the app)
    5. Destruction (custom destroy methods can run)
- **Configuration:**  
    You tell Spring how to create and configure beans (via Java config, annotations, or XML).

---

### 2. **Spring Context (ApplicationContext, events, etc.)**

- **Spring Context (ApplicationContext):**  
    This is the central interface for providing configuration information to the application.  
    It is also called the "Spring Container".
- **What does it do?**
    - Manages beans and their lifecycles
    - Handles dependency injection
    - Publishes and listens to events (for communication between beans)
    - Provides access to resources (files, properties, etc.)
- **Example:**  
    `ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);`  
    This creates the container and loads your beans.

---

### 3. **Dependency Injection (DI)**

- **Dependency Injection:**  
    A design pattern where dependencies (objects a class needs) are provided by the container, not created manually inside the class.
- **In Spring:**  
    The Spring container injects (provides) beans into other beans, so you don’t have to use `new` to create dependencies.
- **Types of DI in Spring:**
    - Constructor Injection
    - Setter Injection
    - Field Injection
- **Benefit:**  
    Makes your code more modular, testable, and easier to manage.
---
**External jar file for project:**

If you use **Maven**, you **don’t need to manually download** external JARs like in old Java projects. Maven will:

- Automatically **download the required JAR** from **Maven Central Repository**
    
- **Cache it locally** in your system
    
- **Include it in your build** (like your `.jar` file)
### **How to get MySQL Connector in Spring Boot project?**

Just add the dependency in your `pom.xml`:
```
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <scope>runtime</scope>
</dependency>

```

Then, Maven will automatically:

- Download the `mysql-connector-java-x.x.x.jar` from the internet (Maven Central)
    
- Store it in your local repository (typically `~/.m2/repository`)
    
- Include it in your Spring Boot project during build
### 5. **No Internet?**

If you don’t have internet, Maven won’t be able to fetch new dependencies unless:

- You've already downloaded them earlier (they're cached in `.m2`)
    
- Or you manually download the `.jar` and install it locally with:
    
```
mvn install:install-file -Dfile=path-to-jar -DgroupId=mysql -DartifactId=mysql-connector-java -Dversion=8.0.33 -Dpackaging=jar

```

---