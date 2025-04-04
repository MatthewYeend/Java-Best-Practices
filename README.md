# Java Best Practices
<!-- TOC -->
## Table of Contents
1. [Variable Naming](#variable-naming)
2. [Method Naming](#methoc-naming)
3. [Magic Numbers](#magic-numbers)
4. [Code Formatting](#code-formatting)
5. [Avoiding Redundant Code](#avoiding-redundant-code)
6. [Using StringBuilder for Concatenation in Loops](#using-stringbuilder-for-concatenation-in-loops)
7. [Proper Resource Management (Avoiding Resource Leaks)](#proper-resource-management-avoiding-resource-leaks)
8. [Avoid Catching Generic Exceptions](#avoid-catching-generic-exceptions)
9. [Use Enum Instead of Constant Strings](#use-enum-instead-of-constant-strings)
10. [Using Streams Instead of Loops for Filtering](#using-streams-instead-of-loops-for-filtering)
11. [Avoid Using Raw Types (Generics)](#avoid-using-raw-types-generics)
12. [Prefer Interfaces Over Concrete Classes for Type References](#prefer-interfaces-over-concrete-classes-for-type-references)
13. [Best Practices accepted by community](#best-practices-accepted-by-community)
14. [Java Naming Conventions](#python-naming-conventions)
15. [Interview Questions](#interview-questions)
    1. [Beginner](#beginner)
    2. [Intermediate](#intermediate)
    3. [Expert](#expert)
    4. [General](#general)
    5. [Miscellaneous Questions](#miscellaneous-questions)
<!-- /TOC -->

## Variable Naming
### Bad
```java
int a = 10;
int b = 20;
int c = a + b;
```

### Good
```java
int numApples = 10;
int numOranges = 20;
int totalFruits = numApples + numOranges;
```

The **Good** approach uses descriptive variable names that clearly convey their purpose, making the code easier to understand and maintain.

---

## Method Naming
### Bad
```java
public int f(int x, int y) {
    return x * y;
}
```

### Good
```java
public int multiply(int firstNumber, int secondNumber) {
    return firstNumber * secondNumber;
}
```
The **Good** example uses a descriptive method name (multiply) and meaningful parameter names, improving readability.

---
## Magic Numbers
### Bad
```java
double finalAmount = 1000 * 0.08;
```

```java
final double TAX_RATE = 0.08;
double initialAmount = 1000;
double finalAmount = initialAmount * TAX_RATE;
```
The **Good** example avoids “magic numbers” by using a constant (TAX_RATE), making the code self-explanatory and easier to modify.

--- 
## Code Formatting
### Bad
```java
public class Example {public void sayHello(){System.out.println("Hello!");}}
```

### Good
```java
public class Example {
    public void sayHello() {
        System.out.println("Hello!");
    }
}
```
Proper indentation and spacing improve readability and maintainability.

---
## Avoiding Redundant Code
### Bad
```java
if (userAge >= 18) {
    return true;
} else {
    return false;
}
```

### Good
```java
return userAge >= 18;
```
The **Good** example simplifies the logic without unnecessary conditionals.

---
## Using StringBuilder for Concatenation in Loops
### Bad
```java
String result = "";
for (int i = 0; i < 10; i++) {
    result += i;
}
```

### Good
```java
StringBuilder result = new StringBuilder();
for (int i = 0; i < 10; i++) {
    result.append(i);
}
```
Using `StringBuilder` is more efficient than repeatedly concatenating strings, as it avoids creating multiple immutable `String` objects.

--- 
## Proper Resource Management (Avoiding Resource Leaks)
### Bad
```java
FileReader reader = new FileReader("file.txt");
BufferedReader br = new BufferedReader(reader);
System.out.println(br.readLine());
br.close();
reader.close();
```

### Good
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
}
```
Using Try-with-resources automatically closes resources, preventing memory leaks.

---
## Avoid Catching Generic Exceptions
### Bad
```java
try {
    int result = 10 / 0;
} catch (Exception e) {
    System.out.println("Error occurred.");
}
```

### Good
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
}
```
Use Catch specific exceptions to improve debugging and error handling.

---
## Use Enum Instead of Constant Strings
### Bad
```java
public static final String STATUS_ACTIVE = "ACTIVE";
public static final String STATUS_INACTIVE = "INACTIVE";
```

### Good
```java
public enum Status {
    ACTIVE, INACTIVE;
}
```
Enums improve type safety, readability, and prevent invalid values.

---
## Using Streams Instead of Loops for Filtering
### Bad
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        filteredNames.add(name);
    }
}
```

### Good
```java
List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("A"))
                                  .collect(Collectors.toList());
```
Streams are more concise and readable than traditional loops.

---
## Avoid Using Raw Types (Generics)
### Bad 
```java
List list = new ArrayList();
list.add("Hello");
String s = (String) list.get(0); // Requires explicit casting
```

### Good
```java
List<String> list = new ArrayList<>();
list.add("Hello");
String s = list.get(0); // No explicit casting needed
```
Using generics makes the code type-safe and eliminates unnecessary type casting.

---
## Prefer Interfaces Over Concrete Classes for Type References
### Bad
```java
ArrayList<String> names = new ArrayList<>();
```

### Good
```java
List<String> names = new ArrayList<>();
```
Using interfaces (List instead of ArrayList) improves flexibility and allows for easier switching of implementations.

---
## Best Practices accepted by community
| Task | Standard Tools | 3rd Party Tools |
|---|---|---|
| API Documentation | Javadoc | Swagger, Postman collections |
| API Security | Spring Security, Java EE Security | Custom JWT/OAuth implementations |
| Build Tool | Maven, Gradle |Ant, Bazel |
| Database Access | JDBC, JPA, Hibernate | MyBatis, jOOQ |
| Dependency Injection | Spring Framework, Jakarta CDI | Google Guice |
| Logging | SLF4J + Logback, Java Util Logging (JUL) | Log4j |
| Testing | JUnit, TestNG, Mockito | Spock, Cucumber |
| Web Frameworks | Spring Boot, Java EE (Jakarta EE) | Play Framework, Micronaut | 

--- 
## Java Naming Conventions
| What | How | Good | Bad |
|---|---|---|---|
| Class Attributes | CamelCase, start with a lowercase letter | `customerName`, `totalAmount` | `Customer_name`, `TOTALAMOUNT` |
| Classes | PascalCase | `CustomerDetails`, `OrderProcessor` | `customerDetails`, `order_processor` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRIES`, `DEFAULT_TIMEOUT` | `MaxRetries`, `defaultTimeout` | 
| Enum Names | PascalCase | `OrderStatus`, `UserType` | `order_status`, `usertype` | 
| Exceptions | PascalCase with Exception suffix | `InvalidInputException` | `invalidinputexception` |
| Interfaces | PascalCase, usually adjective-based | `Runnable`, `Serializable` | `runnable`, `serializable` | 
| Local Variables | camelCase | `orderCount`, `userId` | `Order_count`, `User_ID` |
| Methods | camelCase | `calculateTotal()`, `getUserId()` | `Calculate_Total()`, `GetUserID()` |
| Packages | lowercase, domain-based | `com.example.service` | `Com.Example.Service` |
| Static Variables | camelCase | `defaultConfig`, `appName` | `DefaultConfig`, `APP_NAME` |
| Test Classes | PascalCase with Test suffix | `UserServiceTest`, `OrderTest` | `userservicetest`, `ordertest` |

---
## Interview Questions
### Beginner
- What are Java’s key features?
	- Platform-Independent: Java runs on any OS with a JVM.
	- Object-Oriented: Java supports OOP principles like inheritance and polymorphism.
	- Multi-threaded: Java supports concurrent programming using threads.
	- Garbage Collection: Automatic memory management via the Garbage Collector.
- What is the difference between `==` and `.equals()` in Java?
    - `==` checks if two references point to the same object in memory.
	- `.equals()` checks if two objects have the same value.
- What are Java’s primitive data types?
    - `byte`, `short`, `int`, `long` (integer types)
	- `float`, `double` (floating-point types)
	- `char` (character)
	- `boolean` (true/false)
### Intermediate
- What is the difference between an ArrayList and a LinkedList?
    - | Feature | ArrayList | LinkedList
      |---|---|---|
      | Storage | Dynamic array | Doubly linked list |
      | Access Time | Fast (O(1)) random access | Slow (O(n)) sequential access |
      | Insert/Delete | Slow (O(n)) | Fast (O(1) at head/tail) |
      | Memory Usage | Less (contiguous memory) | More (extra pointers) |
- What is the difference between `final`, `finally`, and `finalize()`?
    - `final`: Used for constants, preventing method overriding or inheritance.
	- `finally`: A block in a try-catch-finally statement that always executes.
	- `finalize()`: A method called before an object is garbage collected.
- How does Java achieve memory management?
    - Heap and Stack: Java uses a heap (for objects) and stack (for local variables).
	- Garbage Collection: Java automatically removes unused objects.
### Expert
- What is the difference between checked and unchecked exceptions?
    - Checked Exception: Must be handled using try-catch or declared with throws.
	    - Example: `IOException`, `SQLException`.
	- Unchecked Exception: Extends RuntimeException, doesn’t require handling.
	    - Example: `NullPointerException`, `ArrayIndexOutOfBoundsException`.
- What is the purpose of volatile in Java?
    - The volatile keyword ensures that changes to a variable are visible to all threads immediately, preventing caching issues.
- What is the difference between synchronized and lock in Java?
    - `synchronized` is a keyword that locks an object or method.
	- Lock (from `java.util.concurrent.locks`) provides more flexibility, allowing try-lock and timed locking.
### General
- What is the difference between String, StringBuilder, and StringBuffer?
    - | Feature | `String` (Immutable) | `StringBuilder` (Mutable) | `StringBuffer` (Thread-Safe) |
      |---|---|---|---| 
      | Thread Safety | No | No | Yes |
      | Performance | Slow | Fast | Slower than `StringBuilder` |
- What is the Java Collections Framework?
    - A set of classes and interfaces for working with data structures like lists, sets, and maps.
	    - List: `ArrayList`, `LinkedList`
	    - Set: `HashSet`, `TreeSet`
	    - Map: `HashMap`, `TreeMap`

### Miscellaneous Questions
- What is the `transient` keyword in Java?
    - The `transient` keyword prevents a field from being serialized.
- What are Java 8 features?
    - Lambda Expressions
	- Streams API
	- Functional Interfaces
	- Optional Class

---