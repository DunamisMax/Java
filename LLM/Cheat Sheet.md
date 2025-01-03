Below is a **comprehensive Java Programming Cheat Sheet** covering key language features, best practices, and ecosystem highlights. It is not exhaustive but provides a quick reference for important concepts you’ll encounter in modern Java development.

---

## 1. Basic Syntax and Structure

### 1.1 Hello World Example

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- **Class Name**: Must match the filename (if public).
- **`main` Method**: Entry point for Java applications.
- **Compilation**: `javac HelloWorld.java`
- **Execution**: `java HelloWorld`

### 1.2 Java Source File Structure

1. **Package Declaration** (optional, but recommended):
   ```java
   package com.example.myapp;
   ```
2. **Imports** (to bring in external classes/packages):
   ```java
   import java.util.List;
   ```
3. **Class Definition**:
   ```java
   public class MyClass {
       // Fields, methods, nested classes, etc.
   }
   ```

---

## 2. Data Types and Variables

### 2.1 Primitive Types

| Type    | Size (bits) | Range                                     | Default Value |
|---------|------------:|-------------------------------------------|---------------|
| `byte`  | 8           | -128 to 127                               | 0             |
| `short` | 16          | -32,768 to 32,767                         | 0             |
| `int`   | 32          | -2,147,483,648 to 2,147,483,647           | 0             |
| `long`  | 64          | -9,223,372,036,854,775,808 to 9,223,372...| 0L            |
| `float` | 32          | IEEE 754 floating-point                   | 0.0f          |
| `double`| 64          | IEEE 754 floating-point                   | 0.0d          |
| `char`  | 16          | Unicode characters (\u0000 to \uffff)     | '\u0000'      |
| `boolean`| 1 (conceptually)| `true` or `false`                     | `false`       |

### 2.2 Reference Types
- **Classes**: Custom objects created from a class definition.
- **Arrays**: `int[] arr = new int[5];`
- **Enums**: Restricted set of constants. Example:
  ```java
  public enum Day { MON, TUE, WED, THU, FRI, SAT, SUN }
  ```
- **Records** (Java 16+): Immutable data carrier classes.
  ```java
  public record Point(int x, int y) { }
  ```

### 2.3 Variable Declarations
- **Local Variables**: Declared within methods/blocks, must be initialized before use.
- **Instance Variables**: Declared at the class level, created with the object.
- **Class (Static) Variables**: Declared with the `static` keyword at class level.

### 2.4 `var` (Java 10+)
- Allows local variable type inference:
  ```java
  var list = new ArrayList<String>();
  ```

---

## 3. Operators

| Operator Type        | Examples                  |
|----------------------|---------------------------|
| **Arithmetic**       | `+`, `-`, `*`, `/`, `%`  |
| **Assignment**       | `=`, `+=`, `-=`, etc.    |
| **Comparison**       | `==`, `!=`, `>`, `<`, `>=`, `<=` |
| **Logical**          | `&&`, `\|\|`, `!`         |
| **Bitwise**          | `&`, `\|`, `^`, `~`, `<<`, `>>`, `>>>` |
| **Ternary**          | `condition ? expr1 : expr2` |

---

## 4. Control Flow

### 4.1 `if` Statements

```java
if (x > 10) {
    // ...
} else if (x > 5) {
    // ...
} else {
    // ...
}
```

### 4.2 `switch` Statement

```java
switch (day) {
    case MON -> System.out.println("Monday");
    case TUE -> System.out.println("Tuesday");
    default  -> System.out.println("Other day");
}
```
- **Enhanced switch** (Java 14+): Use `->` or `yield` for more concise code.

### 4.3 Loops

- **`for` loop**:
  ```java
  for (int i = 0; i < 5; i++) { /* ... */ }
  ```
- **Enhanced `for` (for-each)**:
  ```java
  for (String item : list) { /* ... */ }
  ```
- **`while` loop**:
  ```java
  while (condition) { /* ... */ }
  ```
