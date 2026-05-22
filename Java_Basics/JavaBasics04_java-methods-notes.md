# Java Methods - Complete Beginner Notes

---

## Table of Contents

1. [What is a Method?](#1-what-is-a-method)
2. [Why Use Methods?](#2-why-use-methods)
3. [Method Syntax and Components](#3-method-syntax-and-components)
4. [Access Modifiers in Java](#4-access-modifiers-in-java)
5. [Types of Methods](#5-types-of-methods)
6. [Methods Based on Parameters and Return Type](#6-methods-based-on-parameters-and-return-type)
7. [Method Arguments (Parameters)](#7-method-arguments-parameters)
8. [How to Access Methods in Java](#8-how-to-access-methods-in-java)
9. [Method Overloading (Brief Introduction)](#9-method-overloading-brief-introduction)
10. [Summary](#10-summary)

---

## 1. What is a Method?

A **method** is a block of code (set of instructions) that performs a specific task. It runs only when it is **called**.

> In C/C++, methods are called **functions**. In Java, we call them **methods**. Both mean the same thing — only the terminology is different.

### Simple Definition

A method is a reusable block of code designed to perform a single, well-defined task.

---

## 2. Why Use Methods?

- **Reusability** — Write once, call many times
- **Organization** — Break large programs into smaller, manageable pieces
- **Readability** — Each method has a clear purpose
- **Maintainability** — Fix bugs in one place instead of multiple places
- **Avoid repetition** — No need to write the same logic again and again

### Real-World Analogy

Think of a calculator app:
- One button for **addition**
- One button for **subtraction**
- One button for **multiplication**

Each button performs a specific task. Similarly, in Java, each method performs one specific task.

---

## 3. Method Syntax and Components

### General Syntax

```java
accessModifier [static] returnType methodName(parameters) {
    // method body — logic/instructions
    return value; // only if returnType is not void
}
```

### Parts of a Method

| Part | Description | Example |
|------|-------------|---------|
| **Access Modifier** | Controls who can access the method | `public`, `private`, `protected`, default |
| **static keyword** | If present → static method; if absent → non-static method | `static` |
| **Return Type** | Data type of value the method returns; `void` if nothing is returned | `int`, `String`, `void` |
| **Method Name** | Name of the method (follows variable naming rules) | `addition`, `getStudentName` |
| **Parameters** | Input values the method accepts (optional) | `int a, int b` |
| **Method Body** | Actual logic/instructions inside `{ }` | Calculations, print statements, etc. |
| **Return Statement** | Sends a value back to the caller (not used with `void`) | `return result;` |

### Example Breakdown

```java
public static int addition(int a, int b) {
    int result = a + b;
    return result;
}
```

| Component | Value | Explanation |
|-----------|-------|-------------|
| Access Modifier | `public` | Accessible from anywhere |
| Static/Non-static | `static` | Can be called without creating an object |
| Return Type | `int` | This method returns an integer value |
| Method Name | `addition` | Descriptive name for what the method does |
| Parameters | `int a, int b` | Takes two integer inputs |
| Return Statement | `return result;` | Sends the sum back to the caller |

---

## 4. Access Modifiers in Java

### What Are Access Modifiers?

Access modifiers are **keywords** that control **who can access** (use) a class, method, variable, or constructor. They define the **visibility** and **scope** of your code.

Think of it like rooms in a house:
- Some rooms are open for **everyone** (public)
- Some are only for **family** (protected)
- Some are **personal/private** (private)
- Some are open for **neighbors on the same street** (default)

Java provides **4 access modifiers**:

| Modifier | Access Level | Keyword |
|----------|-------------|--------|
| **Public** | Accessible from **anywhere** | `public` |
| **Private** | Accessible only **within the same class** | `private` |
| **Protected** | Accessible within the **same package + subclasses** | `protected` |
| **Default** | Accessible within the **same package only** | No keyword (just leave it blank) |

---

### 1. `public` — Accessible from Everywhere

A `public` method or variable can be accessed from **any class**, **any package**, **anywhere** in the project.

```java
// File: Greeting.java
public class Greeting {

    public void sayHello() {
        System.out.println("Hello from Greeting class!");
    }
}
```

```java
// File: Main.java (same or different package — doesn't matter)
public class Main {
    public static void main(String[] args) {
        Greeting g = new Greeting();
        g.sayHello(); // ✅ Works — sayHello() is public
    }
}
```

**Output:**
```
Hello from Greeting class!
```

**When to use:** When you want the method/variable to be accessible from **anywhere** in your project. Most methods that other classes need to call are marked `public`.

---

### 2. `private` — Accessible Only Within the Same Class

A `private` method or variable **cannot be accessed** from outside the class where it is defined. It is completely hidden from other classes.

```java
// File: BankAccount.java
public class BankAccount {

    private double balance = 50000.0;

    private void showBalance() {
        System.out.println("Balance: " + balance);
    }

    public void accountSummary() {
        System.out.println("--- Account Summary ---");
        showBalance(); // ✅ Works — same class
    }
}
```

```java
// File: Main.java
public class Main {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount();

        acc.accountSummary(); // ✅ Works — accountSummary() is public

        // acc.showBalance();  // ❌ Compiler Error! showBalance() is private
        // acc.balance = 0;    // ❌ Compiler Error! balance is private
    }
}
```

**Output:**
```
--- Account Summary ---
Balance: 50000.0
```

**Why it's useful:** Protects sensitive data. In the example above, no outside class can directly modify `balance` or call `showBalance()`. They must go through the `public` method `accountSummary()`, which acts as a controlled access point. This concept is called **Encapsulation**.

**When to use:** For internal/helper methods and sensitive data that should **not** be exposed to other classes.

---

### 3. `protected` — Accessible Within Same Package + Subclasses

A `protected` method or variable can be accessed by:
- Any class in the **same package**
- **Subclasses** (child classes) even if they are in a **different package**

```java
// File: Animal.java (package: animals)
package animals;

public class Animal {

    protected String sound = "Some sound";

    protected void makeSound() {
        System.out.println("Animal makes: " + sound);
    }
}
```

```java
// File: Dog.java (package: animals) — Same package
package animals;

public class Dog extends Animal {

    public void bark() {
        makeSound(); // ✅ Works — same package + subclass
        System.out.println("Dog barks!");
    }
}
```

```java
// File: Cat.java (package: pets) — Different package but subclass
package pets;
import animals.Animal;

public class Cat extends Animal {

    public void meow() {
        makeSound(); // ✅ Works — Cat is a subclass of Animal
        System.out.println("Cat meows!");
    }
}
```

```java
// File: Main.java (package: pets) — Different package, NOT a subclass
package pets;
import animals.Animal;

public class Main {
    public static void main(String[] args) {
        Animal a = new Animal();
        // a.makeSound(); // ❌ Compiler Error! Main is NOT a subclass of Animal
    }
}
```

**When to use:** When you want to share functionality with **child classes** but hide it from unrelated classes. Common in **inheritance** scenarios.

---

### 4. Default (No Keyword) — Accessible Within Same Package Only

If you **don't write any access modifier**, Java treats it as **default** access. It is accessible only by classes in the **same package**.

```java
// File: Helper.java (package: utils)
package utils;

class Helper {  // default access — no 'public' keyword

    void assist() {  // default access method
        System.out.println("Helping from Helper class");
    }
}
```

```java
// File: Tool.java (package: utils) — Same package
package utils;

public class Tool {
    public void useTool() {
        Helper h = new Helper();
        h.assist(); // ✅ Works — same package
    }
}
```

```java
// File: App.java (package: app) — Different package
package app;
// import utils.Helper; // ❌ Compiler Error! Helper class is not public

public class App {
    public static void main(String[] args) {
        // Helper h = new Helper(); // ❌ Cannot access — different package
    }
}
```

**When to use:** When the class or method is only meant for **internal use within the same package** and shouldn't be exposed outside.

---

### Access Modifier Visibility Table

| Modifier | Same Class | Same Package | Subclass (different package) | Any Other Class |
|----------|-----------|-------------|------------------------------|----------------|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| Default (none) | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

> Read the table from **most open** (public) to **most restricted** (private).

---

### Complete Example: All 4 Modifiers in One Class

```java
public class Employee {

    public String name = "Rahul";              // accessible from anywhere
    protected String department = "Engineering"; // accessible in same package + subclasses
    String position = "Developer";              // default — accessible in same package only
    private double salary = 75000.0;             // accessible only inside this class

    public void showPublicInfo() {
        System.out.println("Name: " + name);
    }

    protected void showDepartment() {
        System.out.println("Dept: " + department);
    }

    void showPosition() { // default access
        System.out.println("Position: " + position);
    }

    private void showSalary() {
        System.out.println("Salary: " + salary);
    }

    // Public method that internally uses private method
    public void showAllDetails() {
        showPublicInfo();  // ✅
        showDepartment();  // ✅
        showPosition();    // ✅
        showSalary();      // ✅ — same class, so private is accessible
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee();

        emp.showPublicInfo();   // ✅ public — works
        emp.showDepartment();   // ✅ protected — works (same package)
        emp.showPosition();     // ✅ default — works (same package)
        // emp.showSalary();    // ❌ private — compiler error!

        System.out.println();
        emp.showAllDetails();   // ✅ Calls everything including private (internally)
    }
}
```

**Output:**
```
Name: Rahul
Dept: Engineering
Position: Developer

Name: Rahul
Dept: Engineering
Position: Developer
Salary: 75000.0
```

> Notice: `showSalary()` cannot be called directly from `Main`, but `showAllDetails()` can call it because both are in the **same class** (`Employee`).

---

### Quick Decision Guide

| Question | Choose |
|----------|--------|
| Should everyone access it? | `public` |
| Only this class should use it? | `private` |
| This class + its children need it? | `protected` |
| Only classes in the same package? | Default (no keyword) |

---

## 5. Types of Methods

### A. Based on Who Created Them

#### 1. Predefined Methods (Built-in)

Methods already provided by Java. You just use them.

```java
System.out.println("Hello");  // println() is a predefined method
Math.max(10, 20);             // max() is a predefined method
String s = "Java";
s.length();                   // length() is a predefined method
```

#### 2. User-Defined Methods

Methods written by the developer to achieve specific tasks.

```java
public static int multiply(int a, int b) {
    return a * b;
}
```

---

### B. Based on Static Keyword

#### 1. Static Methods

- Declared with `static` keyword
- Belongs to the **class**, not to any object
- Can be called **without creating an object**
- Can directly access other static members

```java
public static void greet() {
    System.out.println("Hello from a static method!");
}
```

#### 2. Non-Static Methods (Instance Methods)

- Declared **without** `static` keyword
- Belongs to the **object**
- Requires an **object** to be called
- Can access both static and non-static members

```java
public void greet() {
    System.out.println("Hello from a non-static method!");
}
```

---

### Why is `main()` Always Static?

```java
public static void main(String[] args) { }
```

- JVM needs to call `main()` to start the program
- At startup, no objects exist yet
- Since `static` methods don't need objects, JVM can call `main()` directly
- That's why Java requires `main()` to be `static`

---

## 6. Methods Based on Parameters and Return Type

Java methods fall into **4 categories** based on whether they take input and/or produce output:

---

### Type 1: No Parameters & No Return Value

The method performs an action but doesn't take any input and doesn't return any result.

```java
public class Demo {
    // Method: no input, no output
    public static void sayHello() {
        System.out.println("Hello, Welcome to Java!");
    }

    public static void main(String[] args) {
        sayHello(); // calling the method
    }
}
```

**Output:**
```
Hello, Welcome to Java!
```

**When to use:** When the task is fixed and doesn't depend on any input values (e.g., printing a welcome message).

---

### Type 2: Parameters & No Return Value

The method takes input values but doesn't return anything. It uses the inputs to perform some action.

```java
public class Demo {
    // Method: takes input, no output
    public static void printStudentInfo(String name, int age) {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }

    public static void main(String[] args) {
        printStudentInfo("Rahul", 22);
        printStudentInfo("Priya", 20);
    }
}
```

**Output:**
```
Name: Rahul
Age: 22
Name: Priya
Age: 20
```

**When to use:** When you want to perform an action using input values but don't need a result back (e.g., displaying information).

---

### Type 3: No Parameters & Has Return Value

The method doesn't take any input but returns a result.

```java
public class Demo {
    // Method: no input, returns output
    public static String getCourseName() {
        return "Core Java";
    }

    public static void main(String[] args) {
        String course = getCourseName();
        System.out.println("Course: " + course);
    }
}
```

**Output:**
```
Course: Core Java
```

**When to use:** When the method always produces the same fixed result (e.g., getting a configuration value, returning a company name).

---

### Type 4: Parameters & Has Return Value

The method takes input values, processes them, and returns a result. This is the **most common** type in real applications.

```java
public class Demo {
    // Method: takes input, returns output
    public static int addition(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        int result = addition(10, 20);
        System.out.println("Sum: " + result);

        int result2 = addition(50, 70);
        System.out.println("Sum: " + result2);
    }
}
```

**Output:**
```
Sum: 30
Sum: 120
```

**When to use:** When the logic depends on input values and you need the result back (e.g., calculations, data processing).

---

### Quick Comparison Table

| Type | Parameters | Return | Keyword for Return Type | Return Statement |
|------|-----------|--------|------------------------|-----------------|
| Type 1 | No | No | `void` | Not needed |
| Type 2 | Yes | No | `void` | Not needed |
| Type 3 | No | Yes | `int`, `String`, etc. | Required |
| Type 4 | Yes | Yes | `int`, `String`, etc. | Required |

---

## 7. Method Arguments (Parameters)

### What are Arguments?

Arguments (or parameters) are **input values** that you pass to a method so it can use them in its logic.

- **Parameters** → Variables defined in the method signature (formal parameters)
- **Arguments** → Actual values passed when calling the method

```java
// 'a' and 'b' are parameters
public static int add(int a, int b) {
    return a + b;
}

public static void main(String[] args) {
    // 10 and 20 are arguments
    int result = add(10, 20);
}
```

---

### Rules for Method Arguments

1. **Number of values must match** — If a method has 2 parameters, you must pass exactly 2 values

```java
public static int add(int a, int b) { return a + b; }

// Correct
add(10, 20);

// Wrong — compiler error
add(10);        // Too few arguments
add(10, 20, 30); // Too many arguments
```

2. **Data type order must match** — Pass values in the same order and type as defined

```java
public static void display(String name, int age) {
    System.out.println(name + " - " + age);
}

// Correct
display("Rahul", 25);

// Wrong — compiler error (types are swapped)
display(25, "Rahul");
```

3. **Zero arguments is valid** — Methods don't always need parameters

```java
public static void greet() {
    System.out.println("Hello!");
}
```

---

### Why Use Arguments?

Without arguments, the method always produces the same result (static behavior):

```java
// Without arguments — always returns 30
public static int add() {
    int a = 10, b = 20;
    return a + b; // Always 30
}
```

With arguments, the method becomes **dynamic** — different inputs produce different outputs:

```java
// With arguments — flexible and reusable
public static int add(int a, int b) {
    return a + b;
}

// Now you can get different results
add(10, 20); // 30
add(50, 80); // 130
add(5, 3);   // 8
```

---

## 8. How to Access Methods in Java

### Key Rules to Remember

| Scenario | Rule |
|----------|------|
| Static method calling another **static** method | Call **directly** (same class) or using **ClassName.method()** (different class) |
| Static method calling a **non-static** method | Must create an **object** first |
| Non-static method calling a **static** method | Can call **directly** |
| Non-static method calling another **non-static** method | Can call **directly** (same class) or using **object** (different class) |

---

### Case 1: Calling Static Method from Static Method (Same Class)

No object needed — call directly.

```java
public class Calculator {

    public static int multiply(int a, int b) {
        return a * b;
    }

    public static void main(String[] args) {
        // Direct call — both are static, same class
        int result = multiply(5, 4);
        System.out.println("Result: " + result);
    }
}
```

**Output:**
```
Result: 20
```

---

### Case 2: Calling Non-Static Method from Static Method (Same Class)

Must create an **object** of the same class.

```java
public class Calculator {

    // Non-static method
    public int addition(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        // Cannot call directly: addition(10, 20); ❌ — compiler error!

        // Must create an object first
        Calculator obj = new Calculator();
        int result = obj.addition(10, 20);
        System.out.println("Sum: " + result);
    }
}
```

**Output:**
```
Sum: 30
```

**Why?** The `main` method is static (class-level), but `addition` is non-static (object-level). Non-static members need an object to exist in memory.

---

### Case 3: Calling Non-Static Method from Non-Static Method (Same Class)

Call directly — both belong to the same object.

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }

    public void showResult() {
        // Direct call — both are non-static, same class
        int result = add(15, 25);
        System.out.println("Result: " + result);
    }

    public static void main(String[] args) {
        Calculator obj = new Calculator();
        obj.showResult();
    }
}
```

**Output:**
```
Result: 40
```

---

### Case 4: Calling Static Method from Non-Static Method (Same Class)

Call directly — static members are always accessible.

```java
public class Calculator {

    public static int multiply(int a, int b) {
        return a * b;
    }

    public void showProduct() {
        // Direct call — static methods are accessible from anywhere
        int result = multiply(6, 7);
        System.out.println("Product: " + result);
    }

    public static void main(String[] args) {
        Calculator obj = new Calculator();
        obj.showProduct();
    }
}
```

**Output:**
```
Product: 42
```

---

### Case 5: Calling Methods from a Different Class

#### Calling Non-Static Method of Another Class

Create an object of **that** class.

```java
// File: Calculator.java
public class Calculator {
    public int addition(int a, int b) {
        System.out.println("Addition from Calculator class");
        return a + b;
    }
}
```

```java
// File: MainApp.java
public class MainApp {
    public static void main(String[] args) {
        // Create object of Calculator class
        Calculator calc = new Calculator();
        int result = calc.addition(30, 50);
        System.out.println("Result: " + result);
    }
}
```

**Output:**
```
Addition from Calculator class
Result: 80
```

---

#### Calling Static Method of Another Class

Use **ClassName.methodName()** — no object needed.

```java
// File: Calculator.java
public class Calculator {
    public static int multiply(int a, int b) {
        System.out.println("Multiplication from Calculator class");
        return a * b;
    }
}
```

```java
// File: MainApp.java
public class MainApp {
    public static void main(String[] args) {
        // Call using class name — no object needed
        int result = Calculator.multiply(5, 20);
        System.out.println("Result: " + result);
    }
}
```

**Output:**
```
Multiplication from Calculator class
Result: 100
```

---

### Complete Example: All Access Patterns Together

```java
// File: MathUtils.java
public class MathUtils {

    // Static method
    public static int square(int n) {
        return n * n;
    }

    // Non-static method
    public int cube(int n) {
        return n * n * n;
    }
}
```

```java
// File: App.java
public class App {

    public static void main(String[] args) {

        // Calling STATIC method from different class — use class name
        int sq = MathUtils.square(5);
        System.out.println("Square of 5: " + sq);

        // Calling NON-STATIC method from different class — use object
        MathUtils obj = new MathUtils();
        int cu = obj.cube(3);
        System.out.println("Cube of 3: " + cu);
    }
}
```

**Output:**
```
Square of 5: 25
Cube of 3: 27
```

---

### Summary of Access Rules

```
┌─────────────────────────────────────────────────────────────────┐
│               HOW TO CALL METHODS IN JAVA                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SAME CLASS:                                                    │
│  ┌────────────────────────────────────────────┐                 │
│  │ static  →  static    : Call directly       │                 │
│  │ static  →  non-static: Use object          │                 │
│  │ non-static → static  : Call directly       │                 │
│  │ non-static → non-static: Call directly     │                 │
│  └────────────────────────────────────────────┘                 │
│                                                                 │
│  DIFFERENT CLASS:                                               │
│  ┌────────────────────────────────────────────┐                 │
│  │ Calling static method:                     │                 │
│  │   → ClassName.methodName()                 │                 │
│  │                                            │                 │
│  │ Calling non-static method:                 │                 │
│  │   → ClassName obj = new ClassName();       │                 │
│  │   → obj.methodName()                       │                 │
│  └────────────────────────────────────────────┘                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

### Common Compiler Errors

| Error Message | Cause | Fix |
|--------------|-------|-----|
| `non-static method cannot be referenced from a static context` | Calling non-static method directly from static method | Create an object first |
| `method X in class Y cannot be applied to given types` | Wrong number or type of arguments | Match the parameter count and types |
| `incompatible types` | Return type mismatch (e.g., method returns String but assigned to int) | Match the variable type with return type |

---

## 9. Method Overloading (Brief Introduction)

**Method overloading** means having multiple methods with the **same name** but **different parameters** in the same class.

Java identifies which method to call based on the **number** and **type** of arguments.

```java
public class Calculator {

    // Two int parameters
    public static int add(int a, int b) {
        return a + b;
    }

    // Three int parameters
    public static int add(int a, int b, int c) {
        return a + b + c;
    }

    // Two double parameters
    public static double add(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        System.out.println(add(10, 20));        // Calls first method → 30
        System.out.println(add(10, 20, 30));    // Calls second method → 60
        System.out.println(add(2.5, 3.5));      // Calls third method → 6.0
    }
}
```

**Output:**
```
30
60
6.0
```

### Rules for Overloading

- Method name must be the **same**
- Parameters must be **different** (count, type, or order)
- Return type alone is **not** enough to overload

---

## 10. Summary

### Key Takeaways

| Concept | Key Point |
|---------|-----------|
| Method | A reusable block of code to perform a specific task |
| Static method | Belongs to class — call without object |
| Non-static method | Belongs to object — needs object to call |
| void | Method returns nothing |
| return | Sends a value back to the caller |
| Parameters | Input values a method accepts |
| Arguments | Actual values passed when calling a method |
| Overloading | Same name, different parameters |

### Golden Rules

1. **Every Java program starts execution from `main()` method**
2. **`main()` is always static** — JVM calls it without creating an object
3. **Non-static methods need an object** — always create object before calling
4. **Static methods can be called directly** (same class) or via **ClassName.method()** (different class)
5. **Number and type of arguments must match** the method's parameter list
6. **Return type must match** — if a method returns `int`, store it in an `int` variable
7. **Don't write methods inside other methods** — Java doesn't allow nested method definitions
8. **One method can call any other method** — there's no restriction on which method calls which (just follow static/non-static rules)
9. **In real-time applications, 90%+ methods are non-static** — because Java is object-oriented

### Method Declaration Cheat Sheet

```java
// Static method with return value
public static int methodName(int param1, int param2) {
    // logic
    return value;
}

// Static method without return value
public static void methodName(int param1) {
    // logic — no return statement
}

// Non-static method with return value
public int methodName(int param1) {
    // logic
    return value;
}

// Non-static method without return value
public void methodName() {
    // logic — no return statement
}
```

---

> **Tip:** Practice writing different types of methods. Start with simple ones (void, no parameters) and gradually move to methods with parameters and return values. The more you practice, the more natural it becomes.

---

*Happy Coding! ☕*
