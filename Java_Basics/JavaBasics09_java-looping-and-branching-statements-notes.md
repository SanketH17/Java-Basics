# Looping and Branching Statements in Java

## 1. Introduction

In Java, **control flow statements** determine the order in which statements are executed. By default, Java executes code line by line (top to bottom). Control flow statements allow you to change this default behavior.

Control flow statements are divided into three categories:

1. **Decision-making statements** – Execute specific logic based on a condition (e.g., `if`, `if-else`, `switch`).
2. **Looping statements (Iteration statements)** – Execute logic repeatedly until a condition is satisfied.
3. **Branching statements (Jumping statements)** – Transfer control from one point to another unconditionally.

This document covers **Looping Statements** and **Branching Statements**.

---

## 2. Looping Statements in Java

Looping statements are used when you want to **execute a block of code repeatedly** until a condition becomes false.

- **Decision-making statements** → Execute logic based on a condition (once).
- **Looping statements** → Execute logic **repeatedly** until a condition is broken.

Java provides the following loop types:

| Loop Type | Description |
|-----------|-------------|
| `for` | Used when the number of iterations is known |
| `while` | Used when the number of iterations is not known in advance |
| `do-while` | Similar to while, but executes at least once |
| Enhanced `for` (for-each) | Used to iterate over arrays or collections |

> **Note:** From Java 8 onwards, the Stream API has reduced the usage of traditional loops in real-time applications. However, knowledge of loops is still essential for interviews, written exams, and understanding core programming concepts.

---

### 2.1 for Loop

#### Definition

The `for` loop is used when you **know in advance** how many times you want to execute a block of code. All three components (initialization, condition, update) are defined in a single line.

#### Syntax

```java
for (initialization; condition; increment/decrement) {
    // logic to execute repeatedly
}
```

#### Components Explained

| Component | Purpose |
|-----------|---------|
| **Initialization** | Defines the starting value (executed only once) |
| **Condition** | Checked before each iteration; loop runs while `true` |
| **Increment/Decrement** | Updates the variable after each iteration |

#### Execution Flow

1. Initialization happens **only once**.
2. Condition is checked — if `true`, the body executes.
3. After body execution, the increment/decrement operation runs.
4. Steps 2–3 repeat until the condition becomes `false`.
5. When condition is `false`, the loop exits.

#### Simple Example

```java
public class ForLoopExample {
    public static void main(String[] args) {
        // Print numbers from 1 to 5
        for (int i = 1; i <= 5; i++) {
            System.out.println("Value: " + i);
        }
    }
}
```

#### Output

```
Value: 1
Value: 2
Value: 3
Value: 4
Value: 5
```

#### Decrement Example

```java
public class ForLoopDecrement {
    public static void main(String[] args) {
        // Print numbers from 5 to 1 (backward)
        for (int i = 5; i >= 1; i--) {
            System.out.println("Value: " + i);
        }
    }
}
```

#### Output

```
Value: 5
Value: 4
Value: 3
Value: 2
Value: 1
```

#### When to Use a for Loop

- When you know the **exact number of iterations** in advance.
- When initialization, condition, and update are straightforward.
- When the loop variable is **not needed outside** the loop.

#### Important Point

The variable declared inside the `for` loop (e.g., `int i`) is a **local variable** of the for loop. It **cannot be accessed outside** the loop.

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i); // works fine
}
// System.out.println(i); // ERROR: 'i' cannot be resolved
```

---

### 2.2 while Loop

#### Definition

The `while` loop is used when you want to execute a block of code repeatedly, but the **number of iterations is not known** in advance. The condition is checked **before** each iteration.

#### Syntax

```java
// Initialization (before the loop)
int variable = startingValue;

while (condition) {
    // logic to execute repeatedly
    // increment or decrement (inside the body)
}
```

#### Key Difference from for Loop

| Aspect | for Loop | while Loop |
|--------|----------|------------|
| Initialization | Inside the for statement | Outside (before) the loop |
| Condition | Inside the for statement | Inside the while parentheses |
| Increment/Decrement | Inside the for statement | Inside the loop body |
| Variable scope | Local to the for loop | Accessible outside the loop |

#### Simple Example

```java
public class WhileLoopExample {
    public static void main(String[] args) {
        int i = 1; // initialization outside

        while (i <= 5) { // condition
            System.out.println("Value: " + i);
            i++; // increment inside the body
        }

        // Variable 'i' is accessible here
        System.out.println("Final value of i: " + i);
    }
}
```

#### Output

```
Value: 1
Value: 2
Value: 3
Value: 4
Value: 5
Final value of i: 6
```

#### When to Use a while Loop

- When the **starting value comes from an external source** (e.g., another method).
- When you need to **access the loop variable after** the loop finishes.
- When you need the **last incremented/decremented value** outside the loop.
- When the number of iterations depends on a dynamic condition.

#### Example: Variable from External Method

```java
public class WhileLoopExternal {