- **`do-while` loop**:
  ```java
  do {
      // ...
  } while (condition);
  ```

---

## 5. Object-Oriented Programming (OOP)

### 5.1 Classes and Objects

```java
public class Person {
    // Fields
    private String name;
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Methods
    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}
```

- **Instantiation**: `Person p = new Person("Alice", 30);`

### 5.2 Inheritance

- **Subclass extends a superclass**:
  ```java
  public class Employee extends Person {
      private String position;
      public Employee(String name, int age, String position) {
          super(name, age);
          this.position = position;
      }
  }
  ```

### 5.3 Interfaces & Abstract Classes
- **Interface**: Defines a contract (no state, only abstract methods by default).
  ```java
  public interface Drivable {
      void drive();
  }
  ```
- **Abstract Class**: May contain abstract methods and concrete methods.
  ```java
  public abstract class Vehicle {
      public abstract void move();
      public void stop() { /* ... */ }
  }
  ```

### 5.4 Encapsulation
- Use **private** fields + **public** getters/setters to limit direct access.

```java
public class BankAccount {
    private double balance;
    public double getBalance() { return balance; }
    public void deposit(double amount) { balance += amount; }
    public void withdraw(double amount) { balance -= amount; }
}
```

### 5.5 Polymorphism
- Different classes implementing the same interface or overriding methods differently.

### 5.6 Access Modifiers

| Modifier    | Class | Package | Subclass | World  |
|-------------|:-----:|:-------:|:--------:|:------:|
| **public**  | Y     | Y       | Y        | Y      |
| **protected** | Y   | Y       | Y        | N      |
| *(default)* | Y     | Y       | N        | N      |
| **private** | Y     | N       | N        | N      |

---

## 6. Collections and Generics

### 6.1 Common Collection Interfaces

| Interface    | Purpose                              | Common Implementations    |
|--------------|--------------------------------------|---------------------------|
| **List**     | Ordered, allows duplicates           | `ArrayList`, `LinkedList` |
| **Set**      | Unique elements                      | `HashSet`, `TreeSet`      |
| **Queue**    | FIFO ordering                        | `LinkedList`, `PriorityQueue` |
| **Map**      | Key-value pairs                      | `HashMap`, `TreeMap`, `LinkedHashMap` |

### 6.2 Generics

```java
List<String> names = new ArrayList<>();
names.add("Alice");
String first = names.get(0); // No cast needed
```

- **Wildcards**: `?`, `? extends Type`, `? super Type`
  ```java
  static void printList(List<?> list) { /* ... */ }
  ```

---

## 7. Functional Programming (Java 8+)

### 7.1 Lambda Expressions

```java
// Traditional
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};

// Lambda
Runnable r2 = () -> System.out.println("Hello");
```

### 7.2 Method References

```java
list.forEach(System.out::println);
```

### 7.3 Streams API

```java
List<String> filtered = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .sorted()
    .collect(Collectors.toList());
```

- **Common Stream Operations**: `filter`, `map`, `reduce`, `collect`, `sorted`, `distinct`, `limit`, `skip`.

---

## 8. Concurrency

### 8.1 Threads and Runnables

```java
public class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Running on thread " + Thread.currentThread().getName());
    }
}
```

- **Starting a Thread**:
  ```java
  Thread t = new Thread(new MyTask());
  t.start();
  ```

