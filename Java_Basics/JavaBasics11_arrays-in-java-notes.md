# Arrays in Java and Array Operations

---

## 1. Introduction

In Java, when you work with a single value, you use a simple variable. But in real-world applications (like Flipkart, banking apps, etc.), you almost always deal with **more than one value** at a time — a list of prices, a list of student names, a group of product IDs, and so on.

**Arrays** are the most basic and fundamental data structure available in every programming language — C, C++, Java, Python, JavaScript, and more. Understanding arrays deeply is essential because:

- They form the foundation for more advanced topics like the **Collections Framework** in Java.
- They are one of the **most commonly asked topics in interviews**.
- Interviewers test your **thought process** and **core programming skills** through array-based questions.

---

## 2. What is an Array?

An array is a **reference that points to a group of values** of the **same data type**.

- A regular variable holds **only one value** at a time.
- An array allows you to hold **multiple values** under a single variable name.

```java
// A regular variable — holds only one value
int price = 99;

// An array — holds multiple values
int[] prices = {99, 88, 77, 66, 55};
```

**Key point:** In Java, you **cannot** store more than one value in a single regular variable.

```java
// This is NOT allowed in Java
int number = 10, 20; // Compile-time error
```

If you need to store more than one value, you must use an **array**.

---

## 3. Why Do We Use Arrays?

| Situation | What to Use |
|---|---|
| You have a **single value** to work with | Use a simple variable |
| You have **more than one value** (a group of values) | Use an array |

### Real-Life Analogies

1. **Book Index Analogy:**
   A book has a page number index. Page 1 has Topic A, Page 150 has Arrays, Page 200 has Collections, and so on. Using the index, you can directly jump to a specific page. Similarly, arrays use an **index** to directly access a specific value.

2. **Student Register Analogy:**
   In a classroom, every student has a unique ID (Roll Number). If you call "Student Number 5", only that student responds. Similarly, in an array, each value has a unique **index number**, and you access it using that index.

---

## 4. Array Declaration, Creation, and Initialization

In Java, arrays are always declared using **square braces `[]`**. Wherever you see `[]` in Java, it represents an array.

There are **two main ways** to create arrays:

### Way 1: Array Literal (Direct Initialization)

Use this when you **already know the values** at the time of creating the array.

**Syntax:**
```java
dataType[] arrayName = {value1, value2, value3, ...};
```

**Examples:**

```java
// Integer array
int[] numbers = {1, 4, 7, 8, 9};

// Double array
double[] prices = {99.99, 88.88, 44.56};

// String array
String[] products = {"iPhone 16", "iPhone 16 Pro", "iPhone 16 Pro Max"};
```

- You do **not** specify the size — Java automatically determines it from the number of values.
- Array creation and value assignment happen **at the same time**.

### Way 2: Array Initialization (With Size)

Use this when you **don't have the values yet** but know **how many values** you will store later.

**Syntax:**
```java
dataType[] arrayName = new dataType[size];
```

**Examples:**

```java
// Create an integer array that can hold 5 values
int[] ages = new int[5];

// Create a string array that can hold 10 values
String[] names = new String[10];
```

- You specify the **maximum number of values** (size) the array can hold.
- JVM allocates consecutive memory locations for the given size.
- Values are **not assigned yet** — default values are filled in automatically.
- You assign values **later** using the index.

### Key Difference Between the Two Ways

| Feature | Array Literal | Array Initialization |
|---|---|---|
| Values provided at creation? | Yes | No |
| Size specified? | No (automatic) | Yes (manual) |
| Default values? | No (your values are used) | Yes (filled automatically) |
| When to use? | Values are ready | Values will come later |

---

## 5. Accessing Array Elements

Every value in an array is stored at a specific **position** called an **index**.

### Array Index Starts from 0

> In human life, counting starts from **1**. In Java (and most programming languages), index starts from **0**.

```
Values:  1    4    7    8    9
Index:   0    1    2    3    4
```

- Index `0` → First value
- Index `1` → Second value
- Index `2` → Third value
- ...and so on.

### Reading a Value from an Array

