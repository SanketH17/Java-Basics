# Java Basics 02 — Platform Independence, Classes & Objects

> These notes cover the Java compilation/execution process, platform dependence vs independence, the WORA principle, and the fundamentals of classes and objects in Java.

---

## Table of Contents

1. [Recap — Java Compilation & Execution](#1-recap--java-compilation--execution)
2. [What is a Platform?](#2-what-is-a-platform)
3. [Platform Dependent Languages (C Language Example)](#3-platform-dependent-languages-c-language-example)
4. [Platform Independent Language — Java](#4-platform-independent-language--java)
5. [Write Once, Run Anywhere (WORA)](#5-write-once-run-anywhere-wora)
6. [Introduction to Classes and Objects](#6-introduction-to-classes-and-objects)
7. [Defining a Class in Java](#7-defining-a-class-in-java)
8. [Java Keywords](#8-java-keywords)
9. [Object Creation & the main() Method](#9-object-creation--the-main-method)
10. [Execution Flow of a Java Program](#10-execution-flow-of-a-java-program)
11. [Method Calling Flow in Java](#11-method-calling-flow-in-java)
12. [Java Keywords Revisited — class, interface, enum](#12-java-keywords-revisited--class-interface-enum)
13. [Objects — Identity, State & Behavior](#13-objects--identity-state--behavior)
14. [Variables in Java](#14-variables-in-java)
15. [Data Types in Java](#15-data-types-in-java)
16. [Primitive Data Types (The 8 Basics)](#16-primitive-data-types-the-8-basics)
17. [Compilation vs Runtime — Understanding Error Phases](#17-compilation-vs-runtime--understanding-error-phases)
18. [Printing Output — System.out.println()](#18-printing-output--systemoutprintln)
19. [Code Formatting — A Good Habit](#19-code-formatting--a-good-habit)

---

## 1. Recap — Java Compilation & Execution

Before we dive into new topics, let's quickly revise how a Java program goes from code to output.

### The Journey: Writing Code → Seeing Output

As a Java developer, you write your logic in a file with the **`.java`** extension. But you don't run this file directly. There are **two important steps** in between:

### Step 1 — Compilation

- You use the **Java Compiler** (`javac`) to compile your `.java` file.
- The compiler **validates every line** of your code — it checks whether you followed all the rules and regulations of the Java language.
- Java is a **case-sensitive** language, which means `a` and `A` are treated as **different** characters. The compiler checks this too.
- **If errors are found:** The compiler shows all the errors as a report. You must fix every single error before moving forward.
- **If no errors are found (zero errors):** The compiler creates a **`.class`** file.

### Step 2 — Execution

- The `.class` file contains something called **byte code** — a special format that the Java Virtual Machine (JVM) can understand.
- You use the **`java`** command followed by the file name (without the `.class` extension) to execute the program.
- The **JVM** loads the `.class` file into memory, reads the byte code, executes your logic, and produces the **output**.

### How it looks in practice

```
                 javac                        java
Student.java  ────────►  Student.class  ────────►  Output
 (source code)           (byte code)              (result)
```

### Important Points

- **`javac`** = Java Compiler (validates code and creates `.class` file)
- **`java`** = Starts the Java Runtime Environment / JVM (executes the `.class` file)
- Both `javac` and `java` are executable files found inside the **`bin`** folder of your Java installation directory (e.g., `Program Files/Java/jdk.../bin/`).
- The `.java` file is useful for **writing and editing** your code.
- The `.class` file is what actually **gets executed** to produce the output.
- If you make any changes to your `.java` file, you **must recompile** it to generate a fresh `.class` file with the latest byte code.

---

## 2. What is a Platform?

When we talk about "platform" in this context, we mean:

> **Platform = Operating System (+ Hardware)**

Examples of platforms:

| Platform | Used On |
|----------|---------|
| **Windows** (e.g., Windows 10, 11) | Most PCs and laptops |
| **macOS** | Apple MacBooks and iMacs |
| **Linux** (Ubuntu, Fedora, etc.) | Servers, some desktops |

So when someone says "platform dependent" or "platform independent," they are talking about whether a program is **tied to a specific operating system** or **can run on any operating system**.

---

## 3. Platform Dependent Languages (C Language Example)

### What does "Platform Dependent" mean?

A **platform dependent** language creates compiled output that **only works on the operating system where it was compiled**. You **cannot** take that compiled output and run it directly on a different operating system.

### Example with C Language

Let's say you write a C program called `student.c`.

#### Scenario: Compile on Windows

```
student.c  ──► C Compiler (on Windows) ──► student.exe (Windows executable)
```

- This `.exe` file **works only on Windows**.
- If you copy `student.exe` to a Mac or Linux computer, **it will NOT work**.

#### What if you want to run on macOS?

```
student.c  ──► C Compiler (on macOS) ──► student (Mac executable, e.g., .dmg format)
```

- You must take the **original source code** (`student.c`) to the Mac.
- You must **recompile** it using the C compiler installed on macOS.
- The new compiled output works **only on macOS** — not on Windows or Linux.

#### What if you want to run on Linux?

```
student.c  ──► C Compiler (on Linux) ──► student (Linux executable)
```

- Again, you must **recompile** the source code on the Linux machine.
- The output works **only on Linux**.

### The Problem

Every time you switch to a different operating system, you have to:

1. Take the original source code.
2. Recompile it on the new operating system.
3. Only then can you execute it.

This is a **lot of extra work** and is called **platform dependency**.

### Real-Life Analogy

Imagine you have a charger that only works with Indian power sockets. If you travel to the USA, you need a different charger or an adapter. The charger is "dependent" on the type of socket (platform). That's inconvenient!

---

## 4. Platform Independent Language — Java

### What does "Platform Independent" mean?

A **platform independent** language lets you **compile your code once** on any operating system, and then **run the compiled output on any other operating system** — without recompilation.

### How Java Achieves Platform Independence

The secret is the **byte code** and the **JVM (Java Virtual Machine)**.

#### Step-by-Step:

1. You write your Java source code in a `.java` file (on any OS — say Windows).
2. You compile it using `javac` → a `.class` file is created containing **byte code**.
3. This byte code is **NOT specific to any operating system**. It is a universal format that any JVM can understand.
4. Now, you can take this `.class` file to **any computer** — Windows, macOS, or Linux.
5. As long as that computer has **Java (JVM) installed**, the JVM will read the byte code and execute it.
6. **No recompilation needed!**

```
                     javac (on Windows)
Student.java  ─────────────────────────►  Student.class (byte code)
                                              │
                    ┌─────────────────────────┼─────────────────────────┐
                    │                         │                         │
                    ▼                         ▼                         ▼
             JVM on Windows            JVM on macOS             JVM on Linux
                    │                         │                         │
                    ▼                         ▼                         ▼
                 Output ✓                  Output ✓                 Output ✓
```

### Why does this work?

- The `.class` file contains **byte code**, not machine-specific code.
- **Byte code** is a special intermediate language understood by the JVM.
- Every operating system has its **own version of the JVM**, but all JVMs understand the **same byte code**.
- So the developer compiles once, and the JVM on each OS takes care of the rest.

### Key Insight

> **The `.class` file is the hero of platform independence.** It acts as a bridge between your source code and any operating system.

### Java Software Downloads for Different Platforms

When you download Java, you pick the version for your OS:

| Operating System | Java Installer Format |
|------------------|-----------------------|
| Windows | `.exe` |
| macOS | `.dmg` |
| Linux | `.tar.gz`, `.deb`, `.rpm` |

Even though the **installer** is different for each OS, once Java is installed, the **JVM inside works the same way** — it can read and execute any `.class` file.

---

## 5. Write Once, Run Anywhere (WORA)

### What is WORA?

**WORA** stands for **Write Once, Run Anywhere**. It is a principle that Java follows.

### What it means in simple words:

- **Write** your Java source code **once** (on any operating system).
- **Compile** it **once** to get the `.class` file.
- **Run** that `.class` file on **any operating system** where Java (JVM) is installed — without changing or recompiling your code.

### WORA vs Platform Dependency — Comparison

| Feature | C Language (Platform Dependent) | Java (Platform Independent — WORA) |
|---------|-------------------------------|--------------------------------------|
| Compiled output | OS-specific executable | Universal byte code (`.class`) |
| Run on other OS? | No — must recompile | Yes — just need JVM |
| Extra work for new OS? | Recompile source code every time | No extra work |
| Key enabler | OS-specific compiler | JVM + byte code |

### Important Points to Remember

- Java's platform independence is possible because of **byte code** and the **JVM**.
- The `.java` file is needed for writing and compiling. After compilation, only the `.class` file matters for execution.
- WORA does **not** mean Java doesn't need to be installed. The target machine **must** have Java (JVM) installed.

---

## 6. Introduction to Classes and Objects

### Real-Life Analogy — Car Manufacturing

Before a car company makes a single car, they go through a detailed process:

1. **Gather requirements** — What kind of car do they want to build?
2. **Design** — Create blueprints and plans.
3. **Define features** — Speed, color options, seating, engine type, etc.
4. **Define behavior** — How fast can it go? What happens when you brake?
5. **Build the car** — Using the plan, they manufacture actual cars.

Now here's the key point:

- The **plan/blueprint** is created **once**.
- From that **one plan**, they manufacture **thousands or millions** of cars.
- Every car follows the **same design**, but each car can have small differences (e.g., color, license plate).

> **The plan/blueprint = Class**
> **Each actual car = Object**

### Another Real-Life Example — iPhone Manufacturing

When Apple releases the iPhone 16 Pro:
- They spend months designing it — defining features, behavior, appearance.
- This design is the **blueprint** (Class).
- From that one design, they produce **millions of identical iPhones** (Objects).
- Every iPhone 16 Pro in the world looks and works the same — because they all came from the same blueprint.

### What is a Class?

A **class** in Java is like a **blueprint** or a **plan**. It defines:

- **What data** an object will hold (called **variables** or **fields**)
- **What actions** an object can perform (called **methods**)
- **How** an object is created (called **constructors**)

A class itself is **not** the real thing — it's just the description. You need to create **objects** from the class to actually do something.

### What is an Object?

An **object** is a **real instance** created from a class. It actually exists in memory and can:

- Hold real data
- Perform actions
- Interact with other objects

### Class vs Object — Simple Comparison

| Class (Blueprint) | Object (Real Thing) |
|--------------------|---------------------|
| Car design plan | An actual car you can drive |
| iPhone blueprint | A real iPhone in your hand |
| Recipe for a cake | An actual cake you can eat |
| Java code that defines structure | A real entity created in memory during execution |

### Key Points

- **Without a class, you cannot create an object** in Java.
- From **one class**, you can create **multiple objects**.
- Every object follows the structure defined by its class, but can have its own unique data (e.g., different color, name, etc.).
- Java is called an **Object-Oriented Programming (OOP)** language because everything revolves around objects.

### Everything is an Object

In real life, everything you can see, touch, or interact with is an object — a laptop, a car, a phone, a person. Similarly, in Java, you model real-world things as objects. That's why it's called **Object-Oriented**.

---

## 7. Defining a Class in Java

### Syntax (Template) for a Java Class

```java
public class ClassName {
    // Your logic goes here
}
```

Let's break this down word by word:

| Part | What it means |
|------|---------------|
| `public` | An **access specifier** (keyword) — it means this class is accessible from anywhere. Don't worry about the details now; you'll learn more later. |
| `class` | A **keyword** that tells Java: "I am defining a class." |
| `ClassName` | The **name** you give to your class. You choose this name. |
| `{ }` | **Curly braces** — they mark the **start** and **end** of the class body. |

### What is a Syntax?

"Syntax" simply means **template** or **formula**. It's the predefined structure you must follow. Think of it like a math formula:

```
A + B = ?
```

You follow the formula and plug in your values. Similarly, in Java, you follow the class syntax and plug in your class name and logic.


### Rule: File Name = Class Name

#### Example:

- If your file is named **`Student.java`**, then your class must be:

```java
public class Student {
    // logic here
}
```

- If your file is named **`MyApp.java`**, then your class must be:

```java
public class MyApp {
    // logic here
}
```

- ❌ **Wrong:** File is `Student.java` but class is `student` (lowercase 's') — **will cause an error** because Java is case-sensitive!

### What Goes Inside a Class?

A class can contain several things (you'll learn each one step by step):

| Component | What it is |
|-----------|------------|
| **Variables** | Store data (e.g., name, age, color) |
| **Methods** | Define actions/behavior (e.g., drive, brake, accelerate) |
| **Constructors** | Special methods used to create objects |
| **Static blocks** | Code that runs when the class is loaded |
| **Instance blocks** | Code that runs when an object is created |

### Complete Example

**File name:** `Student.java`

```java
public class Student {
    // This is where you will write all your logic
    // Variables, methods, constructors, etc.
}
```

---

## 8. Java Keywords

### What are Keywords?

**Keywords** are special words that are **reserved by the Java language** for specific purposes. You cannot use them for anything else (like naming your variables or classes).

### Key Facts about Keywords

- Java has approximately **50 keywords**.
- Each keyword has a **fixed, specific purpose** in the language.
- Keywords are always written in **lowercase** (e.g., `public`, `class`, `static`, `void`).
- You'll learn different keywords as you learn different concepts — you won't memorize all 50 at once.

### Real-Life Analogy

Think of the word "car." When someone says "car," your mind immediately pictures a vehicle with four wheels. You don't think of a bicycle. Similarly, when Java sees the word `class`, it knows you're defining a class — not a variable or a method.

### Keywords We've Seen So Far

| Keyword | Purpose |
|---------|---------|
| `public` | Access specifier — makes the class/method accessible from anywhere |
| `class` | Used to define/declare a class |
| `static` | (Coming soon) — belongs to the class, not to an object |
| `void` | (Coming soon) — means a method returns nothing |

### Important Rule

Since Java is **case-sensitive**, keywords must be typed in **exact lowercase**:

- ✅ `public` — Correct
- ❌ `Public` — Wrong (Java won't recognize it as a keyword)
- ❌ `PUBLIC` — Wrong

---

## 9. Object Creation & the main() Method

### Who Creates the Object?

You (the developer) **write the code** that tells Java to create an object. But the actual creation happens at **runtime** — when the program is being executed by the JVM.

So:

- **Developer** → writes the logic for object creation
- **JVM** → actually creates the object in memory when the program runs

### How Many Objects Can You Create?

From **one class**, you can create **as many objects as you need** — 1, 10, 100, or even millions. It depends on your requirement.

### What is the `main()` Method?

In Java, every program needs a **starting point** — a place where the JVM knows to begin execution. That starting point is the **`main()` method**.

#### Syntax of the main() Method

```java
public static void main(String[] args) {
    // Your program starts executing from here
}
```

Let's understand each word (high-level overview — details will come in later topics):

| Word | Meaning |
|------|---------|
| `public` | Accessible from anywhere (JVM needs to access it) |
| `static` | Can be called without creating an object (JVM calls it directly) |
| `void` | This method does not return any value |
| `main` | The name of the method — JVM looks for exactly this name |
| `String[] args` | Can accept command-line arguments (don't worry about this for now) |

### Why is `main()` Important?

- The JVM **always looks for the `main()` method** as the entry point of your program.
- Without `main()`, the JVM doesn't know where to start, and your program **won't run**.
- All your initial logic — including object creation — starts from inside `main()`.

---

## 10. Execution Flow of a Java Program

### Putting It All Together

Here's the complete journey of a Java program from start to finish:

#### Step 1 — Write the Source Code

Create a `.java` file and write your class with the `main()` method.

```java
public class Student {
    public static void main(String[] args) {
        System.out.println("Hello, I am learning Java!");
    }
}
```

#### Step 2 — Compile

Open your terminal/command prompt and run:

```
javac Student.java
```

- The compiler checks your code for errors.
- If everything is correct, it creates `Student.class` (byte code).

#### Step 3 — Execute

Run the program using:

```
java Student
```

- Notice: you type `Student`, **not** `Student.class`.
- The JVM loads `Student.class`, finds the `main()` method, and starts executing the code inside it.

#### Step 4 — See the Output

```
Hello, I am learning Java!
```

### Visual Flow

```
 ┌─────────────────────────────────┐
 │   1. Write code in Student.java │
 └──────────────┬──────────────────┘
                │
                ▼
 ┌─────────────────────────────────┐
 │   2. Compile: javac Student.java│
 │      → Student.class created    │
 └──────────────┬──────────────────┘
                │
                ▼
 ┌─────────────────────────────────┐
 │   3. Execute: java Student      │
 │      → JVM loads .class file    │
 │      → Finds main() method     │
 │      → Executes the logic       │
 └──────────────┬──────────────────┘
                │
                ▼
 ┌─────────────────────────────────┐
 │   4. Output is displayed        │
 │      "Hello, I am learning Java!"│
 └─────────────────────────────────┘
```

### Complete Example — Step by Step

**File name:** `HelloWorld.java`

```java
public class HelloWorld {
    public static void main(String[] args) {
        // This line prints text to the screen
        System.out.println("Welcome to Java Programming!");

        // You can print multiple lines
        System.out.println("Java is platform independent.");
        System.out.println("Write Once, Run Anywhere!");
    }
}
```

**Compile and Run:**

```bash
javac HelloWorld.java
java HelloWorld
```

**Output:**

```
Welcome to Java Programming!
Java is platform independent.
Write Once, Run Anywhere!
```

**Code Explanation:**

- `public class HelloWorld` — defines a class named `HelloWorld` (must match file name).
- `public static void main(String[] args)` — the entry point of the program.
- `System.out.println(...)` — prints text to the console followed by a new line.
- `//` — starts a single-line comment (ignored by the compiler, helps humans understand the code).

---

## Common Mistakes Beginners Make

| Mistake | Why It's Wrong | Fix |
|---------|---------------|-----|
| File name doesn't match class name | Java requires them to be the same | Rename the file or the class to match |
| Using uppercase for keywords (`Class`, `Public`) | Java keywords are lowercase and case-sensitive | Always use `class`, `public`, `static`, etc. |
| Forgetting to recompile after changes | The `.class` file still has the old byte code | Always run `javac` again after editing `.java` |
| Writing `java Student.class` instead of `java Student` | The `java` command doesn't need the `.class` extension | Use just the class name: `java Student` |
| Missing curly braces `{ }` | The compiler won't know where the class/method starts and ends | Always use matching `{` and `}` pairs |
| Missing semicolons `;` | Java statements must end with a semicolon | Add `;` at the end of each statement |

---

## Quick Revision — Important Points to Remember

1. **Java compilation** creates a `.class` file containing **byte code**.
2. **Byte code** is a universal format understood by the **JVM** on any operating system.
3. **Platform dependent** (like C) = compiled output works only on the OS where it was compiled.
4. **Platform independent** (like Java) = compiled `.class` file works on **any OS** with a JVM.
5. **WORA** = Write Once, Run Anywhere.
6. **Class** = Blueprint/plan that defines structure and behavior.
7. **Object** = A real instance created from a class.
8. From **one class**, you can create **multiple objects**.
9. **Keywords** are reserved words in Java (e.g., `public`, `class`, `static`, `void`) — always lowercase.
10. **File name must match the class name** (case-sensitive).
11. **`main()` method** is the entry point — the JVM starts execution from here.
12. **`javac`** = compile, **`java`** = execute.

---

## 11. Method Calling Flow in Java

When a Java program has multiple methods, the JVM follows a specific order when executing them.

### How it works

1. Execution **always starts** from the `main()` method.
2. The JVM executes code **line by line** inside `main()`.
3. When a line **calls another method**, the JVM **jumps** to that method and starts executing it line by line.
4. Once that method finishes, the JVM **returns** to the exact line after the method call and continues.
5. If the called method itself calls another method, the same jump-and-return happens again.
6. Execution **always ends** back in the `main()` method.

### Example Flow

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("Line 1");       // 1st
        System.out.println("Line 2");       // 2nd
        m1();                                // 3rd → jumps to m1()
        System.out.println("Line 5");       // 6th (after m1 finishes)
    }

    static void m1() {
        System.out.println("Line 3");       // 4th
        System.out.println("Line 4");       // 5th
    }
}
```

### Key Takeaway

> The JVM always starts from `main()` and always terminates from `main()`. It follows the call chain in and out like a stack — the last method entered is the first one exited.

---

## 12. Java Keywords Revisited — class, interface, enum

Java uses **keywords** to understand what the developer is creating. Based on the keyword, Java applies the corresponding rules and functionalities.

| Keyword | What It Creates | Example |
|---------|----------------|---------|
| `class` | A class | `class Student { }` |
| `interface` | An interface | `interface Printable { }` |
| `enum` | An enumeration | `enum Day { MON, TUE, WED }` |

- Each has its **own set of rules** and features that Java applies internally.
- You will learn `interface` and `enum` in detail later — for now, just know that Java distinguishes them by their keyword.

---

## 13. Objects — Identity, State & Behavior

Every object (both in real life and in Java) has three fundamental aspects:

| Aspect | Meaning | Real-Life Example | Java Equivalent |
|--------|---------|-------------------|-----------------|
| **Identity** | A unique identifier to distinguish one object from another | Student ID, Employee ID, Email ID | Object reference name |
| **State** | The data/characteristics that describe the object | Name, age, gender, height, weight | Variables (fields) |
| **Behavior** | The actions the object can perform | Dance, code, teach, play cricket | Methods |

### Identity

- Every object needs something **unique** to tell it apart from others.
- In real life: student IDs, email addresses, phone numbers.
- In Java: the variable name you use when creating an object (e.g., `s1`, `s2`).

### State

- State describes **what the object looks like** or **what information it holds**.
- Two students may have different names, ages, and genders — that means their **state is different**.
- In Java, state is defined by **variables** inside a class.

```java
class Student {
    int id;
    String name;
    String gender;
    int age;
}
```

### Behavior

- Behavior defines **what the object can do** — its actions.
- One student might be good at dancing, another at coding — their **behavior differs**.
- In Java, behavior is defined by **methods** inside a class.

```java
class Student {
    // State
    int id;
    String name;

    // Behavior
    void study() {
        // logic for studying
    }

    void play() {
        // logic for playing
    }
}
```

### How They Connect

- **Behavior depends on state.** Methods use variables to perform their logic.
- For example, a method that calculates EMI uses variables like `principal`, `time`, and `rateOfInterest`.

```java
// Variables define state
int principal = 100000;
int time = 5;
double rate = 8.5;

// Method defines behavior (uses state to perform an action)
double emi = (principal * time * rate) / 100;
```

### Different Objects = Different State + Different Behavior

```java
Student s1 = new Student();   // Identity: s1
// s1 → id=1, name="Dilip", gender="Male"

Student s2 = new Student();   // Identity: s2
// s2 → id=2, name="Veena", gender="Female"
```

`s1` and `s2` are two **different objects** — they have different identities and different states.

---

## 14. Variables in Java

### What is a Variable?

A variable is a **named reference to a memory location** where a real value is stored.

Think of it this way:

| Concept | Explanation |
|---------|-------------|
| **Computer memory** | Where values are actually stored (RAM) |
| **Memory address** | A complex, unreadable address that the computer uses internally |
| **Variable** | A simple, human-readable name that **points to** that memory location |

### Why Do We Need Variables?

When Java stores a value (say `30`) in computer memory, it goes to a specific memory address (something like `0xA3F2B1`). As humans, we **cannot remember** these addresses.

Variables solve this problem — instead of dealing with memory addresses, we use meaningful names like `age`, `name`, or `price`.

```
Variable "age"  ──points to──►  Memory Address 0xA3F2B1  ──contains──►  Value: 30
```

When you write `age`, Java internally:
1. Goes to the variable `age`
2. Finds the memory address it references
3. Retrieves the value `30` from that location

### Two Common Definitions

1. **Technical:** A variable is a reference to a memory location where the real value is stored.
2. **Simple:** A variable is a container that holds some value.

Both mean the same thing — just different levels of detail.

### Syntax for Declaring Variables

**With a value (initialization):**

```java
dataType variableName = value;
```

```java
int age = 30;
```

**Without a value (declaration only):**

```java
dataType variableName;
```

```java
int age;
```

You can assign the value later:

```java
int age;
// ... some logic ...
age = 30;    // assigned later
```

### Reassigning a Variable

When you assign a new value to an existing variable, the **old value is replaced**.

```java
int a = 30;    // memory stores 30
a = 100;       // memory now stores 100 (30 is replaced)
```

### Variable Naming Rules

| Rule | Example |
|------|---------|
| Variable names **cannot contain spaces** | ❌ `my age` → ✅ `myAge` |
| Names are **developer's choice** (you pick meaningful names) | `age`, `studentName`, `totalPrice` |
| Must **declare before using** — you cannot use a variable that hasn't been created | See below |
| Java is **case-sensitive** — `age`, `Age`, and `AGE` are three different variables | Be consistent |

### You Must Declare Before You Use

```java
// ❌ This will cause a COMPILE-TIME error
System.out.println(b);    // Error: "cannot find symbol" — b was never declared

// ✅ Correct — declare first, then use
int b = 50;
System.out.println(b);    // prints 50
```

The compiler checks: "Does this variable exist?" If not, it throws an error and **refuses to create the `.class` file**.

---

## 15. Data Types in Java

### What is a Data Type?

A data type tells Java **what kind of value** a variable will store. Just like in real life — a name holds text, an age holds a number, a price might hold a decimal number.

> **Data Type = Type of Data**

### Two Categories

Java divides data types into:

1. **Primitive Data Types** — basic, simple, built-in types (8 total)
2. **Non-Primitive Data Types** — complex types like `String`, arrays, classes (covered later)

---

## 16. Primitive Data Types (The 8 Basics)

Java has exactly **8 primitive data types**. They are all **keywords** (reserved, lowercase).

### Overview Table

| # | Data Type | What It Stores | Example |
|---|-----------|----------------|---------|
| 1 | `byte` | Small whole numbers | `byte age = 25;` |
| 2 | `short` | Medium whole numbers | `short year = 2024;` |
| 3 | `int` | Standard whole numbers | `int salary = 50000;` |
| 4 | `long` | Very large whole numbers | `long population = 140000000L;` |
| 5 | `float` | Decimal numbers (less precision) | `float pi = 3.14f;` |
| 6 | `double` | Decimal numbers (more precision) | `double price = 99.99;` |
| 7 | `char` | A single character | `char grade = 'A';` |
| 8 | `boolean` | `true` or `false` only | `boolean passed = true;` |

### Grouping by Purpose

```
Primitive Data Types (8)
├── Numeric — Whole Numbers (no decimals)
│   ├── byte
│   ├── short
│   ├── int
│   └── long
├── Numeric — Decimal Numbers (with precision)
│   ├── float
│   └── double
├── Character
│   └── char
└── Logical
    └── boolean
```

### Why 4 Types for Whole Numbers?

All four (`byte`, `short`, `int`, `long`) store plain numbers without decimals. So why not just one?

**The answer: Memory management.**

Each type uses a **different amount of memory**. Choosing the right type based on your data saves memory, which improves performance.

> **More memory used → Lower performance**
> **Less memory used → Better performance**

### How to Choose the Right Type

Think about the **realistic range of values** your variable will hold:

| Scenario | Possible Values | Best Choice |
|----------|----------------|-------------|
| A person's age | 0–150 | `byte` (small range is enough) |
| Birth year | 1900–2100 | `short` (a few thousand) |
| Mobile number (10 digits) | Up to ~9,999,999,999 | `long` (too large for `int`) |
| Country population | Billions | `long` |
| A simple counter | 0–100,000 | `int` |

> Always think: **"What is the maximum realistic value this variable will ever hold?"** Then pick the smallest data type that fits.

### When to Use `float` / `double`

If your values have **decimal points** (e.g., `89.99`, `3.14159`), the four integer types (`byte`, `short`, `int`, `long`) **cannot** store them. You must use `float` or `double`.

```java
// ❌ Invalid — int cannot hold decimals
int price = 89.99;

// ✅ Valid
double price = 89.99;
```

---

## 17. Compilation vs Runtime — Understanding Error Phases

When working with Java, errors can occur at two different phases:

### Phase 1 — Compilation (using `javac`)

- The **compiler** checks your code for **syntax and rule violations**.
- Examples: missing semicolons, undeclared variables, wrong keywords.
- If errors are found → **no `.class` file is created** → you cannot run the program.
- These are called **compile-time errors**.

### Phase 2 — Runtime (using `java`)

- The **JVM** executes your code.
- Some errors only appear when the program is actually running (e.g., dividing by zero, accessing invalid data).
- These are called **runtime errors** or **exceptions**.

### Key Difference

| | Compile-Time Error | Runtime Error |
|-|--------------------|---------------|
| **When?** | During compilation (`javac`) | During execution (`java`) |
| **Who catches it?** | The compiler | The JVM |
| **Can you run the program?** | No — `.class` file is not created | Yes, but it crashes at the error |
| **Example** | Using an undeclared variable | Dividing a number by zero |

---

## 18. Printing Output — `System.out.println()`

To display values or messages on the screen (console), use:

```java
System.out.println("Hello World");
```

| Part | Meaning |
|------|---------|
| `System` | A built-in Java class (note the capital `S`) |
| `out` | An output stream object inside `System` |
| `println` | A method that **prints** the value and moves to the **next line** |
| `(...)` | Parentheses — you put the value to print inside here |

### Printing Variable Values

```java
int age = 25;
System.out.println(age);    // prints: 25

int a = 100;
int b = 50;
int c = a + b;
System.out.println(c);      // prints: 150
```

---

## 19. Code Formatting — A Good Habit

Java doesn't care about extra spaces or indentation — your code will compile either way. But **formatting matters for readability**.

### Bad Formatting (works, but hard to read)

```java
public class Demo{public static void main(String[] args){System.out.println("Hello");}}
```

### Good Formatting (easy to read and debug)

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

### Best Practices

- Use **one tab of indentation** for each level of nesting.
- Each opening `{` should have a matching closing `}` at the same indentation level.
- Write **one statement per line**.
- Start building this habit now — it becomes critical in larger programs.

---

## Quick Revision — Sessions 09 & 10

1. **Method calling flow**: JVM starts from `main()`, jumps to called methods, and returns after each method finishes. Always starts and ends in `main()`.
2. **Every object has three aspects**: Identity (unique name), State (data/variables), and Behavior (actions/methods).
3. **Variables define the state** of an object. **Methods define the behavior**.
4. A **variable** is a named reference to a memory location — it lets you work with values without worrying about memory addresses.
5. You must **declare a variable before using it**, or the compiler will throw an error.
6. Variable names **cannot have spaces**, are **developer's choice**, and are **case-sensitive**.
7. **Data types** tell Java what kind of value a variable stores.
8. Java has **8 primitive data types**: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.
9. Four integer types exist for **memory optimization** — pick the smallest type that fits your data range.
10. Use `float`/`double` for decimal values. Use `char` for a single character. Use `boolean` for true/false.
11. **Compile-time errors** are caught by the compiler; **runtime errors** occur during execution.
12. `System.out.println()` prints output to the console.
13. **Code formatting** doesn't affect compilation but is essential for readability.

---