### 8.2 Executor Framework

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
executor.submit(() -> System.out.println("Task"));
executor.shutdown();
```

### 8.3 Synchronization

- **`synchronized` Keyword**:
  ```java
  public synchronized void increment() { counter++; }
  ```
- **Locks and Condition**: `ReentrantLock`, `Condition`
- **Concurrent Collections**: `ConcurrentHashMap`, `CopyOnWriteArrayList`, `BlockingQueue` classes.

### 8.4 Common Concurrency Utilities
- **CountDownLatch**, **CyclicBarrier**, **Semaphore**, **Atomic** classes (`AtomicInteger`, `AtomicLong`), **CompletableFuture** for async programming.

---

## 9. Exception Handling

### 9.1 `try-catch-finally`

```java
try {
    // Risky operation
} catch (IOException e) {
    // Handle exception
} finally {
    // Cleanup (always executed)
}
```

### 9.2 Checked vs. Unchecked Exceptions

- **Checked** (e.g., `IOException`, `SQLException`): Must be declared or handled.
- **Unchecked** (e.g., `RuntimeException`, `NullPointerException`): Not enforced by the compiler.

### 9.3 Try-With-Resources (Java 7+)

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // ...
} catch (IOException e) {
    // ...
}
```

---

## 10. Memory Management and the JVM

### 10.1 Heap vs. Stack
- **Stack**: Stores local variables, function call frames.
- **Heap**: Stores objects, allocated via `new`.

### 10.2 Garbage Collection
- **Common Collectors**: Serial, Parallel, CMS, G1, ZGC, Shenandoah.
- **Tuning**: `-Xms`, `-Xmx`, `-XX:MetaspaceSize`, `-XX:MaxMetaspaceSize`, etc.

### 10.3 Class Loading
- **Bootstrap**, **Extension**, **System** class loaders.
- **JVM Flags** for debugging: `-verbose:class`, `-verbose:gc`.

---

## 11. Modern Language Features

### 11.1 Records (Java 16+)
- Immutable data classes:
  ```java
  public record Point(int x, int y) {}
  ```

### 11.2 Sealed Classes (Java 17+)
- Restrict which classes can extend or implement a class/interface:
  ```java
  public sealed class Shape permits Circle, Square {}
  ```

### 11.3 Pattern Matching for `instanceof` (Java 16+)
```java
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

### 11.4 Switch Expressions (Java 14+)
```java
String result = switch (day) {
    case MON, FRI -> "Short day";
    case TUE, WED, THU -> "Long day";
    default -> {
        yield "Unknown";
    }
};
```

---

## 12. Build Tools

### 12.1 Maven
- **Project Object Model (POM)** in `pom.xml`.
- Basic commands:
    - `mvn clean`
    - `mvn compile`
    - `mvn test`
    - `mvn package`
    - `mvn install`

### 12.2 Gradle
- Uses **Groovy** or **Kotlin** DSL.
- Common tasks:
    - `gradle clean build`
    - `gradle test`
    - `gradle bootRun` (with Spring Boot plugin)

---

## 13. Testing

### 13.1 JUnit 5

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class MyTests {
    @Test
    void testSomething() {
        assertEquals(4, 2 + 2);
    }
}
```

### 13.2 Mockito

```java
@ExtendWith(MockitoExtension.class)
public class MyServiceTest {
    @Mock private Dependency dependency;
    @InjectMocks private MyService myService;

    @Test
    void testServiceMethod() {
        when(dependency.call()).thenReturn("mocked");
        String result = myService.serviceMethod();
        assertEquals("mocked", result);
    }
}
```

### 13.3 Other Tools
- **TestNG**: Alternative to JUnit with advanced configurations.
- **Behavior-Driven Development (BDD)** frameworks like **Cucumber**.

---

## 14. Popular Frameworks

### 14.1 Spring Boot
- **Annotations**: `@SpringBootApplication`, `@RestController`, `@Autowired`, `@Configuration`.
- **Application Properties**: `application.properties` or `application.yml`.
- **Dependency Injection** with `@Component`, `@Service`, `@Repository`.

### 14.2 Jakarta EE
- **CDI** (Contexts and Dependency Injection)
- **JPA** for ORM (e.g., Hibernate)
- **Servlets** and **JAX-RS** for web services.

### 14.3 Microservices
- **Spring Cloud** for config server, discovery (Eureka), load balancing (Ribbon), API gateway (Zuul/Gateway).
- **Quarkus**, **Micronaut**, **Helidon** for lightweight microservices.

