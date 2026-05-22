# Types of Operators in Java

## Introduction

An **operator** in Java is a special symbol used to perform operations on variables and values. Operations include calculations, comparisons, logical decisions, and value assignments.

Java provides the following types of operators:

| # | Operator Type | Symbol Examples |
|---|--------------|----------------|
| 1 | Arithmetic | `+`, `-`, `*`, `/`, `%` |
| 2 | Unary | `+`, `-`, `++`, `--`, `!` |
| 3 | Assignment | `=`, `+=`, `-=`, `*=`, `/=`, `%=` |
| 4 | Relational / Comparison | `==`, `!=`, `>`, `<`, `>=`, `<=` |
| 5 | Logical / Conditional | `&&`, `||`, `!` |
| 6 | Bitwise | `&`, `|`, `^`, `~` |
| 7 | Shift | `<<`, `>>`, `>>>` |
| 8 | Ternary | `? :` |
| 9 | instanceof | `instanceof` |

---

## 1. Arithmetic Operators

Arithmetic operators are used to perform basic mathematical operations on two values (operands).

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division | `10 / 3` | `3` |
| `%` | Modulus (Remainder) | `10 % 3` | `1` |

> **Note:** When dividing two integers, the result is also an integer (decimal part is discarded).

### Example:

```java
public class ArithmeticDemo {
    public static void main(String[] args) {
        int a = 20, b = 6;

        System.out.println("Addition: " + (a + b));       // 26
        System.out.println("Subtraction: " + (a - b));    // 14
        System.out.println("Multiplication: " + (a * b)); // 120
        System.out.println("Division: " + (a / b));       // 3
        System.out.println("Modulus: " + (a % b));        // 2
    }
}
```

**Output:**
```
Addition: 26
Subtraction: 14
Multiplication: 120
Division: 3
Modulus: 2
```

---

## 2. Unary Operators

Unary operators work with **only one operand**. They are used to increment, decrement, negate, or invert a value.

| Operator | Meaning | Example |
|----------|---------|---------|
| `+` | Positive (indicates positive value) | `+a` |
| `-` | Negation (flips sign) | `-a` |
| `++` | Increment (adds 1) | `a++` or `++a` |
| `--` | Decrement (subtracts 1) | `a--` or `--a` |
| `!` | Logical NOT (inverts boolean) | `!true` → `false` |

### Prefix vs Postfix (Important!)

- **Prefix (`++a`):** Value is incremented **first**, then used in the expression.
- **Postfix (`a++`):** Current value is used in the expression **first**, then incremented.

### Example:

```java
public class UnaryDemo {
    public static void main(String[] args) {
        int x = 10;

        System.out.println("x = " + x);       // 10
        System.out.println("-x = " + (-x));    // -10
        System.out.println("++x = " + (++x));  // 11 (increment first, then use)
        System.out.println("x++ = " + (x++));  // 11 (use first, then increment)
        System.out.println("x after x++ = " + x); // 12

        int y = -20;
        System.out.println("-y = " + (-y));    // 20 (minus of minus = plus)

        boolean flag = true;
        System.out.println("!flag = " + (!flag)); // false
    }
}
```

**Output:**
```
x = 10
-x = -10
++x = 11
x++ = 11
x after x++ = 12
-y = 20
!flag = false
```

### Key Rules:
- `++a` → Increment happens **before** the value is used.
- `a++` → Increment happens **after** the value is used.
- Same logic applies for `--a` and `a--`.
- Minus of minus = positive: `-(-20)` = `20`
- Plus of minus = minus: `+(-20)` = `-20`

---

## 3. Assignment Operators

Assignment operators are used to assign values to variables. The basic assignment operator is `=`. Compound assignment operators combine an arithmetic operation with assignment.

| Operator | Meaning | Equivalent To |
|----------|---------|---------------|
| `=` | Assign | `a = 10` |
| `+=` | Add and assign | `a = a + 5` |
| `-=` | Subtract and assign | `a = a - 5` |
| `*=` | Multiply and assign | `a = a * 5` |
| `/=` | Divide and assign | `a = a / 5` |
| `%=` | Modulus and assign | `a = a % 5` |

