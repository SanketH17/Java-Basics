# User Dynamic Input of Data in Java

## 1. Introduction

### What is User Input?

In Java, **user input** means taking data from the user (via keyboard) while the program is running, instead of hardcoding fixed values directly in the code.

### Why is Dynamic Input Important?

When you hardcode values like this:

```java
int value1 = 10;
int value2 = 20;
```

No matter how many times you execute the program, the output will always be the same (e.g., always `30` for addition). The JVM never asks the user for values — it simply uses whatever is written in the code.

**Dynamic input** solves this problem:
- Every time the program runs, the JVM **asks the user** to enter values.
- The user can enter **different values** on each execution.
- This makes the program behave like a real-world application.
- Until the user provides input, the JVM **waits** — it does not proceed further.

> **Real-time note:** In actual enterprise applications, data comes from the front-end (HTML/CSS/JavaScript) via HTTP requests, not from `Scanner`. However, for **Core Java practice and interviews**, using `Scanner` to take keyboard input is the standard approach.

---

## 2. Ways to Take User Input in Java

Java provides predefined classes to take input from the user while the program is executing:

| Class | Package | Description |
|-------|---------|-------------|
| **Scanner** | `java.util` | Simple and commonly used for reading keyboard input |
| **BufferedReader** | `java.io` | Faster but slightly more complex; uses streams |

For Core Java learning and practice, **Scanner** is the recommended and most commonly used approach.

---

## 3. Using Scanner Class

### 3.1 What is Scanner?

`Scanner` is a **predefined class** provided by Java in the `java.util` package. It is used to read input data from the keyboard (or other input sources) while the program is executing.

### 3.2 Syntax

```java
// Step 1: Import the Scanner class
import java.util.Scanner;

// Step 2: Create a Scanner object
Scanner scanner = new Scanner(System.in);

// Step 3: Use scanner methods to read input
int value = scanner.nextInt();        // for integer
String text = scanner.nextLine();     // for string
```

#### Explanation of `System.in`

- `System` is a predefined class from `java.lang` package.
- `in` is a **static variable** of the System class that represents **input from the keyboard**.
- `System.out` → used for **output** (printing to console).
- `System.in` → used for **input** (reading from keyboard).

When you pass `System.in` to the Scanner constructor, you are telling Java: "Read input from the keyboard."

---

### 3.3 Taking Different Types of Input

#### Integer Input — `nextInt()`

```java
import java.util.Scanner;

public class IntegerInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Please enter first value:");
        int x = scanner.nextInt();

        System.out.println("Please enter second value:");
        int y = scanner.nextInt();

        int addition = x + y;
        int subtraction = x - y;

        System.out.println("Addition: " + addition);
        System.out.println("Subtraction: " + subtraction);

        scanner.close();
    }
}
```

**How it works:**
1. JVM prints "Please enter first value:" and **waits** for user input.
2. User enters a number (e.g., `33`) and presses Enter.
3. JVM stores `33` in variable `x`.
4. JVM prints "Please enter second value:" and **waits** again.
5. User enters another number (e.g., `55`) and presses Enter.
6. JVM stores `55` in `y`, then performs the operations.

**Output (example):**
```
Please enter first value:
33
Please enter second value:
55
Addition: 88
Subtraction: -22
```

---

#### String Input — `next()` and `nextLine()`

```java
import java.util.Scanner;

public class StringInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Please enter your first name:");
        String firstName = scanner.next();

        System.out.println("Please enter your last name:");
        String lastName = scanner.next();

        String fullName = firstName + " " + lastName;
        System.out.println("Your full name is: " + fullName);

        scanner.close();
    }
}
```

**Output (example):**
```
Please enter your first name:
Dilip
Please enter your last name:
Singh
Your full name is: Dilip Singh
```

---

#### Double Input — `nextDouble()`

```java
import java.util.Scanner;

public class DoubleInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter average of marks:");
        double average = scanner.nextDouble();

        System.out.println("Your average: " + average);

        scanner.close();
    }
}
```

**Output (example):**
```
Enter average of marks:
76.74
Your average: 76.74
```

---

#### Float Input — `nextFloat()`

```java
import java.util.Scanner;

public class FloatInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter temperature:");
        float temp = scanner.nextFloat();

        System.out.println("Temperature: " + temp);

        scanner.close();
    }
}
```

**Output (example):**
```
Enter temperature:
36.5
Temperature: 36.5
```

---

#### Boolean Input — `nextBoolean()`

```java
import java.util.Scanner;

public class BooleanInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Do you have percentage greater than 70?");
        boolean isQualified = scanner.nextBoolean();

        System.out.println("Qualified: " + isQualified);

        scanner.close();
    }
}
```

**Output (example):**
```
Do you have percentage greater than 70?
true
Qualified: true
```

> **Note:** User must enter exactly `true` or `false` (case-insensitive). Any other value will cause an error.

---

#### Character Input — `next().charAt(0)`

Java's Scanner class does **not** have a direct `nextChar()` method. To read a single character:

```java
import java.util.Scanner;

public class CharInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter a character:");
        char ch = scanner.next().charAt(0);

        System.out.println("You entered: " + ch);

        scanner.close();
    }
}
```

**Output (example):**
```
Enter a character:
A
You entered: A
```

**Explanation:** `next()` reads a string, and `.charAt(0)` extracts the first character from it.

---

### Summary of Scanner Methods

