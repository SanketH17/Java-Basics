# Java Packages & Naming Conventions - Complete Beginner Notes

---

## Table of Contents

1. [Packages in Java](#1-packages-in-java)
2. [Package and Import Statements](#2-package-and-import-statements)
3. [Predefined vs User-Defined Packages](#3-predefined-vs-user-defined-packages)
4. [The java.lang Default Package](#4-the-javalang-default-package)
5. [Naming Conventions in Java](#5-naming-conventions-in-java)
6. [Summary](#6-summary)

---

## 1. Packages in Java

### What is a Package?

A **package** in Java is simply a **folder (directory)** that contains related Java classes, interfaces, and other files. It is used to organize your code into logical groups.

> Think of it like organizing files on your computer — you create folders like "Movies", "Documents", "Photos" to keep things organized. Packages do the same for Java code.

---

### Why Use Packages?

| Benefit | Explanation |
|---------|-------------|
| **Organization** | Group related classes together (e.g., all payment-related classes in one package) |
| **Avoid naming conflicts** | Two classes can have the same name if they are in different packages |
| **Access control** | Packages work with access modifiers to control visibility |
| **Reusability** | Easier to find and reuse classes when organized properly |
| **Maintainability** | Easier to manage large projects with hundreds of classes |

---

### Real-World Analogy

Without packages:
```
src/
├── Student.java
├── Product.java
├── Calculator.java
├── Order.java
├── Payment.java
├── Login.java
└── ... (hundreds of files in one place — messy!)
```

With packages:
```
src/
├── com/myapp/student/
│   ├── Student.java
│   └── StudentService.java
├── com/myapp/product/
│   ├── Product.java
│   └── ProductService.java
├── com/myapp/payment/
│   ├── Payment.java
│   └── PaymentService.java
└── com/myapp/auth/
    ├── Login.java
    └── AuthService.java
```

---

### How to Create a Package

Use the `package` keyword as the **first line** of your Java file:

```java
package com.myapp.student;

public class Student {
    String name;
    int age;
}
```

**Rules:**
- `package` statement must be the **first line** of the Java file (before any import or class declaration)
- Only **one** package statement per file
- Package name represents the folder structure (dots = subfolders)

---

### Package = Folder Structure

The dot (`.`) in a package name creates **subfolders**:

```java
package com.instagram.orders;
```

This creates the folder structure:
```
com/
└── instagram/
    └── orders/
        └── YourClass.java
```

---

## 2. Package and Import Statements

### Accessing Classes from Different Packages

When you want to use a class from **another package**, there are two scenarios:

#### Scenario 1: Both Classes in the Same Package → No Import Needed

```java
// File: com/myapp/Calculator.java
package com.myapp;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

```java
// File: com/myapp/Main.java
package com.myapp;

// No import needed — both classes are in the same package
public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(10, 20)); // 30
    }
}
```

#### Scenario 2: Classes in Different Packages → Import Required

```java
// File: com/myapp/utils/MathHelper.java
package com.myapp.utils;

public class MathHelper {
    public static int square(int n) {
        return n * n;
    }
}
```

```java
// File: com/myapp/main/App.java
package com.myapp.main;

import com.myapp.utils.MathHelper; // Import required — different package

public class App {
    public static void main(String[] args) {
        int result = MathHelper.square(5);
        System.out.println(result); // 25
    }
}
```

---

### Import Statement Syntax

```java
import packageName.ClassName;
```

- Import tells the compiler: "This class I'm using exists in this specific package"
- Must come **after** the package statement and **before** the class declaration

---

### Import All Classes from a Package

Use the wildcard `*` to import all classes from a package:

```java
import com.myapp.utils.*;  // Imports ALL classes from this package
```

> **Note:** Wildcard import does **not** import sub-packages. Each sub-package needs its own import.

---

### File Structure Order

Every Java file follows this order:

```java
package com.myapp.student;          // 1. Package declaration (first line)

import com.myapp.utils.MathHelper;  // 2. Import statements
import java.util.ArrayList;

public class Student {               // 3. Class declaration
    // class body
}
```

| Order | Statement | Required? |
|-------|-----------|-----------|
| 1st | `package` | Optional (but always used in real projects) |
| 2nd | `import` | Only when using classes from other packages |
| 3rd | `class` | Always required |

---

### When is Import NOT Needed?

1. **Same package** — Classes in the same package can access each other directly
2. **java.lang package** — Classes from `java.lang` are auto-imported (explained below)

---

## 3. Predefined vs User-Defined Packages

### Predefined Packages (Built-in)

Packages already provided by the Java language. They contain ready-to-use classes.

| Package | Contains | Example Classes |
|---------|----------|----------------|
| `java.lang` | Core language classes | `String`, `Math`, `Integer`, `System`, `Object` |
| `java.util` | Utility classes | `ArrayList`, `HashMap`, `Scanner`, `Date` |
| `java.io` | Input/Output classes | `File`, `FileReader`, `BufferedReader` |
| `java.net` | Networking classes | `URL`, `HttpURLConnection`, `Socket` |
| `java.sql` | Database classes | `Connection`, `Statement`, `ResultSet` |
| `java.time` | Date/Time API | `LocalDate`, `LocalTime`, `DateTimeFormatter` |

```java
import java.util.Scanner;      // From java.util package
import java.util.ArrayList;    // From java.util package
import java.io.File;           // From java.io package

public class Demo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<String> list = new ArrayList<>();
        File f = new File("data.txt");
    }
}
```

---

### User-Defined Packages

Packages created by the developer for their own project.

```java
package com.swiggy.delivery;

public class DeliveryPartner {
    String name;
    String vehicleType;

    public void deliver(String orderId) {
        System.out.println(name + " is delivering order: " + orderId);
    }
}
```

---

### How to Find Predefined Packages and Classes

Use the **Java API Documentation**:
- URL: [https://docs.oracle.com/en/java/javase/17/docs/api/](https://docs.oracle.com/en/java/javase/17/docs/api/)
- Browse packages, see all classes within each package
- Check method signatures, return types, parameters, etc.

---

## 4. The java.lang Default Package

### What Makes java.lang Special?

`java.lang` is the **default package** in Java. Any class from this package is **automatically imported** — you never need to write an import statement for it.

```java
// No import needed for String, System, Math, Integer, etc.
public class Demo {
    public static void main(String[] args) {
        String name = "Java";              // String is from java.lang
        int max = Math.max(10, 20);        // Math is from java.lang
        System.out.println(name + " " + max); // System is from java.lang
    }
}
```

### Common java.lang Classes (No Import Needed)

| Class | Purpose |
|-------|---------|
| `String` | Text handling |
| `System` | Standard I/O, environment |
| `Math` | Mathematical operations |
| `Integer`, `Double`, `Float`, etc. | Wrapper classes |
| `Object` | Root class of all Java classes |
| `Thread` | Multi-threading |
| `Exception`, `RuntimeException` | Error handling |
| `StringBuilder` | Mutable strings |

### Rule to Remember

| Package | Import Required? |
|---------|-----------------|
| `java.lang` | **No** — auto-imported |
| Any other package (`java.util`, `java.io`, etc.) | **Yes** — must import |
| Same package classes | **No** — directly accessible |

---

## 5. Naming Conventions in Java

### What Are Naming Conventions?

Naming conventions are **guidelines** (not rules) for giving names to classes, methods, variables, packages, and constants in Java.

> **Important:** Breaking naming conventions will **NOT** cause compiler errors. Your program will still work. But following them makes your code professional, readable, and consistent with the Java community worldwide.

---

### Why Follow Naming Conventions?

- Code becomes **readable** and **understandable** by any developer
- Maintains **consistency** across teams and projects
- Shows **professionalism** in interviews and at work
- Java's own libraries follow these conventions — you should too

---

### Convention 1: Class Names — PascalCase

**Rule:** Every word's first letter should be **uppercase**, remaining letters **lowercase**.

This is called **PascalCase** (or UpperCamelCase).

```java
// ✅ Correct — follows naming convention
public class Student { }
public class StudentInformation { }
public class ProductDetails { }
public class OrderHistory { }
public class BankAccountService { }

// ❌ Incorrect — does NOT follow naming convention (but still compiles)
public class student { }           // first letter lowercase
public class STUDENT { }           // all uppercase
public class studentInformation { } // first letter lowercase
public class Productdetails { }    // 'd' should be uppercase
```

**Java's own classes follow this:**
- `String`, `ArrayList`, `HashMap`, `IOException`
- `ArrayIndexOutOfBoundsException` (6 words — each starts with uppercase)
- `StringBuilder`, `FileReader`, `HttpURLConnection`

---

### Convention 2: Variable Names — camelCase

**Rule:** First word starts with **lowercase**, every subsequent word starts with **uppercase**.

This is called **camelCase** (or lowerCamelCase).

```java
// ✅ Correct
int age = 25;
String fullName = "Rahul Kumar";
double averageMarks = 85.5;
int numberOfStudents = 60;
String collegeName = "ABC College";
boolean isActive = true;

// ❌ Incorrect (works but not standard)
int Age = 25;                  // starts with uppercase
String FULLNAME = "Rahul";     // all uppercase (reserved for constants)
int numberofstudents = 60;     // no separation between words
String college_name = "ABC";   // underscore style (not Java convention)
```

---

### Convention 3: Method Names — camelCase

**Rule:** Same as variables — first word lowercase, subsequent words start with uppercase.

```java
// ✅ Correct
public void getStudentName() { }
public int calculateTotal() { }
public void printAllDetails() { }
public boolean isEligible() { }
public String getCollegeName() { }

// ❌ Incorrect (works but not standard)
public void GetStudentName() { }    // starts with uppercase
public void CALCULATE_TOTAL() { }   // all uppercase with underscores
public void printstudentinfo() { }  // no word separation
```

---

### Convention 4: Package Names — all lowercase

**Rule:** Package names should be entirely in **lowercase**. Use dots to separate levels. Typically starts with the reverse domain name.

```java
// ✅ Correct
package com.instagram.orders;
package com.swiggy.delivery.tracking;
package org.apache.commons.lang;
package com.myapp.utils;

// ❌ Incorrect (works but not standard)
package Com.Instagram.Orders;     // uppercase letters
package com.Swiggy.Delivery;      // mixed case
package COM.MYAPP.UTILS;          // all uppercase
```

**Real-world pattern:**
```
package <reverse-domain>.<project>.<module>.<feature>;

// Examples:
package com.amazon.ecommerce.orders;
package com.google.maps.navigation;
package com.mycompany.hrms.employee;
```

---

### Convention 5: Constants — UPPER_SNAKE_CASE

**Rule:** Constants (final variables) should be all **UPPERCASE** with words separated by **underscores**.

```java
// ✅ Correct
public static final int MAX_STUDENTS = 100;
public static final double PI_VALUE = 3.14159;
public static final String DATABASE_URL = "jdbc:mysql://localhost:3306/mydb";
public static final int HTTP_STATUS_OK = 200;

// ❌ Incorrect
public static final int maxStudents = 100;     // camelCase — not for constants
public static final double piValue = 3.14;     // looks like a regular variable
```

---

### Convention 6: Interface Names — PascalCase (like classes)

```java
// ✅ Correct
public interface Serializable { }
public interface Comparable { }
public interface PaymentGateway { }
public interface UserRepository { }
```

> Some teams prefix interfaces with `I` (e.g., `IPaymentGateway`), but this is **not** the standard Java convention. Java's own interfaces don't use prefixes.

---

### Quick Reference Table

| Element | Convention | Style | Example |
|---------|-----------|-------|---------|
| Class | PascalCase | Every word capitalized | `StudentMarks` |
| Interface | PascalCase | Every word capitalized | `PaymentGateway` |
| Method | camelCase | First word lowercase | `calculateAverage()` |
| Variable | camelCase | First word lowercase | `totalMarks` |
| Package | all lowercase | No uppercase, dot-separated | `com.myapp.utils` |
| Constant | UPPER_SNAKE_CASE | All caps, underscore-separated | `MAX_VALUE` |

---

### Rules vs Conventions — The Difference

| Aspect | Rule | Convention |
|--------|------|-----------|
| What happens if broken? | **Compiler error** — program won't compile | **No error** — program works fine |
| Example of rule | Class name cannot have spaces | Class name should start with uppercase |
| Enforced by | Java compiler | Developer discipline |
| Required? | Yes (mandatory) | No (but strongly recommended) |

```java
// RULE broken — Compiler Error ❌
public class Student Information { }  // Space in class name — won't compile

// CONVENTION broken — No Error, but bad practice ⚠️
public class student_information { }  // Compiles fine, but not standard
```

---

## 6. Summary

### Packages — Key Points

| Point | Detail |
|-------|--------|
| What is a package? | A folder/directory to organize Java classes |
| Keyword | `package` (first line of file) |
| Dots in package name | Create sub-folders (`com.app.utils` → `com/app/utils/`) |
| Same package | No import needed |
| Different package | `import` statement required |
| `java.lang` | Auto-imported (no need to write import) |
| Wildcard import | `import java.util.*` (imports all classes from that package) |
| Real projects | 100% of real-time projects use packages — never skip them |

### Naming Conventions — Key Points

| Element | Convention | Example |
|---------|-----------|---------|
| Class | PascalCase | `StudentDetails` |
| Variable | camelCase | `studentName` |
| Method | camelCase | `getStudentName()` |
| Package | all lowercase | `com.myapp.student` |
| Constant | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |

### Golden Rules

1. **Package statement** is always the **first line** in a Java file
2. **Import statements** come **after** package, **before** class
3. **Same package** → no import; **Different package** → import required
4. **java.lang** is the only package that doesn't need import
5. Follow naming conventions — your code should look professional even without comments
6. Naming conventions won't break your code, but breaking them shows lack of professionalism

---

> **Pro Tip:** If you open any Java library class (`String.java`, `ArrayList.java`, etc.), you'll see that Java's own developers follow all these naming conventions perfectly. Follow their lead.

---