# Wrapper Classes in Java

---

## 1. Introduction

### What Are Wrapper Classes?

In Java, we have **8 primitive data types** (`int`, `char`, `double`, `boolean`, etc.) that are simple keywords used to define variables and hold values. But **primitives are not objects** — they are just raw values.

**Wrapper classes** are special classes provided by Java that "wrap" each primitive data type into an **object**. They convert primitive values into object format.

> **Analogy:** Think of a wrapper class like a gift box. The actual value (gift) is the primitive, and the wrapper class is the box that wraps around it — turning it into an object.

### Why Are Wrapper Classes Needed?

- **Java claims to be 100% object-oriented**, but primitives are not objects. Wrapper classes fill this gap.
- **Collections (like ArrayList) only accept objects**, not primitives. So you must use wrapper classes to store numeric/character/boolean data in collections.
- Wrapper classes provide **useful methods** for converting, comparing, and manipulating data.
- They allow **null values**, which primitives cannot hold.

> **Key Rule:** By default, use primitives for everyday variables. Use wrapper classes **only when the requirement demands objects** (e.g., collections, generics, null handling).

---

## 2. Primitive Data Types vs Wrapper Classes

| Primitive Type | Wrapper Class | Size    | Default Value |
|----------------|---------------|---------|---------------|
| `byte`         | `Byte`        | 1 byte  | `0`           |
| `short`        | `Short`       | 2 bytes | `0`           |
| `int`          | `Integer`     | 4 bytes | `0`           |
| `long`         | `Long`        | 8 bytes | `0L`          |
| `float`        | `Float`       | 4 bytes | `0.0f`        |
| `double`       | `Double`      | 8 bytes | `0.0`         |
| `char`         | `Character`   | 2 bytes | `'\u0000'`    |
| `boolean`      | `Boolean`     | 1 bit   | `false`       |

### Key Differences

| Feature              | Primitive          | Wrapper Class       |
|----------------------|--------------------|---------------------|
| Type                 | Keyword            | Class (Object)      |
| Memory               | Stack              | Heap                |
| Default value        | Has a default      | `null`              |
| Can be used in Collections? | No          | Yes                 |
| Has methods?         | No                 | Yes                 |
| Package              | —                  | `java.lang` (auto-imported) |

> **Note:** All wrapper classes belong to the `java.lang` package, so you **do not need to import** them.

---

## 3. Creating Wrapper Objects

### Method 1: Using Constructors (Deprecated since Java 9)

```java
Integer age = new Integer(25);      // Deprecated ⚠️
Double price = new Double(99.99);   // Deprecated ⚠️
```

- Java shows a **strikethrough line** and a **warning**: _"The constructor Integer(int) has been deprecated since version 9 and marked for removal."_
- **Deprecated** means this approach is **not recommended** and **will be removed** in a future Java version.
- Java has found a **better, more memory-efficient** alternative.

> **What does "Deprecated" mean?**
> It is a warning/notice from Java saying: _"Don't use this old option. We have a better solution. This old one will be removed in a future version."_
> It's like Windows 7 being deprecated — it still works for now, but Microsoft stopped supporting it and recommends upgrading to Windows 10/11.

### Method 2: Using `valueOf()` (Recommended)

```java
Integer age = Integer.valueOf(25);       // Recommended ✅
Double price = Double.valueOf(99.99);    // Recommended ✅
Boolean flag = Boolean.valueOf(true);    // Recommended ✅
Character ch = Character.valueOf('A');   // Recommended ✅
```

- This is the **recommended way** to create wrapper objects.
- No warning, no deprecation.

---

## 4. Autoboxing and Unboxing

This is one of the most important concepts related to wrapper classes.

### What is Autoboxing?

**Autoboxing** = Automatic conversion from **primitive → wrapper object**.

Java allows you to assign a primitive value directly to a wrapper class reference — **no extra code needed**.

```java
int year = 2024;
Integer year1 = year;  // Autoboxing: int → Integer (automatic)
```

> **Analogy:** Autoboxing is like putting a gift inside a box (wrapping it). The value goes into the wrapper object automatically.

**More examples:**

```java
double price = 88.99;
Double price1 = price;       // Autoboxing: double → Double

char firstChar = 'D';
Character ch = firstChar;    // Autoboxing: char → Character

boolean status = true;
Boolean flag = status;       // Autoboxing: boolean → Boolean
```

### What is Unboxing?

**Unboxing** = Automatic conversion from **wrapper object → primitive**.

```java
Integer age = Integer.valueOf(40);
int age2 = age;  // Unboxing: Integer → int (automatic)
```

> **Analogy:** Unboxing is like opening a chocolate wrapper — you open the wrapper (object) and take out the actual value (primitive).

**More examples:**