---

## 15. Best Practices & Clean Code

1. **SOLID Principles**: Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.
2. **DRY, KISS**: Avoid duplication, keep it simple.
3. **Immutability**: Prefer immutable objects where possible.
4. **Exception Handling**: Throw descriptive exceptions, avoid catching generic `Exception`.
5. **Logging**: Use a framework (SLF4J, Log4j) instead of `System.out.println`.
6. **Testing**: Practice TDD/BDD, maintain high code coverage.
7. **Code Style**: Consistent naming conventions, indentation, and use static analysis tools (Checkstyle, PMD, SonarQube).

---

## 16. Concurrency Best Practices

1. **Use Higher-Level Concurrency APIs**: `ExecutorService`, `CompletableFuture`, parallel streams.
2. **Minimize Shared Mutable State**: Use thread-safe data structures or immutability.
3. **Avoid Deadlocks**: Acquire locks in a consistent order, or use lock-free algorithms.
4. **Parallel Streams**: Efficient for CPU-bound tasks, but watch out for side effects.

---

## 17. Debugging and Profiling

1. **JVM Flags**: `-Xmx`, `-Xms`, `-Xdebug`, `-Xrunjdwp` for remote debugging.
2. **Profilers**: **VisualVM**, **Java Flight Recorder**, **YourKit** to analyze CPU, memory usage, and thread activity.
3. **Logging Levels**: TRACE, DEBUG, INFO, WARN, ERROR.

---

## 18. Deployment and DevOps

1. **Containerization**: Dockerize your Java app using a Dockerfile.
2. **Orchestration**: Kubernetes (k8s) for scaling, load balancing, and self-healing.
3. **CI/CD**: Jenkins, GitHub Actions, or GitLab CI for automated builds/tests.
4. **Monitoring & Observability**: Prometheus & Grafana for metrics; ELK (Elasticsearch, Logstash, Kibana) for logging; Jaeger/Zipkin for distributed tracing.

---

## 19. Security

1. **Authentication & Authorization**: OAuth2, JWT, SAML, Spring Security.
2. **OWASP Top Ten**: Protect against XSS, SQL Injection, CSRF, etc.
3. **Transport Security**: SSL/TLS (HTTPS), strong cipher suites.
4. **Secure Config**: Store secrets safely (Vault, KMS).

---

## 20. Additional Tips

1. **Use IDE Features**: Refactoring, debugging, code generation, version control integration.
2. **Stay Current**: Keep up with the latest LTS releases (Java 17, Java 21, etc.).
3. **Documentation**: Javadoc comments (`/** ... */`) and code-level docs for maintainability.
4. **Community**: Contribute to open source, follow updates on OpenJDK, attend Java conferences and user groups.

---

## Quick Reference Summary

- **Basic Syntax**: Classes, `main` method, statements, blocks.
- **Data Types**: 8 primitives + reference types.
- **Collections**: `List`, `Set`, `Map` with generics.
- **Functional**: Lambdas, Streams, Method References.
- **OOP**: Classes, Interfaces, Inheritance, Polymorphism, Encapsulation.
- **Concurrency**: `Thread`, `ExecutorService`, `synchronized`, atomic classes.
- **Exceptions**: `try-catch-finally`, checked vs. unchecked.
- **Modern Java**: Records, Sealed Classes, Switch Expressions, Pattern Matching.
- **Tools**: Maven, Gradle, JUnit, Mockito.
- **Best Practices**: SOLID, DRY, KISS, TDD, secure coding.
- **Profiling/Debugging**: VisualVM, JFR, logging frameworks.
- **Deployment**: Docker, Kubernetes, Jenkins/GitHub Actions, cloud providers.
- **Security**: Spring Security, OAuth2, JWT, OWASP.

---

Use this cheat sheet as a high-level overview and quick reference. For more details, consult the official [Java Documentation](https://docs.oracle.com/en/java/) or specific framework manuals. Happy coding!