    public static int getStartingValue() {
        return 5; // value coming from some logic
    }

    public static void main(String[] args) {
        int value = getStartingValue(); // initialization from external method

        while (value <= 10) {
            System.out.println("Value: " + value);
            value++;
        }

        // Can use 'value' after the loop
        System.out.println("Last value after loop: " + value);
    }
}
```

#### Output

```
Value: 5
Value: 6
Value: 7
Value: 8
Value: 9
Value: 10
Last value after loop: 11
```

---

### 2.3 do-while Loop

#### Definition

The `do-while` loop is similar to the `while` loop, but it **executes the body at least once** before checking the condition. The condition is evaluated **after** the body executes.

#### Syntax

```java
// Initialization
int variable = startingValue;

do {
    // logic to execute
    // increment or decrement
} while (condition); // semicolon is mandatory
```

#### Simple Example

```java
public class DoWhileExample {
    public static void main(String[] args) {
        int i = 1;

        do {
            System.out.println("Value: " + i);
            i++;
        } while (i <= 5);
    }
}
```

#### Output

```
Value: 1
Value: 2
Value: 3
Value: 4
Value: 5
```

#### Important Point: Executes at Least Once

Even if the condition is `false` from the start, the body executes **at least once**.

```java
public class DoWhileOnce {
    public static void main(String[] args) {
        int i = 10;

        do {
            System.out.println("Value: " + i); // executes once
            i++;
        } while (i <= 5); // condition is false from start
    }
}
```

#### Output

```
Value: 10
```

#### Difference Between while and do-while

| Aspect | while | do-while |
|--------|-------|----------|
| Condition check | **Before** body execution | **After** body execution |
| Minimum execution | 0 times (if condition is false) | **At least 1 time** |
| Semicolon | Not required after condition | Required after `while(condition);` |
| Use case | When execution depends on condition | When body must run at least once |

#### When to Use a do-while Loop

- When the logic **must execute at least once**, regardless of the condition.
- Common use case: menu-driven programs where you show the menu at least once.

---

### 2.4 Enhanced for Loop / for-each Loop

#### Definition

The enhanced for loop (also called **for-each loop**) is a simplified way to iterate over arrays or collections. It was introduced in **Java 5**.

> **Note:** The enhanced for loop is best understood after learning arrays and collections.

#### Syntax

```java
for (dataType variable : arrayOrCollection) {
    // logic using variable
}
```

#### Simple Example Using an Array

```java
public class ForEachExample {
    public static void main(String[] args) {
        int[] numbers = {10, 20, 30, 40, 50};

        for (int num : numbers) {
            System.out.println("Value: " + num);
        }
    }
}
```

#### Output

```
Value: 10
Value: 20
Value: 30
Value: 40
Value: 50
```

#### When to Use Enhanced for Loop

- When you want to **iterate over all elements** of an array or collection.
- When you **don't need the index** of elements.
- When you want cleaner and more readable code.

#### Limitation

- You **cannot modify** the array/collection elements directly.
- You **don't have access** to the index of the current element.

---

## 3. Branching Statements in Java

Branching statements (also called **jumping statements**) are used to **transfer control** of program execution **unconditionally** from one point to another.

Key points:
- These statements do **not** require a condition to execute.
- They are mostly used **inside loops** and **switch statements**.
- They change the normal sequential flow of execution.

Java provides three branching statements:

| Statement | Purpose |
|-----------|---------|
| `break` | Exit/terminate the loop or switch immediately |
| `continue` | Skip current iteration and move to the next |
| `return` | Exit from a method |

---

### 3.1 break Statement

#### Definition

The `break` statement is used to **immediately terminate** the execution of a loop or switch statement. When JVM encounters `break`, it exits the loop/switch block without executing the remaining iterations or cases.

#### How It Works

- In a **loop**: Exits the loop entirely, skipping all remaining iterations.
- In a **switch**: Exits the switch block, preventing fall-through to other cases.

#### Simple Example: break in a Loop

```java
public class BreakExample {
    public static void main(String[] args) {
        // Find value 5 from 1 to 10
        for (int i = 1; i <= 10; i++) {
            if (i == 5) {
                System.out.println("Value 5 found! Breaking the loop.");
                break; // exit the loop immediately
            }
            System.out.println("Checking: " + i);
        }
        System.out.println("Loop ended.");
    }
}
```

#### Output

```
Checking: 1
Checking: 2
Checking: 3
Checking: 4
Value 5 found! Breaking the loop.
Loop ended.
```

#### Use Case

When you are **searching for a value** in a group of values, and once you find it, there is no need to check the remaining values. You tell the JVM: "I found my value, please stop iterating."

---

### 3.2 continue Statement

#### Definition

The `continue` statement is used to **skip the current iteration** and move to the **next iteration** of the loop. Unlike `break`, it does **not** exit the loop — it only skips the rest of the current round.

#### How It Works

- Skips all remaining statements in the current iteration.
- Moves control to the next iteration (next value).
- The loop **continues** executing with the next value.

#### Simple Example: Skip Odd Numbers

```java
public class ContinueExample {
    public static void main(String[] args) {
        // Print only even numbers from 1 to 10
        for (int i = 1; i <= 10; i++) {
            if (i % 2 != 0) {
                continue; // skip odd numbers
            }
            System.out.println("Even number: " + i);
        }
    }
}
```

#### Output

```
Even number: 2
Even number: 4
Even number: 6
Even number: 8
Even number: 10
```

#### How It Works Step-by-Step

1. `i = 1` → 1 % 2 != 0 → `true` → `continue` → skip, move to next value.
2. `i = 2` → 2 % 2 != 0 → `false` → print "Even number: 2".
3. `i = 3` → 3 % 2 != 0 → `true` → `continue` → skip, move to next value.
4. And so on...

---

### 3.3 return Statement

#### Definition

The `return` statement is used to **exit from a method**. It can optionally return a value to the calling method. When JVM encounters `return`, the method execution stops immediately.

#### How It Works

- Exits the current method.
- If the method has a return type, it sends a value back to the caller.
- If the method is `void`, `return;` (without a value) can be used to exit early.

#### Simple Example: return with a Value

```java
public class ReturnExample {

