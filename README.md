# Java Best Practices
<!-- TOC -->
## Table of Contents
1. [Variable Naming](#variable-naming)
2. [Method Naming](#methoc-naming)
3. [Magic Numbers](#magic-numbers)
4. [Code Formatting](#code-formatting)
5. [Avoiding Redundant Code](#avoiding-redundant-code)
6. [Using StringBuilder for Concatenation in Loops](#using-stringbuilder-for-concatenation-in-loops)
7. [Best Practices accepted by community](#best-practices-accepted-by-community)
8. [Java Naming Conventions](#python-naming-conventions)
9. [Interview Questions](#interview-questions)
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