| Data Type | Method | Example |
|-----------|--------|---------|
| `int` | `nextInt()` | `int age = scanner.nextInt();` |
| `double` | `nextDouble()` | `double avg = scanner.nextDouble();` |
| `float` | `nextFloat()` | `float temp = scanner.nextFloat();` |
| `boolean` | `nextBoolean()` | `boolean flag = scanner.nextBoolean();` |
| `String` (single word) | `next()` | `String name = scanner.next();` |
| `String` (full line) | `nextLine()` | `String line = scanner.nextLine();` |
| `long` | `nextLong()` | `long num = scanner.nextLong();` |
| `short` | `nextShort()` | `short s = scanner.nextShort();` |

---

## 4. Important Points about Scanner

### Difference between `next()` and `nextLine()`

| Feature | `next()` | `nextLine()` |
|---------|----------|--------------|
| Reads | A single word (until space) | Entire line (until Enter) |
| Stops at | Space or newline | Only newline (Enter key) |
| Use case | Single-word input (name, city) | Full sentences or multi-word input |

**Example:**

```java
Scanner scanner = new Scanner(System.in);

System.out.println("Enter something:");
String word = scanner.next();       // If user types "Hello World", reads only "Hello"

String line = scanner.nextLine();   // Reads the full line including spaces
```

### Buffer Issue (Newline Problem)

When you use `nextInt()`, `nextDouble()`, or `next()` followed by `nextLine()`, a common issue occurs:

```java
Scanner scanner = new Scanner(System.in);

System.out.println("Enter age:");
int age = scanner.nextInt();       // reads number, leaves \n in buffer

System.out.println("Enter name:");
String name = scanner.nextLine();  // reads the leftover \n, appears to skip!
```

**Solution:** Add an extra `scanner.nextLine()` after `nextInt()` to consume the leftover newline:

```java
Scanner scanner = new Scanner(System.in);

System.out.println("Enter age:");
int age = scanner.nextInt();
scanner.nextLine(); // consume the leftover newline

System.out.println("Enter name:");
String name = scanner.nextLine(); // now works correctly
```

### Closing Scanner — `scanner.close()`

It is good practice to close the Scanner object after use to free up resources:

```java
scanner.close();
```

---

## 5. BufferedReader (Basic Overview)

### What is BufferedReader?

`BufferedReader` is another predefined class (from `java.io` package) that can read input from the keyboard. It is older than Scanner and slightly more complex to use.

### Why is it Used?

- It is **faster** than Scanner for reading large amounts of data.
- It reads data as a **String**, so you need to manually convert to other data types.

### Simple Example

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

        System.out.println("Enter your name:");
        String name = reader.readLine();

        System.out.println("Enter your age:");
        int age = Integer.parseInt(reader.readLine()); // manual conversion

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);

        reader.close();
    }
}
```

**Key differences from Scanner:**
- Always reads input as `String` — you must parse/convert manually.
- Requires handling `IOException`.
- Uses `readLine()` method for reading input.

> **For beginners:** Focus on Scanner. BufferedReader understanding will come naturally as you progress to advanced Java and file I/O operations.

---

## 6. Common Mistakes to Avoid

### 1. Input Mismatch Exception

If the Scanner method expects an `int` but the user enters a `String`, you get `InputMismatchException`:

```java
int age = scanner.nextInt();
// User enters "twenty-five" instead of 25 → InputMismatchException!
```

**Fix:** Always enter data that matches the expected data type.

### 2. Forgetting to Import Scanner

```java
// ERROR: Scanner cannot be resolved to a type
Scanner scanner = new Scanner(System.in);
```

**Fix:** Add the import statement at the top:
```java
import java.util.Scanner;
```

### 3. Confusing `next()` and `nextLine()`

- `next()` reads only **one word** (stops at space).
- `nextLine()` reads the **entire line** (stops at Enter).

If you expect "Java Language" but use `next()`, you will only get "Java".

### 4. Not Handling Newline After `nextInt()`

After `nextInt()` or `nextDouble()`, a newline character (`\n`) remains in the buffer. The next `nextLine()` call reads this leftover newline instead of actual user input.

**Fix:** Add `scanner.nextLine()` after `nextInt()` or `nextDouble()` to consume the newline.

### 5. Entering Wrong Data Types

The method used must match the data type expected:
- `nextInt()` → enter integer values only
- `nextBoolean()` → enter `true` or `false` only
- `nextDouble()` → enter decimal numbers

Mismatched input causes `InputMismatchException` at runtime.

### 6. Not Closing the Scanner

Always close the Scanner when done:
```java
scanner.close();
```
Leaving it open won't cause an immediate error but is bad practice and can lead to resource leaks.

---

## 7. Summary

### Dynamic Input Concept

- **Fixed values** (hardcoded) → Same output every time. JVM never asks the user.
- **Dynamic input** (via Scanner) → JVM waits for the user to enter values on every execution. Different input = different output.

### Scanner Usage

| Step | Action |
|------|--------|
| 1 | Import: `import java.util.Scanner;` |
| 2 | Create object: `Scanner scanner = new Scanner(System.in);` |
| 3 | Display prompt: `System.out.println("Enter value:");` |
| 4 | Read input: `int x = scanner.nextInt();` |
| 5 | Use the variable in your logic |
| 6 | Close: `scanner.close();` |

### Key Takeaways

- Use `Scanner` class from `java.util` package to take dynamic input.
- `System.in` represents keyboard input; `System.out` represents console output.
- Different methods exist for different data types: `nextInt()`, `nextDouble()`, `nextBoolean()`, `next()`, `nextLine()`, etc.
- Always display a message (prompt) before reading input so the user knows what to enter.
- Match the input data type with the Scanner method being used.
- In real-time applications, data comes from the front-end (not Scanner), but Scanner is essential for Core Java practice and interviews.
- From today onwards: **avoid hardcoding values** — always take data dynamically from the keyboard for practice.

---