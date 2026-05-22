# Control Flow Statements & Switch Statement in Java

---

## 1. Introduction to Control Flow Statements

In Java, the program executes **line by line in a sequential order** (top to bottom). But in real-time applications, we often need to:

- Execute specific logic based on conditions.
- Skip certain lines of code.
- Repeat the same logic multiple times.

**Control flow statements** allow us to control the execution flow of a program instead of always going sequentially.

### Types of Control Flow Statements:

| Type | Purpose | Examples |
|------|---------|----------|
| Decision Making / Selection | Execute logic based on conditions | `if`, `if-else`, `if-else-if`, `switch` |
| Looping / Iteration | Repeat logic multiple times | `for`, `while`, `do-while` |
| Branching / Jumping | Jump from one statement to another | `break`, `continue`, `return` |

---

## 2. Decision Making Statements (Quick Overview)

### 2.1 `if` Statement

Used when you only need to handle the **true** scenario.

```java
if (condition) {
    // executes only when condition is true
}
```

### 2.2 `if-else` Statement

Used when you need to handle **both true and false** scenarios.

```java
if (condition) {
    // executes when condition is true
} else {
    // executes when condition is false
}
```

### 2.3 `if-else-if` Ladder

Used when you have **multiple conditions** to check one by one.

```java
if (condition1) {
    // executes when condition1 is true
} else if (condition2) {
    // executes when condition2 is true
} else if (condition3) {
    // executes when condition3 is true
} else {
    // executes when ALL conditions are false (default)
}
```

**Key Rules:**
- Once a condition becomes `true`, that block executes and **rest of the blocks are skipped**.
- The last `else` block is optional — it acts as a **default** when no condition is satisfied.
- The `else` block (without condition) must always be the **last block**.

### 2.4 Nested `if` Statement

An `if` block inside another `if` block — used when you need condition inside a condition.

```java
if (condition1) {
    if (condition2) {
        // executes when both condition1 AND condition2 are true
    }
}
```

---

## 3. What is a Switch Statement?

The **switch statement** is an alternative to the `if-else-if` ladder. It is used to write **specific logic for specific fixed values**.

### When to use Switch instead of if-else-if:

| Use `if-else-if` | Use `switch` |
|-------------------|--------------|
| When you have **range-based** conditions (e.g., score > 70) | When you have **fixed/defined values** (e.g., Monday, Tuesday) |
| When conditions involve comparisons (`>`, `<`, `>=`, `<=`) | When checking **equality** with specific values |
| When conditions are complex with `&&`, `||` | When values are known and limited |

### Real-Life Example:
If you create a **weekly plan** where each day has specific activities:
- Monday → Study + Walk
- Tuesday → Visit a place
- Sunday → Movie + Dinner

Each day has **fixed, defined** activities. This is a perfect use case for a switch statement.