```java
int[] numbers = {1, 4, 7, 8, 9};

System.out.println(numbers[0]); // Output: 1  (first value)
System.out.println(numbers[2]); // Output: 7  (third value)
System.out.println(numbers[4]); // Output: 9  (fifth/last value)
```

### Storing a Value into an Array Using Index

```java
int[] ages = new int[5]; // Array with size 5, all values are 0

ages[0] = 25;  // Store 25 at index 0
ages[1] = 30;  // Store 30 at index 1
ages[4] = 22;  // Store 22 at index 4 (last position)
```

### Important Formulas

```
Last Index  = Array Size - 1
Array Size  = Last Index + 1
```

If an array has size **5**, the valid indexes are: `0, 1, 2, 3, 4` (last index = 4).

---

## 6. Length of an Array

Use the `.length` property to find out how many elements an array can hold.

```java
int[] numbers = {1, 4, 7, 8, 9};
System.out.println(numbers.length); // Output: 5
```

- `.length` gives the **total size** of the array, not the last index.
- Last index = `arrayName.length - 1`

---

## 7. Default Values in Arrays

When you create an array using the **initialization approach** (with `new`), JVM fills all positions with **default values** based on the data type:

| Data Type | Default Value |
|---|---|
| `int` | `0` |
| `long` | `0` |
| `double` | `0.0` |
| `float` | `0.0f` |
| `boolean` | `false` |
| `char` | `'\u0000'` (null character) |
| `String` (and all non-primitive types) | `null` |

```java
int[] nums = new int[3];
// nums → [0, 0, 0]

String[] names = new String[3];
// names → [null, null, null]

double[] prices = new double[3];
// prices → [0.0, 0.0, 0.0]
```

---

## 8. Common Errors in Arrays

### 8.1 ArrayIndexOutOfBoundsException

This error occurs when you try to access an index that **does not exist** in the array.

```java
int[] numbers = {10, 20, 30}; // Valid indexes: 0, 1, 2

System.out.println(numbers[3]); // ERROR! Index 3 does not exist
System.out.println(numbers[-1]); // ERROR! Negative index
```

**Rule:** Valid index range is `0` to `length - 1`.

### 8.2 Type Mismatch

All values in an array must belong to the **same data type** as declared.

```java
int[] numbers = {1, 4, 7, 8, 9.99}; // ERROR! 9.99 is not an int

// For a product details array, you can only store product objects
ProductDetails[] products = new ProductDetails[5];
products[0] = 99;       // ERROR! Cannot store int in a ProductDetails array
products[0] = "Hello";  // ERROR! Cannot store String in a ProductDetails array
```

### 8.3 Storing Multiple Values Without Array Syntax

```java
int number = 10, 20; // ERROR! A simple variable cannot hold multiple values
```

---

## 9. Array Operations

### 9.1 Traversing an Array

Traversing means visiting **each element** of the array one by one.

#### Using a Regular `for` Loop

```java
int[] numbers = {10, 20, 30, 40, 50};

for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

- `i = 0` → Start from the first index.
- `i < numbers.length` → Continue until the last index.
  - You can also write: `i <= numbers.length - 1` (same meaning).
- `i++` → Move to the next index one by one.

#### Using Enhanced `for` Loop (for-each Loop)

The for-each loop is a **simplified version** of the regular for loop. It picks up each value **directly** from the first to the last element.

```java
int[] numbers = {10, 20, 30, 40, 50};

for (int num : numbers) {
    System.out.println(num);
}
```

**Advantages of for-each loop:**
- No need to write starting point, ending point, or increment.
- No need to use index numbers.
- Cleaner and simpler syntax.

**Limitations of for-each loop:**
- Always goes **forward only** (first to last).
- Always increments by **+1** (no customization).
- Cannot start from a middle index or skip elements.
- Cannot modify elements during iteration (no index access).

| Feature | Regular `for` Loop | Enhanced `for-each` Loop |
|---|---|---|
| Index access | Yes | No |
| Custom start/end | Yes | No |
| Custom increment | Yes (e.g., +2, +3) | No (always +1) |
| Reverse traversal | Yes | No |
| Simplicity | Moderate | Very simple |

---

### 9.2 Printing Array Elements

#### Print All Elements (Forward)

```java
String[] names = {"Alice", "Bob", "Charlie", "Diana"};

