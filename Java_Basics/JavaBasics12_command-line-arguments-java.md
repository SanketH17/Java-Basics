# Command Line Arguments in Java

---

## 1. Introduction

### What are Command Line Arguments?

Command line arguments are **values that you pass to a Java program at the time of execution** (when you run the program).

Think of it like this:
> When you order food, you tell the waiter **what you want** at the time of ordering.  
> Similarly, you tell the Java program **what data to use** at the time of running it.

These values are received by the `main` method through the `String[] args` parameter.

### Why are they used?

- To **pass input values externally** to the `main` method without hardcoding them.
- The `main` method is called by the **JVM automatically** — we cannot call it manually. So, command line arguments are the way to send data to it.
- Useful in real-time applications, especially when running programs via **scripts** or **Spring Boot** configurations.

---

## 2. How Command Line Arguments Work

### The `main` Method Signature

Every Java program starts execution from the `main` method:

```java
public static void main(String[] args) {
    // program logic here
}
```

### What does `String[] args` mean?

| Part         | Meaning                                                      |
|--------------|--------------------------------------------------------------|
| `String[]`   | An array of Strings                                          |
| `args`       | Variable name (can be anything — `args`, `abc`, `myInput`)   |

- `args` is just a **variable name** — you can rename it to anything you like.
- `String[]` means the method accepts a **group of String values** in the form of an array.

### Why is it a String array (not int or double)?

Java chose `String` because:
- Inside a String, you can store **any kind of data** — numbers, text, special characters, emails, etc.
- If it were `int[]`, you could only pass numbers — no text, no emails, no special characters.
- After receiving as String, you can **convert** to int, double, etc. using methods like `Integer.parseInt()`.

> **Example:** `"123"` is a valid String. You can convert it to int later.  
> But `"Dileep"` can **never** be stored in an int — that's why String is the safest choice.

### What happens if you change `String[]` to `int[]`?

```java
// This will NOT work as a valid main method
public static void main(int[] args) {
    // JVM will NOT recognize this as the main method
}
```

- **Compilation:** Success (no error)
- **Execution:** Error!

```
Error: Main method not found in class ClassName.
Please define the main method as:
   public static void main(String[] args)
```

> **Key Point:** JVM always looks for the main method with **exactly** `String[]` as the parameter. Any other type = program won't run.

---

## 3. Passing Command Line Arguments

### From the Command Line (Terminal / Command Prompt)

**Step 1:** Compile the program

```
javac MyProgram.java
```

**Step 2:** Run the program and pass values after the class name

```
java MyProgram value1 value2 value3
```

- Each value is **separated by a space**.
- You can pass **any number of values**.

**Example:**

```
java MyProgram 123 Dileep dileep@gmail.com 66.77
```

Here, 4 values are passed:
| Index | Value              |
|-------|--------------------|
| 0     | `"123"`            |
| 1     | `"Dileep"`         |
| 2     | `"dileep@gmail.com"` |
| 3     | `"66.77"`          |

> **Note:** All values are stored as **Strings**, regardless of what they look like.

### From Eclipse IDE

1. Go to **Run** → **Run Configurations...**
2. Select your class under **Java Application**.
3. Click the **Arguments** tab.
4. In the **Program Arguments** text box, type your values separated by spaces.
5. Click **Run**.

Example input in Program Arguments box:
```
abc@gmail.com abc123
```

> Once configured, Eclipse will use these values every time you run. To change them, go back to Run Configurations.

---

## 4. Accessing Command Line Arguments

### Using Index

Command line arguments are stored in the `args` array. Access them using **index numbers** (starting from **0**).

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println(args[0]); // First value
        System.out.println(args[1]); // Second value
        System.out.println(args[2]); // Third value
    }
}
```

**Run:**
```
java Demo Hello World Java
```

**Output:**
```
Hello
World
Java
```

### Checking the Number of Arguments

Use `args.length` to find how many values were passed:

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("Number of arguments: " + args.length);
    }
}
```

**Run:**
```
java Demo A B C D
```

**Output:**
```
Number of arguments: 4
```