### Example:

```java
public class AssignmentDemo {
    public static void main(String[] args) {
        int a = 10;
        System.out.println("a = " + a);   // 10

        a += 5;
        System.out.println("a += 5 → " + a);  // 15

        a -= 3;
        System.out.println("a -= 3 → " + a);  // 12

        a *= 2;
        System.out.println("a *= 2 → " + a);  // 24

        a /= 4;
        System.out.println("a /= 4 → " + a);  // 6

        a %= 4;
        System.out.println("a %= 4 → " + a);  // 2
    }
}
```

**Output:**
```
a = 10
a += 5 → 15
a -= 3 → 12
a *= 2 → 24
a /= 4 → 6
a %= 4 → 2
```

---

## 4. Relational / Comparison Operators

Relational operators compare two values and return a **boolean** result (`true` or `false`).

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `10 == 10` | `true` |
| `!=` | Not equal to | `10 != 5` | `true` |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `10 < 5` | `false` |
| `>=` | Greater than or equal to | `10 >= 10` | `true` |
| `<=` | Less than or equal to | `5 <= 10` | `true` |

### Important Points:
- `==` checks if both sides are **equal** → returns `true` if same, `false` if different.
- `!=` is the **opposite** of `==` → returns `true` if different, `false` if same.
- `>` checks if left side is **greater** than right side.
- No value is greater than or less than **itself**: `30 > 30` → `false`, `30 < 30` → `false`.
- `>=` checks: is left greater? If yes → `true`. If not, are they equal? If yes → `true`. Otherwise → `false`.

### Example:

```java
public class RelationalDemo {
    public static void main(String[] args) {
        int a = 30, b = 20;

        System.out.println("a == b: " + (a == b));  // false
        System.out.println("a != b: " + (a != b));  // true
        System.out.println("a > b: " + (a > b));    // true
        System.out.println("a < b: " + (a < b));    // false
        System.out.println("a >= 30: " + (a >= 30)); // true
        System.out.println("a <= b: " + (a <= b));  // false
    }
}
```

**Output:**
```
a == b: false
a != b: true
a > b: true
a < b: false
a >= 30: true
a <= b: false
```

---

## 5. Logical / Conditional Operators

Logical operators are used to **join multiple conditions** and produce a single boolean result. They are essential when you need to evaluate more than one condition together.

| Operator | Name | Meaning |
|----------|------|---------|
| `&&` | Logical AND | Both conditions must be `true` |
| `||` | Logical OR | At least one condition must be `true` |
| `!` | Logical NOT | Inverts the boolean value |

### AND Operator (`&&`):
- Returns `true` **only if ALL conditions are true**.
- If any one condition is `false`, the result is `false`.

### OR Operator (`||`):
- Returns `true` **if at least one condition is true**.
- Returns `false` only when ALL conditions are `false`.

### Truth Table:

| A | B | A && B | A \|\| B |
|---|---|--------|----------|
| true | true | true | true |
| true | false | false | true |
| false | true | false | true |
| false | false | false | false |

### Real-Life Example:
- **AND:** "Person who has more than 70% marks **AND** is female" → Both conditions must be satisfied.
- **OR:** "Person who has more than 70% marks **OR** is female" → Any one condition is enough.

### Example:

```java
public class LogicalDemo {
    public static void main(String[] args) {
        int percentage = 85;
        String gender = "Male";

        // AND operator - both must be true
        boolean andResult = (percentage > 70) && (gender.equals("Female"));
        System.out.println("AND result: " + andResult); // false

        // OR operator - at least one must be true
        boolean orResult = (percentage > 70) || (gender.equals("Female"));
        System.out.println("OR result: " + orResult);   // true

        // NOT operator
        boolean flag = false;
        System.out.println("!flag: " + (!flag));        // true
    }
}
```

**Output:**
```
AND result: false
OR result: true
!flag: true
```

### Short-Circuit Evaluation:
- `&&` → If the first condition is `false`, the second condition is **not checked** (result is already `false`).
- `||` → If the first condition is `true`, the second condition is **not checked** (result is already `true`).

---

## 6. Bitwise Operators

Bitwise operators work at the **bit level** (binary representation of numbers). They perform operations on individual bits.