for (int i = 0; i < names.length; i++) {
    System.out.println("Index " + i + " → " + names[i]);
}
```

**Output:**
```
Index 0 → Alice
Index 1 → Bob
Index 2 → Charlie
Index 3 → Diana
```

#### Print All Elements in Reverse

```java
String[] names = {"Alice", "Bob", "Charlie", "Diana"};

for (int i = names.length - 1; i >= 0; i--) {
    System.out.println(names[i]);
}
```

**Output:**
```
Diana
Charlie
Bob
Alice
```

---

### 9.3 Taking Input in an Array

Use `Scanner` to take values from the user and store them in an array.

```java
import java.util.Scanner;

public class ArrayInput {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int[] marks = new int[5];

        System.out.println("Enter 5 marks:");
        for (int i = 0; i < marks.length; i++) {
            marks[i] = sc.nextInt();
        }

        System.out.println("You entered:");
        for (int mark : marks) {
            System.out.println(mark);
        }

        sc.close();
    }
}
```

---

### 9.4 Updating Array Elements

You can update any element by assigning a new value to a specific index.

```java
int[] numbers = {10, 20, 30, 40, 50};

numbers[2] = 99; // Update index 2 from 30 to 99

// numbers → {10, 20, 99, 40, 50}
```

---

### 9.5 Sum of Array Elements

```java
int[] numbers = {10, 20, 30, 40, 50};
int sum = 0;

for (int i = 0; i < numbers.length; i++) {
    sum = sum + numbers[i];
}

System.out.println("Sum: " + sum); // Output: Sum: 150
```

---

### 9.6 Average of Array Elements

```java
int[] numbers = {10, 20, 30, 40, 50};
int sum = 0;

for (int num : numbers) {
    sum += num;
}

double average = (double) sum / numbers.length;
System.out.println("Average: " + average); // Output: Average: 30.0
```

---

### 9.7 Maximum Element in an Array

```java
int[] numbers = {25, 11, 47, 8, 33};
int max = numbers[0]; // Assume first element is the largest

for (int i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
        max = numbers[i];
    }
}

System.out.println("Maximum: " + max); // Output: Maximum: 47
```

---

### 9.8 Minimum Element in an Array

```java
int[] numbers = {25, 11, 47, 8, 33};
int min = numbers[0]; // Assume first element is the smallest

for (int i = 1; i < numbers.length; i++) {
    if (numbers[i] < min) {
        min = numbers[i];
    }
}

System.out.println("Minimum: " + min); // Output: Minimum: 8
```

---

### 9.9 Searching an Element in an Array

Check whether a given value exists in the array (Linear Search).

```java
int[] numbers = {10, 25, 30, 45, 50};
int target = 30;
boolean found = false;

for (int i = 0; i < numbers.length; i++) {
    if (numbers[i] == target) {
        System.out.println(target + " found at index " + i);
        found = true;
        break;
    }
}

if (!found) {
    System.out.println(target + " not found in the array");
}
```

---

### 9.10 Copying an Array

Copy all elements from one array into another.

```java
int[] original = {10, 20, 30, 40, 50};
int[] copy = new int[original.length];

for (int i = 0; i < original.length; i++) {
    copy[i] = original[i];
}

// Verify
for (int val : copy) {
    System.out.print(val + " "); // Output: 10 20 30 40 50
}
```

---

### 9.11 Reversing an Array

Reverse the elements of an array in-place.

```java
int[] numbers = {10, 20, 30, 40, 50};

int start = 0;
int end = numbers.length - 1;

while (start < end) {
    // Swap elements at start and end
    int temp = numbers[start];
    numbers[start] = numbers[end];
    numbers[end] = temp;

    start++;
    end--;
}

