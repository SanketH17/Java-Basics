# Comparable in Java (Simple Explanation)

Think of **Comparable** as a way for an object to tell Java:

> **"If you want to compare two objects of my class, this is how you should compare them."**

For example:

- Students can be compared by **marks**
- Employees can be compared by **salary**
- Products can be compared by **price**

Without Comparable, Java doesn't know how to compare your custom objects.

---

# Real-Life Example

Imagine you're arranging books on a shelf.

Someone asks:

> "Arrange these books."

You'll naturally ask:

> "Arrange by what?"
>
> - Title?
> - Price?
> - Number of pages?

Comparable answers that question.

It defines **one natural/default way** to compare objects.

---

# Why do we need Comparable?

Java already knows how to sort numbers.

```java
List<Integer> numbers = Arrays.asList(5, 2, 9, 1);

Collections.sort(numbers);

System.out.println(numbers);
```

### Output

```text
[1, 2, 5, 9]
```

Why?

Because `Integer` already implements `Comparable`.

---

But suppose we have our own class.

```java
class Student {
    int id;
    String name;
    int marks;
}
```

Now we try:

```java
Collections.sort(studentList);
```

Java says:

```text
Cannot sort Student objects.
I don't know how to compare two students.
```

That's where Comparable comes in.

---

# Comparable Interface

```java
public interface Comparable<T> {

    int compareTo(T other);
}
```

It contains only one method:

```java
compareTo()
```

You write the comparison logic here.

---

# How compareTo() Works

Suppose we compare:

```text
this
```

with

```text
other
```

The method returns:

## Return 0

Both objects are equal.

```text
5 compared with 5

return 0
```

---

## Return Positive

Current object is bigger.

```text
10 compared with 5

return positive number
```

Example:

```text
10 - 5 = 5
```

---

## Return Negative

Current object is smaller.

```text
5 compared with 10

return negative number
```

Example:

```text
5 - 10 = -5
```

---

# Easy Way to Remember

```text
this.compareTo(other)

Negative -> this comes BEFORE other

Zero -> both are equal

Positive -> this comes AFTER other
```

---

# Example 1: Compare Students by Marks

```java
class Student implements Comparable<Student> {

    int marks;

    Student(int marks) {
        this.marks = marks;
    }

    @Override
    public int compareTo(Student other) {
        return this.marks - other.marks;
    }

    @Override
    public String toString() {
        return String.valueOf(marks);
    }
}
```

---

### Main Method

```java
List<Student> list = Arrays.asList(
        new Student(70),
        new Student(50),
        new Student(90),
        new Student(60)
);

Collections.sort(list);

System.out.println(list);
```

### Output

```text
[50, 60, 70, 90]
```

---

## What happened?

Java internally compares:

```text
70 with 50

70 - 50 = 20
```

Positive

So:

```text
70 comes after 50
```

Then:

```text
50 with 90

50 - 90 = -40
```

Negative

So:

```text
50 comes before 90
```

This keeps happening until everything is sorted.

---

# Visual Flow

Original List

```text
70
50
90
60
```

Java repeatedly calls:

```text
70.compareTo(50)

returns +20

↓

70 after 50
```

Next

```text
90.compareTo(60)

returns +30

↓

90 after 60
```

Eventually:

```text
50
60
70
90
```

---

# Example 2: Sort Employees by Salary

```java
class Employee implements Comparable<Employee> {

    String name;
    double salary;

    Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    @Override
    public int compareTo(Employee other) {
        return Double.compare(this.salary, other.salary);
    }

    @Override
    public String toString() {
        return name + " : " + salary;
    }
}
```

### Main Method

```java
List<Employee> employees = Arrays.asList(
        new Employee("A", 50000),
        new Employee("B", 30000),
        new Employee("C", 70000)
);

Collections.sort(employees);

System.out.println(employees);
```

### Output

```text
B : 30000
A : 50000
C : 70000
```

---

# Descending Order

If you want highest marks first,

instead of

```java
return this.marks - other.marks;
```

write

```java
return other.marks - this.marks;
```

### Output

```text
90
70
60
50
```

---

# Why not simply subtract for all types?

For integers, you'll often see:

```java
return this.marks - other.marks;
```

But this can overflow for very large integer values.

A safer approach is:

```java
return Integer.compare(this.marks, other.marks);
```

