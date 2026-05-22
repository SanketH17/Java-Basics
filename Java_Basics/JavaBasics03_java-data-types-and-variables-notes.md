# Java Data Types and Variables - Complete Beginner Notes

---

## Table of Contents

1. [Memory of Primitive Data Types](#1-memory-of-primitive-data-types)
2. [Categories of Non-Primitive Data Types](#2-categories-of-non-primitive-data-types)
3. [Data Types and Variables in Java](#3-data-types-and-variables-in-java)
4. [Static vs Non-Static Variables](#4-static-vs-non-static-variables)
5. [Summary](#5-summary)

---

## 1. Memory of Primitive Data Types

### What Are Primitive Data Types?

Primitive data types are the most basic data types provided by Java. They are **not classes** — they are simple value holders built directly into the language. Primitive variables **store actual values directly** in memory (not references).

Java provides **8 primitive data types** to handle different kinds of data.

---

### List of Primitive Data Types

| Data Type | Size (Memory) | Default Value | Value Range | Used For |
|-----------|--------------|---------------|-------------|----------|
| `byte` | 1 byte (8 bits) | 0 | -128 to 127 | Very small integers |
| `short` | 2 bytes (16 bits) | 0 | -32,768 to 32,767 | Small integers |
| `int` | 4 bytes (32 bits) | 0 | ~-2.1 billion to ~2.1 billion | General-purpose integers |
| `long` | 8 bytes (64 bits) | 0L | Very large numbers | Large integers (e.g., mobile numbers) |
| `float` | 4 bytes (32 bits) | 0.0f | 6-7 decimal digits precision | Decimal values (less precision) |
| `double` | 8 bytes (64 bits) | 0.0 | 15-16 decimal digits precision | Decimal values (more precision) |
| `char` | 2 bytes (16 bits) | '\u0000' | Single character (A-Z, 0-9, symbols) | Single characters |
| `boolean` | 1 bit* | false | true or false | Yes/No decisions |

> *Boolean size is JVM-dependent, but logically it represents 1 bit of information.

---

### Why Does Memory Size Matter?

When you declare a variable, JVM allocates memory based on the data type — **regardless of the actual value stored**.

```java
byte a = 10;   // Allocates 1 byte — sufficient for small values like age, temperature
int b = 10;    // Allocates 4 bytes — even though value is just 10
```

If you only store values like 10, 20, 30 (human age, temperature), using `int` wastes 3 extra bytes per variable. For a single variable, this doesn't matter much. But in real applications with **thousands or millions of variables**, choosing the right data type improves memory efficiency and application performance.

**Rule of thumb:** Choose the smallest data type that can safely hold all possible values for your variable.

---

### Example Declarations

```java
public class PrimitiveDataTypesDemo {
    public static void main(String[] args) {

        // Integer types
        byte age = 25;                    // 1 byte
        short temperature = -15;          // 2 bytes
        int salary = 50000;               // 4 bytes
        long mobileNumber = 9876543210L;  // 8 bytes — must append 'L'

        // Floating-point types
        float price = 99.99f;             // 4 bytes — must append 'f'
        double pi = 3.141592653589793;    // 8 bytes — no suffix needed

        // Character type
        char grade = 'A';                 // 2 bytes — single quotes only

        // Boolean type
        boolean isJavaFun = true;         // true or false only

        System.out.println("Age: " + age);
        System.out.println("Mobile: " + mobileNumber);
        System.out.println("Price: " + price);
        System.out.println("Grade: " + grade);
        System.out.println("Is Java Fun? " + isJavaFun);
    }
}
```

---

### Important Rules to Remember

| Data Type | Rule |
|-----------|------|
| `long` | Append lowercase `l` or uppercase `L` after the value. Example: `long x = 123456789L;` |
| `float` | Append lowercase `f` or uppercase `F` after the value. Example: `float y = 10.5f;` |
| `double` | No suffix needed — Java treats decimal values as `double` by default. |
| `char` | Value must be inside **single quotes**: `'A'`, `'9'`, `'@'` |
| `boolean` | Only `true` or `false` (lowercase). No other value is allowed. |

---

### When to Use float vs double?

- Use **`float`** when you need up to 6-7 decimal digits (e.g., product prices like `99.99`).
- Use **`double`** when you need up to 15-16 decimal digits (e.g., scientific calculations, lab measurements).

```java
float productPrice = 499.99f;          // Sufficient for everyday prices
double chemicalReading = 3.14159265358979; // High precision needed
```

---

## 2. Categories of Non-Primitive Data Types

### What Are Non-Primitive Data Types?

Non-primitive data types (also called **reference types**) are data types that are **not built into the language as keywords** but are created from classes. Unlike primitives, non-primitive variables **store references (addresses) to objects** in memory — not the actual values.

> Everything in Java that is **not** one of the 8 primitive types is a non-primitive data type.

---

### Categories of Non-Primitive Data Types

Non-primitive data types are classified into two types:

#### A. Predefined (Built-in)

Classes, interfaces, and other types **already created by the Java team** and provided for developers to use.

- Example: `String`, `Scanner`, `Math`, `ArrayList`
- You don't write these classes — Java provides them.

#### B. User-defined

Classes, interfaces, and other types **created by the developer** for their application needs.

- Example: `Student`, `Employee`, `Product`
- You write these classes yourself.

---

### Common Non-Primitive Types with Examples

#### 1. String

Used to store text — alphabets, numbers, symbols, or any combination.

```java
String name = "Dileep Singh";
String email = "dileep@gmail.com";
String course = "Java 2024";
```

> String can hold any combination of characters — unlike `char` which holds only one character.

#### 2. Array

Used to store multiple values of the same type in a single variable.

```java
int[] marks = {85, 90, 78, 92, 88};
String[] fruits = {"Apple", "Banana", "Mango"};
```

#### 3. Class

A blueprint for creating objects. Every class you write is itself a data type.

```java
class Student {
    String name;
    int age;
}
```

> Here, `Student` is a user-defined data type.

#### 4. Object

An instance of a class — a real entity created from the blueprint.

```java
Student s1 = new Student();  // s1 is an object of Student class
```

> In `Student s1 = new Student();`:
> - `Student` → data type (class name)
> - `s1` → variable name (object reference)
> - `new Student()` → actual object created in memory

#### 5. Interface

A contract that defines what methods a class must implement (covered in detail later).

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}
```

#### 6. Enum

Used to define a fixed set of constants.

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

Day today = Day.MONDAY;
```

---

### Primitive vs Non-Primitive — Key Differences

| Feature | Primitive | Non-Primitive |
|---------|-----------|---------------|
| Stores | Actual value | Reference (address) to object |
| Defined by | Java language | Java language or Developer |
| Size | Fixed | Varies |
| Default value | 0, false, etc. | `null` |
| Methods | Cannot call methods | Can call methods |
| Examples | `int`, `char`, `boolean` | `String`, `Array`, `Student` |

---

## 3. Data Types and Variables in Java

### What is a Data Type?

A data type tells the compiler:
- **What kind of value** the variable will store
- **How much memory** to allocate for that variable

### What is a Variable?

A variable is a **named container** in memory that stores a value. The value can change during program execution.

---

### Variable Declaration Syntax

```java
dataType variableName = value;
```

- **dataType** → Defines the type of value (int, String, etc.)
- **variableName** → Name given to the memory location
- **value** → The actual data stored (optional at declaration time)

---

### Declaration, Initialization, and Assignment

```java
// Declaration only (no value yet — gets default value in some contexts)
int age;

// Declaration + Initialization (giving value at the time of creation)
int age = 25;

// Assignment (changing value after declaration)
age = 30;
```

---

### Rules for Variable Names

- Must start with a letter, `_`, or `$`
- Cannot start with a number
- Cannot use Java reserved keywords (`int`, `class`, `static`, etc.)
- Java is **case-sensitive** (`age` and `Age` are different variables)
- Use meaningful names: `studentName` is better than `sn`

---

### Types of Variables in Java

Java has **3 types of variables** based on **where they are declared**:

#### 1. Local Variables

- Declared **inside a method or block**
- Only accessible within that method/block
- **Must be initialized** before use (no default value)
- Created when method is called, destroyed when method ends

```java
public class Example {
    public static void main(String[] args) {
        int marks = 95;  // Local variable — exists only inside main()
        System.out.println(marks);
    }
}
```

#### 2. Instance Variables (Non-Static Variables)

- Declared **inside a class but outside all methods**
- **No `static` keyword**
- Each object gets its **own separate copy**
- Initialized with **default values** when an object is created
- Lifetime: exists as long as the object exists

```java
public class Student {
    String name;     // Instance variable
    int age;         // Instance variable

    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Rahul";
        s1.age = 20;

        Student s2 = new Student();
        s2.name = "Priya";
        s2.age = 22;

        System.out.println(s1.name + " - " + s1.age); // Rahul - 20
        System.out.println(s2.name + " - " + s2.age); // Priya - 22
    }
}
```

> Each object (`s1`, `s2`) has its own `name` and `age`. Changing one doesn't affect the other.

#### 3. Static Variables (Class Variables)

- Declared **inside a class but outside all methods**, with the **`static` keyword**
- Only **one copy** exists, shared by all objects
- Stored in **method area** (not heap — not per object)
- Lifetime: exists as long as the class is loaded

```java
public class Student {
    static String collegeName = "ABC College"; // Static variable
    String name;                               // Instance variable

    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Rahul";

        Student s2 = new Student();
        s2.name = "Priya";

        System.out.println(s1.name + " - " + Student.collegeName);
        System.out.println(s2.name + " - " + Student.collegeName);
    }
}
```

---

### Scope and Lifetime Summary

| Variable Type | Where Declared | Scope | Lifetime | Default Value |
|---------------|---------------|-------|----------|---------------|
| Local | Inside method/block | Within that method/block | Method execution | None (must initialize) |
| Instance | Inside class, outside methods (no `static`) | Entire class (via object) | Object's lifetime | Yes (0, null, false, etc.) |
| Static | Inside class, outside methods (with `static`) | Entire class (via class name) | Program's lifetime | Yes (0, null, false, etc.) |

---

## 4. Static vs Non-Static Variables

### What is a Static Variable?

A static variable is declared with the `static` keyword. It belongs to the **class**, not to any specific object. Only **one copy** exists in memory, and it is **shared** among all objects.

```java
static String collegeName = "ABC College";
```

### What is a Non-Static (Instance) Variable?

A non-static variable is declared without the `static` keyword. It belongs to the **object**. Every time you create a new object, a **new copy** is created in memory.

```java
String studentName;
```

---

### Key Differences

| Feature | Static Variable | Non-Static (Instance) Variable |
|---------|----------------|-------------------------------|
| Keyword | Uses `static` | No `static` keyword |
| Belongs to | Class | Object |
| Memory copies | Single copy (shared) | Separate copy per object |
| Stored in | Method Area (Class Area) | Heap Memory (inside object) |
| Access | Using class name: `ClassName.variable` | Using object reference: `obj.variable` |
| Created when | Class is loaded by JVM | Object is created with `new` |
| Use case | Common/shared data | Data unique to each object |

---

### Real-World Analogy

Think of a **college**:
- **College name** → Same for all students → `static`
- **Principal name** → Same for all students → `static`
- **Established year** → Same for all students → `static`
- **Student name** → Different for each student → `non-static`
- **Student ID** → Different for each student → `non-static`
- **Marks** → Different for each student → `non-static`

---

### Complete Java Example

```java
public class CollegeStudent {

    // Static variables — shared by ALL objects (stored once in method area)
    static String collegeName = "ABC College";
    static String principalName = "Dr. Sharma";
    static int establishedYear = 2011;

    // Instance variables — separate copy for EACH object (stored in heap)
    int studentId;
    String name;
    double averageMarks;

    public static void main(String[] args) {

        // Creating first student object
        CollegeStudent s1 = new CollegeStudent();
        s1.studentId = 101;
        s1.name = "Rahul";
        s1.averageMarks = 85.5;

        // Creating second student object
        CollegeStudent s2 = new CollegeStudent();
        s2.studentId = 102;
        s2.name = "Priya";
        s2.averageMarks = 91.3;

        // Printing student details
        System.out.println("--- Student 1 ---");
        System.out.println("Name: " + s1.name);
        System.out.println("ID: " + s1.studentId);
        System.out.println("Average: " + s1.averageMarks);
        System.out.println("College: " + CollegeStudent.collegeName);

        System.out.println("\n--- Student 2 ---");
        System.out.println("Name: " + s2.name);
        System.out.println("ID: " + s2.studentId);
        System.out.println("Average: " + s2.averageMarks);
        System.out.println("College: " + CollegeStudent.collegeName);

        // Changing static variable — affects ALL objects
        System.out.println("\n--- College name changed ---");
        CollegeStudent.collegeName = "XYZ College";

        System.out.println("S1 College: " + CollegeStudent.collegeName); // XYZ College
        System.out.println("S2 College: " + CollegeStudent.collegeName); // XYZ College
    }
}
```

### Output

```
--- Student 1 ---
Name: Rahul
ID: 101
Average: 85.5
College: ABC College

--- Student 2 ---
Name: Priya
ID: 102
Average: 91.3
College: ABC College

--- College name changed ---
S1 College: XYZ College
S2 College: XYZ College
```

---

### Explanation of Output

- `name`, `studentId`, and `averageMarks` are **instance variables** — each object has its own copy. Changing `s1.name` does **not** affect `s2.name`.
- `collegeName` is a **static variable** — only one copy exists. When we changed it to `"XYZ College"`, the change was visible from **all objects** because they all refer to the same single copy.

---

### When to Use Static vs Non-Static?

| Scenario | Use |
|----------|-----|
| Data is **common** for all objects (college name, company name) | `static` |
| Data **changes** from one object to another (student name, marks) | non-static |
| Configuration values or constants | `static` |
| Personal/unique attributes of each entity | non-static |

---

### Memory Diagram (Simplified)

```
┌─────────────────────────────────────────────────────────┐
│                    METHOD AREA                           │
│  (Static variables — single copy)                       │
│                                                         │
│  collegeName = "ABC College"                            │
│  principalName = "Dr. Sharma"                           │
│  establishedYear = 2011                                 │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                     HEAP MEMORY                          │
│  (Objects with instance variables — separate copies)    │
│                                                         │
│  ┌──────────────────┐    ┌──────────────────┐           │
│  │   Object: s1     │    │   Object: s2     │           │
│  │  studentId = 101 │    │  studentId = 102 │           │
│  │  name = "Rahul"  │    │  name = "Priya"  │           │
│  │  avgMarks = 85.5 │    │  avgMarks = 91.3 │           │
│  └──────────────────┘    └──────────────────┘           │
└─────────────────────────────────────────────────────────┘
```

---

## 5. Summary

### Quick Recap

| Topic | Key Takeaway |
|-------|-------------|
| Primitive Types | 8 types — store actual values — fixed memory size |
| Non-Primitive Types | Store references — includes String, Arrays, Classes, etc. |
| Variables | Named memory containers — 3 types: local, instance, static |
| Static Variables | One copy shared by all objects — use for common data |
| Instance Variables | Separate copy per object — use for unique data |
| Local Variables | Exist only inside the method — must be initialized manually |

### Golden Rules

1. **Choose the right data type** — don't use `int` when `byte` is enough.
2. **Append `L` for long values** and **`f` for float values**.
3. **Static = shared, Instance = personal** — decide based on whether data changes per object.
4. **Every class is a data type** and **every object name is a variable**.
5. **Primitive stores value directly**, Non-primitive stores a **reference to the object**.

---

> **Note:** These notes are based on Java SE fundamentals. Practice each example by writing and running the code yourself to build strong understanding.

---