> **Important:** Every switch statement can be written using if-else-if, but NOT every if-else-if can be written using switch (because switch doesn't support range-based conditions).

---

## 4. Syntax of Switch Statement

```java
switch (expression / value) {
    case value1:
        // logic for value1
        break;
    case value2:
        // logic for value2
        break;
    case value3:
        // logic for value3
        break;
    default:
        // logic when no case matches
        break;
}
```

### Parts Explained:

| Part | Description |
|------|-------------|
| `switch` | Keyword that starts the switch statement |
| `expression/value` | The value to be matched against cases |
| `case` | Keyword followed by a specific value and colon `:` |
| `break` | Stops execution and exits the switch block |
| `default` | Executes when no case value matches (like `else` in if-else-if) |

---

## 5. Simple Example of Switch Statement

```java
public class WeekdayActivities {
    public static void main(String[] args) {
        String day = "Thursday";

        switch (day) {
            case "Monday":
                System.out.println("Study + Morning Walk");
                break;
            case "Tuesday":
                System.out.println("Visit a place");
                break;
            case "Wednesday":
                System.out.println("Study + Training");
                break;
            case "Thursday":
                System.out.println("Training + Fun Activities");
                break;
            case "Friday":
                System.out.println("Project Work");
                break;
            case "Saturday":
                System.out.println("Revision + Rest");
                break;
            case "Sunday":
                System.out.println("Movie + Dinner Outside");
                break;
            default:
                System.out.println("Invalid day! Please enter a valid weekday.");
                break;
        }

        System.out.println("End of program.");
    }
}
```

**Output:**
```
Training + Fun Activities
End of program.
```

### Step-by-Step Execution:
1. `day` = "Thursday" is passed to the switch.
2. JVM checks: "Thursday" == "Monday"? No → skip.
3. "Thursday" == "Tuesday"? No → skip.
4. "Thursday" == "Wednesday"? No → skip.
5. "Thursday" == "Thursday"? **Yes** → execute this case logic.
6. `break` is encountered → JVM exits the switch statement.
7. Rest of the cases are **ignored**.
8. Program continues after the switch block.

---

## 6. Role of `break` Statement

The `break` keyword tells the JVM to **stop executing and exit** the switch block immediately.

### What happens WITHOUT `break` (Fall-Through):

If `break` is missing, JVM will **blindly execute all subsequent cases** after the matched case, regardless of whether their values match or not. This is called **fall-through**.

```java
public class BreakDemo {
    public static void main(String[] args) {
        String day = "Wednesday";

        switch (day) {
            case "Monday":
                System.out.println("Monday activities");
            case "Tuesday":
                System.out.println("Tuesday activities");
            case "Wednesday":
                System.out.println("Wednesday activities");
            case "Thursday":
                System.out.println("Thursday activities");
            case "Friday":
                System.out.println("Friday activities");
                break;
            case "Saturday":
                System.out.println("Saturday activities");
                break;
            case "Sunday":
                System.out.println("Sunday activities");
                break;
        }
    }
}
```

**Output:**
```
Wednesday activities
Thursday activities
Friday activities
```

### Explanation:
- "Wednesday" matches at `case "Wednesday"`.
- No `break` after Wednesday → falls through to Thursday.
- No `break` after Thursday → falls through to Friday.
- `break` found at Friday → JVM exits switch.
- Saturday and Sunday are **not executed**.

### Key Point:
> Once a case match is found, JVM does NOT check values of subsequent cases. It blindly enters next cases until it finds a `break` or reaches the end of the switch.

---

## 7. Role of `default` Case

The `default` block executes when **no case value matches** the switch expression. It is equivalent to the `else` block in an if-else-if ladder.

### Example:

```java
public class DefaultDemo {
    public static void main(String[] args) {
        String day = "Holiday";

        switch (day) {
            case "Monday":
                System.out.println("Monday activities");
                break;
            case "Tuesday":
                System.out.println("Tuesday activities");
                break;
            default:
                System.out.println("Invalid value! Please enter a valid weekday.");
                break;
        }
    }
}
```

**Output:**
```
Invalid value! Please enter a valid weekday.
```

### Important Points about `default`:
- `default` is **optional** — you can skip it if not needed.
- `default` can be placed **anywhere** in the switch (beginning, middle, or end).
- If placed in the middle without `break`, fall-through will still occur.
- **Best practice:** Keep `default` at the end and always add `break` to it.
- If `default` is the **last block**, `break` is technically not required (but recommended for safety).

---

## 8. Important Rules of Switch Statement

### Allowed Data Types in Switch:

| Allowed | Not Allowed |
|---------|-------------|
| `byte`, `short`, `int`, `char` | `long` |
| `String` (from Java 7+) | `float`, `double` |
| `enum` | `boolean` |
| Wrapper classes (`Byte`, `Short`, `Integer`, `Character`) | |

### Other Rules:

1. **Case values must be constants** — you cannot use variables (unless `final`).
   ```java
   // Valid
   case 10:
   case "Monday":

   // Invalid
   int x = 10;
   case x:  // Compile-time error (unless x is final)
   ```

2. **Duplicate case values are NOT allowed** — each case must have a unique value.
   ```java
   case "Monday":
       // logic
   case "Monday":  // Compile-time error: Duplicate case
       // logic
   ```

3. **Data type of case values must match** the switch expression data type.
   ```java
   switch ("Hello") {
       case 10:  // Error: Type mismatch (int to String)
           break;
   }
   ```

4. **`break` is optional** but recommended to avoid fall-through.

5. **`default` is optional** and can be placed anywhere.

6. **`break` must be the last statement** in a case block. Writing code after `break` gives a compile-time error: "Unreachable code".

7. **You can write multiple statements** inside a case — no limit on number of lines.

8. **Switch does NOT support conditions/ranges** — only exact value matching.

---

## 9. Switch Statement with Integers

```java
public class SwitchIntDemo {
    public static void main(String[] args) {
        int month = 3;

        switch (month) {
            case 1:
                System.out.println("January");
                break;
            case 2:
                System.out.println("February");
                break;
            case 3:
                System.out.println("March");
                break;
            case 4:
                System.out.println("April");
                break;
            default:
                System.out.println("Other month");
                break;
        }
    }
}
```

**Output:**
```
March
```

---

## 10. Switch Statement with Characters

```java
public class SwitchCharDemo {
    public static void main(String[] args) {
        char grade = 'B';

        switch (grade) {
            case 'A':
                System.out.println("Excellent!");
                break;
            case 'B':
                System.out.println("Good job!");
                break;
            case 'C':
                System.out.println("Average.");
                break;
            case 'D':
                System.out.println("Below average.");
                break;
            case 'F':
                System.out.println("Failed.");
                break;
            default:
                System.out.println("Invalid grade.");
                break;
        }
    }
}
```

**Output:**
```
Good job!
```

---

## 11. Switch Statement with Strings

```java
public class SwitchStringDemo {
    public static void main(String[] args) {
        String language = "Java";

        switch (language) {
            case "Java":
                System.out.println("Platform independent language.");
                break;
            case "Python":
                System.out.println("Great for AI and Data Science.");
                break;
            case "JavaScript":
                System.out.println("Used for web development.");
                break;
            default:
                System.out.println("Unknown language.");
                break;
        }
    }
}
```

**Output:**
```
Platform independent language.
```

> **Note:** String comparison in switch is **case-sensitive**. "Java" and "java" are treated as different values.

---

## 12. Switch vs If-Else-If — When to Use What

| Scenario | Recommended |
|----------|-------------|
| Fixed, known values (days, months, grades) | `switch` |
| Range-based conditions (score > 70, age < 18) | `if-else-if` |
| Complex conditions with `&&`, `||` | `if-else-if` |
| Simple equality checks with limited values | `switch` |
| Need to check `null` safely | `if-else-if` |

### Key Insight from Transcript:
> "Switch statement is used when you have **fixed set of values** and you want to write specific logic for each value. If you have **range of values** (like civil score 500-600, 600-700), you **cannot** use switch — use if-else-if instead."

---

## 13. Common Mistakes to Avoid

| Mistake | Problem |
|---------|---------|
| Forgetting `break` | Causes fall-through — subsequent cases execute unexpectedly |
| Using duplicate case values | Compile-time error |
| Using non-constant case values | Compile-time error |
| Using invalid data types (`long`, `float`, `double`, `boolean`) | Compile-time error |
| Writing code after `break` | "Unreachable code" compile-time error |
| Placing `break` in the middle of a case | Logic after break is unreachable |
| Assuming `default` must be last | Not required — but recommended |
| Passing `null` to switch (String) | Throws `NullPointerException` at runtime |

---

## 14. Summary

- **Control flow statements** allow controlling the execution order of code.
- Three types: **Decision making**, **Looping**, **Branching**.
- `if` → only true scenario; `if-else` → true and false; `if-else-if` → multiple conditions.
- In if-else-if ladder, once one condition is `true`, **rest are skipped**.
- **Switch statement** is an alternative to if-else-if for **fixed value matching**.
- Switch keywords: `switch`, `case`, `break`, `default`.
- `break` → exits the switch; without it, fall-through occurs.
- `default` → executes when no case matches (like `else`).
- `default` is optional and can be placed anywhere.
- Case values must be: **constant**, **unique**, and **same data type** as switch expression.
- Switch supports: `int`, `byte`, `short`, `char`, `String`, `enum`.
- Switch does NOT support: `long`, `float`, `double`, `boolean`, ranges, or conditions.
- **Best practice:** Always add `break` to every case including `default`.

---

## 15. Quick Revision Checklist

- [ ] Java executes statements sequentially (line by line) by default.
- [ ] Control flow statements change this default sequential execution.
- [ ] `if` handles only true; `if-else` handles true + false.
- [ ] `if-else-if` ladder: first true condition's block executes, rest skipped.
- [ ] Last `else` in ladder = default block (when all conditions are false).
- [ ] Switch = alternative to if-else-if for **exact value matching only**.
- [ ] Switch cannot handle ranges or complex conditions.
- [ ] `case` values must be constants, unique, and same type as switch.
- [ ] Without `break`, JVM blindly executes all cases below the match (fall-through).
- [ ] `break` = exit the switch immediately.
- [ ] `default` = execute when no case matches.
- [ ] Code after `break` in same case → unreachable code error.
- [ ] String values in switch are case-sensitive.

---

## Conclusion

Control flow statements give you the power to make decisions in your Java programs. The **switch statement** provides a clean and readable way to handle **fixed value-based logic** compared to long if-else-if ladders. Always remember to use `break` in every case to avoid unexpected fall-through behavior.

**When in doubt:**
- Use `if-else-if` for **conditions and ranges**.
- Use `switch` for **fixed, known values**.

---