```java
Double price1 = Double.valueOf(88.99);
double price2 = price1;     // Unboxing: Double → double

Character ch = Character.valueOf('D');
char letter = ch;            // Unboxing: Character → char
```

### Combined Example

```java
int a = 10;
Integer b = a;     // Autoboxing: primitive → wrapper
int c = b;         // Unboxing: wrapper → primitive
Integer d = c;     // Autoboxing again

System.out.println(a);  // 10
System.out.println(b);  // 10
System.out.println(c);  // 10
System.out.println(d);  // 10
```

All conversions happen **automatically**. As a developer, you don't write any extra logic.

### Important Rule: Only Associated Types Work

Autoboxing/unboxing works **only between a primitive and its corresponding (associated) wrapper class**.

```java
int x = 10;
Integer y = x;    // ✅ int → Integer (associated)

int x = 10;
Double y = x;     // ❌ Compile Error! int → Double (not associated)

long m = 9;
Integer n = m;    // ❌ Compile Error! long → Integer (not associated)
```

> **Error message:** _"Type mismatch: cannot convert from long to Integer"_

---

## 5. Converting Between Types

### Primitive → Wrapper (Autoboxing)

```java
int num = 50;
Integer obj = num;  // Automatic
```

### Wrapper → Primitive (Unboxing)

```java
Integer obj = Integer.valueOf(50);
int num = obj;  // Automatic
```

### String → Primitive (Using `parseXxx()` Methods)

Each wrapper class provides a `parseXxx()` method to convert a **String into its corresponding primitive**.

```java
int a = Integer.parseInt("100");
double b = Double.parseDouble("45.67");
long c = Long.parseLong("999999");
float d = Float.parseFloat("3.14");
boolean e = Boolean.parseBoolean("true");
```

### String → Wrapper (Using `valueOf()`)

```java
Integer a = Integer.valueOf("100");
Double b = Double.valueOf("45.67");
Boolean c = Boolean.valueOf("true");
```

### Wrapper/Primitive → String

```java
// Using toString()
String s1 = Integer.toString(100);
String s2 = Double.toString(45.67);

// Using String.valueOf()
String s3 = String.valueOf(100);
String s4 = String.valueOf(true);

// Using concatenation (simplest)
String s5 = 100 + "";
String s6 = 45.67 + "";
```

---

## 6. Important Methods in Wrapper Classes

### `parseInt()` / `parseDouble()` / `parseLong()` etc.

Converts a **String** to a **primitive** value.

```java
int num = Integer.parseInt("42");
double price = Double.parseDouble("19.99");
```

### `valueOf()`

Converts a **primitive or String** into a **wrapper object**.

```java
Integer a = Integer.valueOf(42);
Integer b = Integer.valueOf("42");
```

### `toString()`

Converts a **wrapper object** to a **String**.

```java
Integer num = 100;
String s = num.toString();  // "100"
```

### `compareTo()`

Compares two wrapper objects. Returns:
- `0` → if both are equal
- Positive value → if the first is greater
- Negative value → if the first is smaller

```java
Integer a = 10;
Integer b = 20;

System.out.println(a.compareTo(b));  // -1 (a < b)
System.out.println(b.compareTo(a));  // 1  (b > a)
System.out.println(a.compareTo(10)); // 0  (equal)
```

### `equals()`

Compares two wrapper objects for **value equality**.

```java
Integer a = 100;
Integer b = 100;

System.out.println(a.equals(b));  // true (same value)
System.out.println(a == b);      // may be true or false (compares reference)
```

> **Tip:** Always use `.equals()` to compare wrapper objects, not `==`.

### Other Useful Methods

| Method               | Description                          |
|----------------------|--------------------------------------|
| `intValue()`         | Returns the `int` value              |
| `doubleValue()`      | Returns the `double` value           |
| `MAX_VALUE`          | Maximum value of that type           |
| `MIN_VALUE`          | Minimum value of that type           |
| `TYPE`               | Returns the primitive type class     |

```java
System.out.println(Integer.MAX_VALUE);  // 2147483647
System.out.println(Integer.MIN_VALUE);  // -2147483648
```

---

## 7. Use Cases of Wrapper Classes

### 1. Collections (ArrayList, HashMap, etc.)

Collections **only accept objects**, not primitives. You must use wrapper classes.

```java
// ❌ Not allowed
ArrayList<int> list = new ArrayList<>();

// ✅ Correct — use wrapper class
ArrayList<Integer> list = new ArrayList<>();
list.add(10);    // Autoboxing: int → Integer
list.add(20);
list.add(30);

int value = list.get(0);  // Unboxing: Integer → int
```

### 2. Null Value Handling

Primitives **cannot be null**, but wrapper objects **can**.

```java
int age = null;       // ❌ Compile Error
Integer age = null;   // ✅ Valid
```