> **Note:** Bitwise operators are rarely used in regular application development. They are mostly used in system-level programming (operating systems, compilers, etc.).

| Operator | Name | Meaning |
|----------|------|---------|
| `&` | Bitwise AND | Both bits must be 1 |
| `|` | Bitwise OR | At least one bit must be 1 |
| `^` | Bitwise XOR | Bits must be different |
| `~` | Bitwise NOT | Inverts all bits |

### How it works:
Numbers are converted to binary, the operation is applied bit by bit, and the result is converted back to decimal.

### Example:

```java
public class BitwiseDemo {
    public static void main(String[] args) {
        int a = 5;  // Binary: 0101
        int b = 3;  // Binary: 0011

        System.out.println("a & b = " + (a & b));  // 0001 → 1
        System.out.println("a | b = " + (a | b));  // 0111 → 7
        System.out.println("a ^ b = " + (a ^ b));  // 0110 → 6
        System.out.println("~a = " + (~a));        // -6
    }
}
```

**Output:**
```
a & b = 1
a | b = 7
a ^ b = 6
~a = -6
```

### Bit-by-Bit Breakdown (a=5, b=3):

```
  a = 0 1 0 1
  b = 0 0 1 1
  -----------
a&b = 0 0 0 1  → 1
a|b = 0 1 1 1  → 7
a^b = 0 1 1 0  → 6
```

---

## 7. Shift Operators

Shift operators move the bits of a number left or right by a specified number of positions.

| Operator | Name | Meaning |
|----------|------|---------|
| `<<` | Left Shift | Shifts bits to the left (multiplies by 2^n) |
| `>>` | Right Shift (Signed) | Shifts bits to the right (divides by 2^n) |
| `>>>` | Right Shift (Unsigned) | Shifts bits to the right, fills with 0 |

### Quick Formula:
- `a << n` is equivalent to `a * 2^n`
- `a >> n` is equivalent to `a / 2^n`

### Example:

```java
public class ShiftDemo {
    public static void main(String[] args) {
        int a = 8;  // Binary: 1000

        System.out.println("a << 1 = " + (a << 1));  // 16 (8 * 2)
        System.out.println("a << 2 = " + (a << 2));  // 32 (8 * 4)
        System.out.println("a >> 1 = " + (a >> 1));  // 4  (8 / 2)
        System.out.println("a >> 2 = " + (a >> 2));  // 2  (8 / 4)

        int b = -8;
        System.out.println("b >> 1 = " + (b >> 1));   // -4 (preserves sign)
        System.out.println("b >>> 1 = " + (b >>> 1)); // large positive number (fills with 0)
    }
}
```

**Output:**
```
a << 1 = 16
a << 2 = 32
a >> 1 = 4
a >> 2 = 2
b >> 1 = -4
b >>> 1 = 2147483644
```

---

## 8. Ternary Operator

The ternary operator is a **shorthand for if-else** statements. It evaluates a condition and returns one of two values based on whether the condition is `true` or `false`.

### Syntax:

```
result = (condition) ? valueOnTrue : valueOnFalse;
```

- **`?`** → separates the condition from the true-value.
- **`:`** → separates the true-value from the false-value.

### How it works:
1. The condition is evaluated.
2. If `true` → returns the value on the **left side of colon**.
3. If `false` → returns the value on the **right side of colon**.

### Example:

```java
public class TernaryDemo {
    public static void main(String[] args) {
        int a = 89, b = 99;

        // Find maximum of two numbers
        int max = (a > b) ? a : b;
        System.out.println("Max = " + max);  // 99

        // Find minimum of two numbers
        int min = (a < b) ? a : b;
        System.out.println("Min = " + min);  // 89

        // Check even or odd
        int num = 15;
        String result = (num % 2 == 0) ? "Even" : "Odd";
        System.out.println(num + " is " + result);  // 15 is Odd

        // Check eligibility
        int age = 20;
        String status = (age >= 18) ? "Eligible" : "Not Eligible";
        System.out.println(status);  // Eligible
    }
}
```

**Output:**
```
Max = 99
Min = 89
15 is Odd
Eligible
```