> If no arguments are passed, `args.length` will be **0** (not null — the array exists, it's just empty).

---

## 5. Example Programs

### Example 1: Print All Command Line Arguments

```java
public class PrintArgs {
    public static void main(String[] args) {
        System.out.println("Total arguments: " + args.length);

        for (String val : args) {
            System.out.println(val);
        }
    }
}
```

**Run:**
```
java PrintArgs 123 Dileep dileep@gmail.com 66.77
```

**Output:**
```
Total arguments: 4
123
Dileep
dileep@gmail.com
66.77
```

---

### Example 2: Adding Two Numbers

Since arguments come as Strings, we must **convert** them to int before doing math.

```java
public class AddNumbers {
    public static void main(String[] args) {
        int num1 = Integer.parseInt(args[0]);
        int num2 = Integer.parseInt(args[1]);
        int sum = num1 + num2;

        System.out.println("Sum: " + sum);
    }
}
```

**Run:**
```
java AddNumbers 10 20
```

**Output:**
```
Sum: 30
```

---

### Example 3: Checking Number of Arguments Before Accessing

```java
public class SafeAccess {
    public static void main(String[] args) {
        if (args.length < 2) {
            System.out.println("Please provide at least 2 arguments.");
        } else {
            System.out.println("Arg 1: " + args[0]);
            System.out.println("Arg 2: " + args[1]);
        }
    }
}
```

**Run without arguments:**
```
java SafeAccess
```

**Output:**
```
Please provide at least 2 arguments.
```

---

### Example 4: Simple Database Config Simulation

```java
public class DBConfig {
    public static void main(String[] args) {
        if (args.length < 2) {
            System.out.println("Usage: java DBConfig <email> <password>");
            return;
        }

        String email = args[0];
        String password = args[1];

        System.out.println("Email: " + email);
        System.out.println("Password: " + password);
    }
}
```

**Run:**
```
java DBConfig abc@gmail.com abc123
```

**Output:**
```
Email: abc@gmail.com
Password: abc123
```

---

## 6. Important Points

| Point | Detail |
|-------|--------|
| All arguments are **Strings** | Even `"123"` is a String, not an int |
| Use `Integer.parseInt()` | To convert String to int |
| Use `Double.parseDouble()` | To convert String to double |
| Use `Float.parseFloat()` | To convert String to float |
| `args` is just a name | You can rename it to anything (`data`, `input`, etc.) |
| No arguments = empty array | `args.length` will be `0`, not null |
| JVM requires `String[]` | The main method **must** have `String[]` — no other type |

### String to Number Conversion

```java
String s = "100";

int i = Integer.parseInt(s);         // 100
double d = Double.parseDouble(s);    // 100.0
float f = Float.parseFloat(s);       // 100.0
long l = Long.parseLong(s);          // 100
```

---

## 7. Common Errors

### 1. `ArrayIndexOutOfBoundsException`

**Cause:** Accessing an index that doesn't exist.

```java
public class ErrorDemo {
    public static void main(String[] args) {
        System.out.println(args[0]); // Error if no arguments passed!
    }
}
```

**Run:**
```
java ErrorDemo
```

**Error:**
```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0
```

**Fix:** Always check `args.length` before accessing.

---

### 2. `NumberFormatException`

**Cause:** Trying to convert a non-numeric String to a number.

```java
public class ErrorDemo2 {
    public static void main(String[] args) {
        int num = Integer.parseInt(args[0]); // Error if args[0] = "Hello"
    }
}
```

**Run:**
```
java ErrorDemo2 Hello
```

**Error:**
```
Exception in thread "main" java.lang.NumberFormatException: For input string: "Hello"
```

**Fix:** Validate that the input is a valid number before converting.

---

### 3. Main Method Not Found Error

**Cause:** Changing `String[]` to another data type like `int[]`.

```java
public static void main(int[] args) { }  // Wrong!
```

**Error:**
```
Error: Main method not found in class ClassName.
Please define the main method as:
   public static void main(String[] args)
```

---

## 8. Best Practices

1. **Always check `args.length`** before accessing any index.
   ```java
   if (args.length > 0) {
       System.out.println(args[0]);
   }
   ```

2. **Validate input** before converting to numbers.

3. **Print a usage message** when required arguments are missing.
   ```java
   if (args.length < 2) {
       System.out.println("Usage: java MyProgram <arg1> <arg2>");
       return;
   }
   ```

4. **Never assume** that arguments will always be provided.

5. **Use meaningful variable names** after extracting values from `args`.
   ```java
   String username = args[0];
   String password = args[1];
   ```

---

## 9. Quick Revision

- Command line arguments = values passed to program **at the time of execution**.
- They are received by `String[] args` in the `main` method.
- `args` is just a variable name — can be anything.
- All values are stored as **Strings** (even numbers like `"123"`).
- Use `Integer.parseInt()`, `Double.parseDouble()`, etc. to convert.
- Values are separated by **spaces** on the command line.
- Index starts from **0**.
- `args.length` gives the **count** of arguments passed.
- If no arguments are passed, `args.length` is **0**.
- JVM **only** accepts `String[]` in the main method — not `int[]` or any other type.
- In Eclipse: use **Run Configurations → Arguments → Program Arguments**.
- Java chose `String[]` because String can hold **any type** of data.
- Command line arguments are useful in **real-time applications** (e.g., Spring Boot, scripts).

---