This is useful when:
- A value might be absent (e.g., from a database query).
- You want to differentiate between "no value" and "zero."

### 3. Generics

Generic types require objects, not primitives.

```java
// ❌ Not allowed
Comparable<int> comp;

// ✅ Correct
Comparable<Integer> comp;
```

---

## 8. Common Errors

### NullPointerException During Unboxing

If a wrapper object is `null` and you try to unbox it, you get a **NullPointerException**.

```java
Integer num = null;
int value = num;  // ❌ NullPointerException at runtime!
```

**Fix:** Always check for `null` before unboxing.

```java
Integer num = null;
if (num != null) {
    int value = num;
}
```

### NumberFormatException

If you try to parse an invalid String into a number, you get a **NumberFormatException**.

```java
int a = Integer.parseInt("abc");    // ❌ NumberFormatException
int b = Integer.parseInt("12.5");   // ❌ NumberFormatException (not an integer)
int c = Integer.parseInt("100");    // ✅ Works fine
```

**Fix:** Validate the String before parsing, or use try-catch.

```java
try {
    int num = Integer.parseInt("abc");
} catch (NumberFormatException e) {
    System.out.println("Invalid number format!");
}
```

---

## 9. Best Practices

| Scenario                                    | Use            |
|---------------------------------------------|----------------|
| Simple variables, calculations              | **Primitive**  |
| Collections (ArrayList, HashMap, etc.)      | **Wrapper**    |
| Value might be null                         | **Wrapper**    |
| Performance-critical code                   | **Primitive**  |
| Generics / Type parameters                  | **Wrapper**    |
| Default / everyday coding                   | **Primitive**  |

### Summary Rules

- **By default, prefer primitives** — they are faster and use less memory.
- **Use wrapper classes only when required** — collections, generics, or null handling.
- **Do not create wrapper objects using `new` keyword** — it is deprecated since Java 9. Use `valueOf()` or direct assignment (autoboxing).
- **Use `.equals()` to compare wrapper objects**, not `==`.
- **Always check for `null`** before unboxing to avoid `NullPointerException`.

---

## 10. Quick Revision

- Java has **8 primitive types** → each has a corresponding **wrapper class**.
- Wrapper classes are in the `java.lang` package (no import needed).
- **Autoboxing** = primitive → wrapper (automatic).
- **Unboxing** = wrapper → primitive (automatic).
- Autoboxing/unboxing works **only between associated types** (e.g., `int` ↔ `Integer`, not `int` ↔ `Double`).
- Creating wrapper objects using **`new` keyword is deprecated** since Java 9. Use `valueOf()`.
- **Collections accept only objects**, so use wrapper classes there.
- `parseInt()`, `parseDouble()` → convert **String to primitive**.
- `valueOf()` → convert **String or primitive to wrapper object**.
- `toString()` → convert **wrapper to String**.
- **NullPointerException** occurs when unboxing a `null` wrapper.
- **NumberFormatException** occurs when parsing an invalid String.
- Prefer **primitives** for everyday use; use **wrappers** only when needed.

---

## 11. Practice / Interview Questions

**Q1.** What is the output of the following code?

```java
int a = 10;
Integer b = a;
int c = b;
System.out.println(a + " " + b + " " + c);
```

> **Answer:** `10 10 10` — Autoboxing converts `a` to `b`, unboxing converts `b` to `c`. All hold the same value.

---

**Q2.** Will the following code compile? Why or why not?

```java
long x = 100;
Integer y = x;
```

> **Answer:** No, it will **not compile**. Autoboxing only works between **associated** types. `long` is not associated with `Integer` — it is associated with `Long`.

---

**Q3.** What happens when this code runs?

```java
Integer num = null;
int value = num;
```

> **Answer:** It throws a **NullPointerException** at runtime. Unboxing a `null` wrapper object causes this exception.

---

**Q4.** Why is `new Integer(10)` not recommended?

> **Answer:** The constructor `Integer(int)` has been **deprecated since Java 9** and is marked for removal. Java recommends using `Integer.valueOf(10)` instead, which is more memory-efficient.

---

**Q5.** Why can't we use `int` directly in an `ArrayList`?

> **Answer:** `ArrayList` (and all collections) only accept **objects**, not primitives. We must use the wrapper class `Integer` instead of `int`.
> ```java
> ArrayList<Integer> list = new ArrayList<>();  // ✅ Correct
> ```

---

**Q6.** What is the difference between `==` and `.equals()` for wrapper objects?

> **Answer:**
> - `==` compares **references** (memory addresses).
> - `.equals()` compares **actual values**.
> - For wrapper objects, always use `.equals()` to compare values.
> ```java
> Integer a = 200;
> Integer b = 200;
> System.out.println(a == b);       // false (different objects)
> System.out.println(a.equals(b));  // true (same value)
> ```

---

*End of Notes*