    public static int add(int a, int b) {
        return a + b; // exits method and returns the sum
    }

    public static void main(String[] args) {
        int result = add(10, 20);
        System.out.println("Sum: " + result);
    }
}
```

#### Output

```
Sum: 30
```

#### Example: return in void Method

```java
public class ReturnVoidExample {

    public static void checkAge(int age) {
        if (age < 18) {
            System.out.println("Not eligible.");
            return; // exit method early
        }
        System.out.println("Eligible!");
        System.out.println("Processing...");
    }

    public static void main(String[] args) {
        checkAge(15);
        System.out.println("---");
        checkAge(20);
    }
}
```

#### Output

```
Not eligible.
---
Eligible!
Processing...
```

---

## 4. Difference Between break and continue

| Aspect | break | continue |
|--------|-------|----------|
| **Action** | Terminates the entire loop | Skips current iteration only |
| **Loop exit** | Yes, exits the loop immediately | No, stays in the loop |
| **Next iteration** | Does not execute | Moves to the next iteration |
| **Use case** | Stop searching once value is found | Skip unwanted values, continue with rest |
| **Works with** | Loops and switch statements | Loops only |

**In simple terms:**
- `break` → "I'm done. Leave the loop."
- `continue` → "Skip this one. Move to the next value."

---

## 5. Common Mistakes to Avoid

### 1. Infinite Loops

Forgetting the update statement (increment/decrement) in a `while` or `do-while` loop causes an infinite loop.

```java
// WRONG - infinite loop!
int i = 1;
while (i <= 5) {
    System.out.println(i);
    // forgot i++ here!
}
```

### 2. Forgetting Update Statements

In a `while` loop, the increment/decrement must be written **inside the body**. Unlike the `for` loop, it is not part of the loop declaration.

### 3. Confusing break and continue

- `break` → **Exits** the entire loop.
- `continue` → Only **skips** the current iteration.

Using `break` when you meant `continue` will terminate the loop prematurely.

### 4. Misusing do-while Loop

Remember that `do-while` always executes **at least once**. Don't use it when you need to check the condition **before** the first execution.

```java
// Be careful: this prints even though condition is false
int i = 100;
do {
    System.out.println(i); // prints 100
} while (i < 5);
```

### 5. Forgetting Semicolon in do-while

The `do-while` loop requires a **semicolon** after the `while(condition)`.

```java
do {
    // logic
} while (condition); // <-- semicolon is mandatory
```

### 6. Using return Unnecessarily

Don't use `return` in the middle of a method unless there is a clear reason (like early exit). It can make code harder to read.

---

## 6. Summary

### Looping Statements

| Loop | When to Use |
|------|-------------|
| `for` | Number of iterations is known; variable not needed outside loop |
| `while` | Number of iterations unknown; variable needed outside loop; starting value from external source |
| `do-while` | Logic must execute at least once before condition check |
| Enhanced `for` | Iterating over all elements of an array or collection |

### Branching Statements

| Statement | When to Use |
|-----------|-------------|
| `break` | Stop loop execution immediately (e.g., value found) |
| `continue` | Skip current iteration and process next value |
| `return` | Exit a method, optionally returning a value |

### Key Takeaways

- **Looping** = Execute logic repeatedly until a condition becomes false.
- **Branching** = Transfer control unconditionally from one point to another.
- `for` loop defines initialization, condition, and update in **one line**.
- `while` loop keeps initialization **outside** and update **inside** the body.
- `do-while` guarantees **at least one execution**.
- `break` **terminates** the loop; `continue` **skips** the current iteration.
- From Java 8+, Stream API offers alternatives to loops, but loop knowledge remains essential for interviews and problem-solving.

---