Similarly:

```java
Double.compare(this.salary, other.salary);

Long.compare(a, b);

Float.compare(a, b);
```

These methods are clearer and avoid overflow issues.

---

# Where is Comparable Used?

Java uses Comparable in many places:

```java
Collections.sort(list);
```

```java
Arrays.sort(array);
```

```java
TreeSet
```

```java
TreeMap
```

These classes need to know how objects should be ordered.

---

# Comparable vs Comparator

| Comparable | Comparator |
|------------|------------|
| Defined inside the class | Defined outside the class |
| One default sorting rule | Multiple sorting rules |
| Uses `compareTo()` | Uses `compare()` |
| Modifies the class | Doesn't require modifying the class |

Example:

Comparable

```text
Student

↓

Sort by Marks
```

Comparator

```text
Sort by Name

or

Sort by Age

or

Sort by City
```

We'll usually use **Comparable** when there is a single, natural ordering for the object, and **Comparator** when we need different ways to sort the same type.

---

# Interview Questions

### 1. What is Comparable in Java?

**Answer:**

Comparable is an interface that lets a class define its **natural/default ordering**. It contains the `compareTo()` method, which Java uses for sorting.

---

### 2. Why do we use Comparable?

**Answer:**

We use Comparable so Java knows how to compare and sort objects of a custom class.

---

### 3. Which method does Comparable provide?

```java
compareTo()
```

---

### 4. What does compareTo() return?

- **Negative** → Current object comes before the other object.
- **Zero** → Both objects are equal.
- **Positive** → Current object comes after the other object.

---

### 5. What happens if a class doesn't implement Comparable and you try to sort it?

**Answer:**