### Real-Life Analogy:
Think of it as: "If you have more than 70%, you are **eligible**, otherwise **not eligible**."

---

## 9. instanceof Operator

The `instanceof` operator checks whether an object is an **instance of a particular class or interface**. It returns `true` or `false`.

### Syntax:

```java
object instanceof ClassName
```

### Example:

```java
public class InstanceofDemo {
    public static void main(String[] args) {
        String name = "Java";
        Integer num = 100;

        System.out.println(name instanceof String);  // true
        System.out.println(num instanceof Integer);  // true
        System.out.println(name instanceof Object);  // true (every class extends Object)

        // With inheritance
        Animal animal = new Dog();
        System.out.println(animal instanceof Dog);    // true
        System.out.println(animal instanceof Animal); // true
    }
}

class Animal {}
class Dog extends Animal {}
```

**Output:**
```
true
true
true
true
true
```

### When to use:
- Before **type casting** an object to avoid `ClassCastException`.
- To check object type in **polymorphism** scenarios.

---

## Operator Precedence

Operator precedence determines the **order** in which operators are evaluated in an expression. Operators with higher precedence are evaluated first.

| Priority | Operators | Description |
|----------|-----------|-------------|
| 1 (Highest) | `()` | Parentheses |
| 2 | `++`, `--`, `!`, `~` | Unary operators |
| 3 | `*`, `/`, `%` | Multiplication, Division, Modulus |
| 4 | `+`, `-` | Addition, Subtraction |
| 5 | `<<`, `>>`, `>>>` | Shift operators |
| 6 | `<`, `<=`, `>`, `>=`, `instanceof` | Relational |
| 7 | `==`, `!=` | Equality |
| 8 | `&` | Bitwise AND |
| 9 | `^` | Bitwise XOR |
| 10 | `|` | Bitwise OR |
| 11 | `&&` | Logical AND |
| 12 | `||` | Logical OR |
| 13 | `? :` | Ternary |
| 14 (Lowest) | `=`, `+=`, `-=`, etc. | Assignment |

### Tips:
- Use **parentheses `()`** to make precedence clear and avoid confusion.
- When in doubt, add brackets — it improves readability.

---

## Quick Revision

- **Arithmetic** → `+`, `-`, `*`, `/`, `%` → basic math operations.
- **Unary** → `++`, `--`, `+`, `-`, `!` → works on single operand.
- **Prefix (`++a`)** → increment first, then use the value.
- **Postfix (`a++`)** → use the value first, then increment.
- **Assignment** → `=`, `+=`, `-=` → assigns values to variables.
- **Relational** → `==`, `!=`, `>`, `<`, `>=`, `<=` → compares values, returns boolean.
- **No value is greater or less than itself** → `30 > 30` is `false`.
- **Logical AND (`&&`)** → ALL conditions must be true → result is true.
- **Logical OR (`||`)** → At least ONE condition must be true → result is true.
- **Logical operators join multiple conditions** to produce one boolean result.
- **Bitwise** → `&`, `|`, `^`, `~` → operates on bits (rarely used in applications).
- **Shift** → `<<`, `>>` → multiplies/divides by powers of 2.
- **Ternary** → `condition ? trueValue : falseValue` → shorthand for if-else.
- **instanceof** → checks if object belongs to a class → returns boolean.
- **Use parentheses** to control evaluation order.
- **Short-circuit:** `&&` stops at first `false`; `||` stops at first `true`.

---

## Conclusion

Operators are the foundation of writing logic in Java. Every condition, calculation, and decision in your programs uses operators. Understanding how each operator works — especially prefix vs postfix, AND vs OR, and the ternary operator — is crucial for writing correct logic.

**Key Takeaways:**
1. Practice increment/decrement operators (prefix & postfix) thoroughly — they appear in loops and interviews.
2. Know when to use `&&` (all must pass) vs `||` (any one can pass).
3. The ternary operator is a compact alternative to simple if-else.
4. Relational operators always return boolean values.
5. Don't just execute code — analyze it mentally first, then verify with output.

> *"Think as a Java compiler, think as a Java executor."* — Practice step-by-step analysis to build strong logical thinking.

---