// Print reversed array
for (int num : numbers) {
    System.out.print(num + " "); // Output: 50 40 30 20 10
}
```

---

## 10. Arrays of Non-Primitive Types (Object Arrays)

You can create arrays not just for primitive types (`int`, `double`, etc.) but also for **class types** (non-primitive / objects).

```java
class ProductDetails {
    public int id;
    public String name;
    public double price;
}
```

### Creating an Object Array

```java
// Using initialization (with size)
ProductDetails[] products = new ProductDetails[5];
// All 5 positions are initially null

// Creating and storing an object
products[0] = new ProductDetails();
products[0].id = 101;
products[0].name = "Mouse";
products[0].price = 999.0;
```

### Key Points for Object Arrays

- When you create an array of a class type, all positions are initialized with `null` (not actual objects).
- You must **create objects separately** and then store them at specific indexes.
- You can only store **objects of that specific class** in the array.
- Storing an `int` or `String` value directly into a `ProductDetails[]` array will cause a **compile-time error**.

```java
// This will NOT work
products[1] = 99;       // Error: incompatible types
products[1] = "Hello";  // Error: incompatible types

// This WILL work
products[1] = new ProductDetails(); // Correct: storing an object of the matching type
```

### Using Array Literal with Objects

```java
ProductDetails p1 = new ProductDetails();
p1.id = 101;
p1.name = "Keyboard";
p1.price = 1500.0;

ProductDetails p2 = new ProductDetails();
p2.id = 102;
p2.name = "Mouse";
p2.price = 999.0;

ProductDetails[] products = {p1, p2}; // Array literal with objects
```

---

## 11. Quick Revision

| Concept | Summary |
|---|---|
| **Array** | A reference that holds a group of values of the same data type |
| **Declaration (Literal)** | `int[] nums = {1, 2, 3};` |
| **Declaration (Initialization)** | `int[] nums = new int[5];` |
| **Index** | Position of an element; starts from **0** |
| **Last Index** | `array.length - 1` |
| **Length** | `arrayName.length` gives total number of elements |
| **Default Values** | `int → 0`, `double → 0.0`, `boolean → false`, `String → null` |
| **For Loop** | Full control: custom start, end, and increment |
| **For-Each Loop** | Simple: no index, always forward, always +1 |
| **Object Array** | Stores objects of a class; default value is `null` |
| **Common Error** | `ArrayIndexOutOfBoundsException` when index is out of range |
| **Square Braces `[]`** | Always represent arrays in Java |

### One-Liner Formulas

```
Last Index  = Size - 1
Size        = Last Index + 1
Valid Index  = 0 to (length - 1)
```

---

## 12. Common Interview / Practice Questions

These are commonly asked in interviews to test your **core logic and thought process**:

1. **Find the sum of all elements** in an array.
2. **Find the average** of array elements.
3. **Find the maximum and minimum** values in an array.
4. **Reverse an array** without using a second array.
5. **Search for an element** in an array (Linear Search).
6. **Count occurrences** of a specific element in an array.
7. **Find duplicate values** in an array.
   - Example: `{10, 30, 10, 44, 99, 30, 22, 66}` → Duplicates: `10, 30`
8. **Find duplicate characters** in a String (convert String to char array first).
9. **Copy an array** into another array.
10. **Sort an array** in ascending/descending order.
11. **Merge two arrays** into a single array.
12. **Remove a specific element** from an array.

> **Why do interviewers ask array questions even though we use Collections in real projects?**
>
> - They want to test your **thought process** — how you iterate, how you use loops, conditions, and variables.
> - They observe whether you write **clean, optimized logic** with proper syntax.
> - The **Collections Framework is built on top of arrays internally**. If you understand arrays well, Collections become much easier.
> - In advanced roles, you may need to **build custom frameworks** or write manual logic where core skills are essential.

---

## 13. Final Notes

- **Arrays are the foundation** of data structures. Master them before moving to Collections.
- Practice these operations **manually** — don't jump to shortcuts like Stream API during practice.
- Start with **small examples**, then gradually move to **complex problems**.
- The `main` method in Java uses `String[] args` — this is a **String array** that accepts command-line arguments. You will understand it better after learning arrays.
- In real-time projects, developers use the **Collections Framework** for convenience, but the **core concepts remain the same** as arrays.
- Keep practicing — these questions build the **programming mindset** that interviewers look for.

---