Java throws a **ClassCastException** (or won't know how to compare the objects), because it has no comparison logic for that class.

---

# Summary

- `Comparable` defines the **natural/default ordering** of objects.
- It has only one method: `compareTo()`.
- `Collections.sort()` and `Arrays.sort()` use `compareTo()` to arrange objects.
- Return a **negative** value if the current object should come first, **zero** if both are equal, and a **positive** value if it should come later.
- Prefer `Integer.compare()`, `Double.compare()`, etc., over subtraction for safer comparisons.


---


# Comparator in Java (Simple Explanation)

## What is Comparator?

Think of **Comparator** as an **external comparison rule**.

With **Comparable**, the object says:

> "Compare me using this rule."

With **Comparator**, **you** say:

> "Today, compare these objects using this rule."

This means **Comparator allows multiple ways to sort the same object.**

---

# Real-Life Example

Suppose you have a list of students.

```text
Rahul   90   22
Amit    75   20
Neha    90   19
```

You can arrange them by:

- Name
- Marks
- Age

Question:

**Which one is the correct sorting?**

Answer:

**All of them are correct!**

It depends on what you want.

This is exactly why Comparator exists.

---

# Why do we need Comparator?

Suppose our Student class is:

```java
class Student {
    int id;
    String name;
    int marks;
    int age;
}
```

Today you want to sort by marks.

Tomorrow by age.

Next week by name.

Can Comparable do this?

No.

Comparable supports **only one default sorting rule.**

Comparator lets us create **multiple sorting rules** without changing the Student class.

---

# Comparator Interface

```java
public interface Comparator<T> {

    int compare(T o1, T o2);
}
```

It has only one method:

```java
compare()
```

---

# How compare() Works

Suppose Java compares

```text
Student A

with

Student B
```

The compare() method returns

## Negative

First object comes before second.

```text
return -1
```

---

## Zero

Both are equal.

```text
return 0
```

---

## Positive

First object comes after second.

```text
return 1
```

---

# Easy Way to Remember

```text
compare(obj1, obj2)

Negative
↓

obj1 comes BEFORE obj2

----------------------------

Zero
↓

Both are equal

----------------------------

Positive
↓

obj1 comes AFTER obj2
```

---

# Our Student Class

```java
class Student {

    int id;
    String name;
    int marks;
    int age;

    Student(int id, String name, int marks, int age) {
        this.id = id;
        this.name = name;
        this.marks = marks;
        this.age = age;
    }

    @Override
    public String toString() {
        return id + " " + name + " " + marks + " " + age;
    }
}
```

---

# Our Student List

```java
List<Student> students = Arrays.asList(

        new Student(101, "Rahul", 90, 22),

        new Student(102, "Amit", 75, 20),

        new Student(103, "Neha", 90, 19),

        new Student(104, "Priya", 60, 21)

);
```

Current List

```text
101 Rahul 90 22
102 Amit 75 20
103 Neha 90 19
104 Priya 60 21
```

---

# Example 1 : Sort by Marks

## Step 1

Create Comparator

```java
Comparator<Student> marksComparator = new Comparator<Student>() {

    @Override
    public int compare(Student s1, Student s2) {

        return Integer.compare(s1.marks, s2.marks);

    }

};
```

---

## Step 2

Pass it to sort()

```java
Collections.sort(students, marksComparator);
```

---

## Output

```text
104 Priya 60 21

102 Amit 75 20

101 Rahul 90 22

103 Neha 90 19
```

---

# Let's Understand Every Comparison

Current List

```text
Rahul 90

Amit 75

Neha 90

Priya 60
```

Java internally does comparisons like this.

---

## Comparison 1

```text
Rahul (90)

Amit (75)
```

Java calls

```java
compare(Rahul, Amit)
```

Our method

```java
Integer.compare(90,75)
```

returns

```text
1
```

Positive means

```text
Rahul comes AFTER Amit
```

---

## Comparison 2

```text
Amit (75)

Priya (60)
```

Java calls

```java
compare(Amit, Priya)
```

returns

```java
Integer.compare(75,60)
```

returns

```text
1
```

Again

```text
Amit comes AFTER Priya
```

---

## Comparison 3

```text
Rahul (90)

Neha (90)
```

Java calls

```java
compare(Rahul, Neha)
```

returns

```java
Integer.compare(90,90)
```

returns

```text
0
```

Both have equal marks.

---

Eventually Java arranges them as

```text
60

↓

75

↓

90

↓

90
```

---

# Example 2 : Sort by Name

Now suppose we want alphabetical order.

Create another Comparator.

```java
Comparator<Student> nameComparator = new Comparator<Student>() {

    @Override
    public int compare(Student s1, Student s2) {

        return s1.name.compareTo(s2.name);

    }

};
```

Notice something interesting.

We are using

```java
compareTo()
```

Why?

Because **String already implements Comparable.**

---

Now

```java
Collections.sort(students, nameComparator);
```

Output

```text
Amit

Neha

Priya

Rahul
```

---

# Let's See One Comparison

Java compares

```text
Rahul

Amit
```

Calls

```java
compare(Rahul, Amit)
```

Inside

```java
Rahul.compareTo(Amit)
```

returns

Positive

because

```text
R comes after A
```

Therefore

```text
Amit comes first
```

---

# Example 3 : Sort by Age

Create another Comparator

```java
Comparator<Student> ageComparator = new Comparator<Student>() {

    @Override
    public int compare(Student s1, Student s2) {

        return Integer.compare(s1.age, s2.age);

    }

};
```

Now

```java
Collections.sort(students, ageComparator);
```

Output

```text
Neha 19

Amit 20

Priya 21

Rahul 22
```

---

# Three Different Sortings

Same Student objects

```text
Rahul

Amit

Neha

Priya
```

---

Sort by Marks

```text
Priya

Amit

Rahul

Neha
```

---

Sort by Name

```text
Amit

Neha

Priya

Rahul
```

---

Sort by Age

```text
Neha

Amit

Priya

Rahul
```

Same objects.

Different Comparator.

Different result.

---

# Lambda Version (Java 8+)

Instead of writing

```java
Comparator<Student> marksComparator = new Comparator<Student>() {

    @Override
    public int compare(Student s1, Student s2) {

        return Integer.compare(s1.marks, s2.marks);

    }

};
```

we can write

```java
Comparator<Student> marksComparator =
        (s1, s2) -> Integer.compare(s1.marks, s2.marks);
```

Even shorter

```java
students.sort(
        Comparator.comparingInt(student -> student.marks)
);
```

---

# Descending Order

Ascending

```java
Integer.compare(s1.marks, s2.marks)
```

Descending

```java
Integer.compare(s2.marks, s1.marks)
```

Or

```java
students.sort(
        Comparator.comparingInt((Student s) -> s.marks)
                  .reversed()
);
```

---

# Comparable vs Comparator

| Comparable | Comparator |
|------------|------------|
| Inside the class | Outside the class |
| One default sorting rule | Multiple sorting rules |
| Method is `compareTo()` | Method is `compare()` |
| Class must implement Comparable | No need to modify the class |
| Used for natural ordering | Used for custom ordering |

---

# When Should We Use Comparator?

Use Comparator when:

- You need more than one sorting rule.
- You cannot modify the class.
- You want custom sorting.
- You want temporary sorting.

---

# Interview Questions

## 1. What is Comparator?

**Answer:**

Comparator is an interface used to define **custom sorting logic** outside the class. It allows multiple ways to sort the same objects.

---

## 2. Why do we use Comparator?

**Answer:**

We use Comparator when we want different sorting orders, such as sorting students by marks, age, or name.

---

## 3. Which method does Comparator provide?

```java
compare(T o1, T o2)
```

---

## 4. What does compare() return?

- Negative → First object comes before the second.
- Zero → Both objects are equal.
- Positive → First object comes after the second.

---

## 5. Can we have multiple Comparators for one class?

**Answer:**

Yes. That's the main advantage of Comparator. We can create any number of Comparator objects for different sorting rules.

---

# Summary

- Comparator is used for **custom sorting**.
- It is defined **outside** the class.
- It has one method: `compare()`.
- One class can have multiple Comparator implementations.
- It is commonly used with `Collections.sort()`, `List.sort()`, and Java Streams.
- From Java 8 onwards, Comparators are usually written using **lambda expressions** and `Comparator.comparing()`.


---

# Complete Comparator Example (Step-by-Step)

In this example, we'll:

1. Create a `Student` class.
2. Create a list of students.
3. Sort the same list by:
   - Marks
   - Name
   - Age

---

# Step 1: Student Class

```java
class Student {

    int id;
    String name;
    int marks;
    int age;

    Student(int id, String name, int marks, int age) {
        this.id = id;
        this.name = name;
        this.marks = marks;
        this.age = age;
    }

    @Override
    public String toString() {
        return id + " " + name + " " + marks + " " + age;
    }
}
```

---

# Step 2: Main Program

```java
import java.util.*;

public class ComparatorDemo {

    public static void main(String[] args) {

        List<Student> students = new ArrayList<>();

        students.add(new Student(101, "Rahul", 90, 22));
        students.add(new Student(102, "Amit", 75, 20));
        students.add(new Student(103, "Neha", 90, 19));
        students.add(new Student(104, "Priya", 60, 21));

        System.out.println("Original List");
        System.out.println(students);

        // Sort by Marks
        Comparator<Student> marksComparator = new Comparator<Student>() {

            @Override
            public int compare(Student s1, Student s2) {

                return Integer.compare(s1.marks, s2.marks);

            }
        };

        Collections.sort(students, marksComparator);

        System.out.println("\nSorted By Marks");
        System.out.println(students);

        // Sort by Name
        Comparator<Student> nameComparator = new Comparator<Student>() {

            @Override
            public int compare(Student s1, Student s2) {

                return s1.name.compareTo(s2.name);

            }
        };

        Collections.sort(students, nameComparator);

        System.out.println("\nSorted By Name");
        System.out.println(students);

        // Sort by Age
        Comparator<Student> ageComparator = new Comparator<Student>() {

            @Override
            public int compare(Student s1, Student s2) {

                return Integer.compare(s1.age, s2.age);

            }
        };

        Collections.sort(students, ageComparator);

        System.out.println("\nSorted By Age");
        System.out.println(students);
    }
}
```

---

# Output

```text
Original List

[101 Rahul 90 22,
102 Amit 75 20,
103 Neha 90 19,
104 Priya 60 21]


Sorted By Marks

[104 Priya 60 21,
102 Amit 75 20,
101 Rahul 90 22,
103 Neha 90 19]


Sorted By Name

[102 Amit 75 20,
103 Neha 90 19,
104 Priya 60 21,
101 Rahul 90 22]


Sorted By Age

[103 Neha 90 19,
102 Amit 75 20,
104 Priya 60 21,
101 Rahul 90 22]
```

---

# Let's Understand the Flow

## Initial List

```text
Rahul 90 22
Amit 75 20
Neha 90 19
Priya 60 21
```

---

## 1) Sort by Marks

Java executes:

```java
Collections.sort(students, marksComparator);
```

Java internally starts comparing students.

### Comparison 1

```java
compare(Rahul, Amit)
```

Our code runs:

```java
Integer.compare(90, 75)
```

Returns:

```text
1
```

Meaning:

```text
Rahul comes AFTER Amit
```

---

### Comparison 2

```java
compare(Amit, Priya)
```

Runs:

```java
Integer.compare(75, 60)
```

Returns:

```text
1
```

Meaning:

```text
Amit comes AFTER Priya
```

---

### Comparison 3

```java
compare(Rahul, Neha)
```

Runs:

```java
Integer.compare(90, 90)
```

Returns:

```text
0
```

Meaning:

```text
Both have equal marks.
```

Eventually Java arranges them as:

```text
60

↓

75

↓

90

↓

90
```

Result:

```text
Priya
Amit
Rahul
Neha
```

---

## 2) Sort by Name

Now Java executes:

```java
Collections.sort(students, nameComparator);
```

The comparison method is now:

```java
return s1.name.compareTo(s2.name);
```

### Comparison

```java
compare(Rahul, Amit)
```

Runs:

```java
"Rahul".compareTo("Amit")
```

Since **R** comes after **A**, it returns a positive value.

Meaning:

```text
Rahul comes AFTER Amit
```

Another comparison:

```java
compare(Neha, Priya)
```

Runs:

```java
"Neha".compareTo("Priya")
```

Since **N** comes before **P**, it returns a negative value.

Meaning:

```text
Neha comes BEFORE Priya
```

Final result:

```text
Amit
Neha
Priya
Rahul
```

---

## 3) Sort by Age

Now Java executes:

```java
Collections.sort(students, ageComparator);
```

Comparison method:

```java
Integer.compare(s1.age, s2.age);
```

### Comparison

```java
compare(Rahul, Neha)
```

Runs:

```java
Integer.compare(22, 19)
```

Returns:

```text
1
```

Meaning:

```text
Rahul comes AFTER Neha
```

Another comparison:

```java
compare(Amit, Priya)
```

Runs:

```java
Integer.compare(20, 21)
```

Returns:

```text
-1
```

Meaning:

```text
Amit comes BEFORE Priya
```

Final result:

```text
Neha
Amit
Priya
Rahul
```

---

# Visual Flow

```text
               Student List
                     │
                     ▼
      Rahul 90 22
      Amit 75 20
      Neha 90 19
      Priya 60 21
                     │
                     ▼
     Collections.sort(students, marksComparator)
                     │
                     ▼
       compare(s1, s2)
                     │
                     ▼
 Integer.compare(s1.marks, s2.marks)
                     │
                     ▼
       Sorted by Marks
                     │
                     ▼
     Collections.sort(students, nameComparator)
                     │
                     ▼
       compare(s1, s2)
                     │
                     ▼
    s1.name.compareTo(s2.name)
                     │
                     ▼
       Sorted by Name
                     │
                     ▼
     Collections.sort(students, ageComparator)
                     │
                     ▼
       compare(s1, s2)
                     │
                     ▼
 Integer.compare(s1.age, s2.age)
                     │
                     ▼
        Sorted by Age
```

---

# Key Point to Remember

The **Student class never changes**.

We simply create different **Comparator** objects:

- `marksComparator` → Sort by marks
- `nameComparator` → Sort by name
- `ageComparator` → Sort by age

This is the biggest advantage of **Comparator**—you can sort the same objects in multiple ways without modifying the class.


----

# Examples :

## 1. Student

A Student can be sorted in many ways.

Fields:

```java
class Student {
    int rollNo;
    String name;
    int marks;
    int age;
}
```

## Comparable (Default Sorting)

Sort by **Roll Number** (Natural Order)

```java
@Override
public int compareTo(Student other) {
    return Integer.compare(this.rollNo, other.rollNo);
}
```

```java
Collections.sort(students);
```

Output

```text
101
102
103
104
```

---

## Comparator (Custom Sorting)

Sort by **Marks**

```java
Comparator<Student> marksComparator =
        (s1, s2) -> Integer.compare(s1.marks, s2.marks);

Collections.sort(students, marksComparator);
```

Output

```text
60
75
90
95
```

---

Sort by **Name**

```java
Comparator<Student> nameComparator =
        (s1, s2) -> s1.name.compareTo(s2.name);

Collections.sort(students, nameComparator);
```

Output

```text
Amit
Neha
Priya
Rahul
```

---

# 2. Employee

Fields

```java
class Employee {
    int employeeId;
    String name;
    double salary;
    String department;
}
```

## Comparable (Default Sorting)

Sort by **Employee ID**

```java
@Override
public int compareTo(Employee other) {
    return Integer.compare(this.employeeId, other.employeeId);
}
```

```java
Collections.sort(employees);
```

Output

```text
101
102
103
104
```

---

## Comparator (Custom Sorting)

Sort by **Salary**

```java
Comparator<Employee> salaryComparator =
        (e1, e2) -> Double.compare(e1.salary, e2.salary);

Collections.sort(employees, salaryComparator);
```

Output

```text
35000
50000
65000
80000
```

---

Sort by **Department**

```java
Comparator<Employee> deptComparator =
        (e1, e2) -> e1.department.compareTo(e2.department);

Collections.sort(employees, deptComparator);
```

Output

```text
Finance
HR
IT
Sales
```

---

# 3. Product

Fields

```java
class Product {
    int productId;
    String name;
    double price;
    double rating;
}
```

## Comparable (Default Sorting)

Sort by **Product ID**

```java
@Override
public int compareTo(Product other) {
    return Integer.compare(this.productId, other.productId);
}
```

```java
Collections.sort(products);
```

Output

```text
1
2
3
4
```

---

## Comparator (Custom Sorting)

Sort by **Price**

```java
Comparator<Product> priceComparator =
        (p1, p2) -> Double.compare(p1.price, p2.price);

Collections.sort(products, priceComparator);
```

Output

```text
299
599
899
1299
```

---

Sort by **Rating**

```java
Comparator<Product> ratingComparator =
        (p1, p2) -> Double.compare(p1.rating, p2.rating);

Collections.sort(products, ratingComparator);
```

Output

```text
3.8
4.2
4.5
4.9
```

---

# 4. Book

Fields

```java
class Book {
    int isbn;
    String title;
    int pages;
    double price;
}
```

## Comparable (Default Sorting)

Sort by **ISBN**

```java
@Override
public int compareTo(Book other) {
    return Integer.compare(this.isbn, other.isbn);
}
```

```java
Collections.sort(books);
```

Output

```text
1001
1002
1003
1004
```

---

## Comparator (Custom Sorting)

Sort by **Title**

```java
Comparator<Book> titleComparator =
        (b1, b2) -> b1.title.compareTo(b2.title);

Collections.sort(books, titleComparator);
```

Output

```text
Algorithms
Core Java
Python
Spring
```

---

Sort by **Price**

```java
Comparator<Book> priceComparator =
        (b1, b2) -> Double.compare(b1.price, b2.price);

Collections.sort(books, priceComparator);
```

Output

```text
399
499
599
799
```

---

# 5. Movie

Fields

```java
class Movie {
    int movieId;
    String title;
    double rating;
    int duration;
}
```

## Comparable (Default Sorting)

Sort by **Movie ID**

```java
@Override
public int compareTo(Movie other) {
    return Integer.compare(this.movieId, other.movieId);
}
```

```java
Collections.sort(movies);
```

Output

```text
1
2
3
4
```

---

## Comparator (Custom Sorting)

Sort by **Rating**

```java
Comparator<Movie> ratingComparator =
        (m1, m2) -> Double.compare(m1.rating, m2.rating);

Collections.sort(movies, ratingComparator);
```

Output

```text
3.9
4.2
4.6
4.8
```

---

Sort by **Duration**

```java
Comparator<Movie> durationComparator =
        (m1, m2) -> Integer.compare(m1.duration, m2.duration);

Collections.sort(movies, durationComparator);
```

Output

```text
120 mins
145 mins
160 mins
180 mins
```

---

# Summary

| Class | Comparable (Default Sorting) | Comparator (Custom Sorting Examples) |
|--------|------------------------------|--------------------------------------|
| Student | Roll Number | Marks, Name, Age |
| Employee | Employee ID | Salary, Department |
| Product | Product ID | Price, Rating |
| Book | ISBN | Title, Price |
| Movie | Movie ID | Rating, Duration |