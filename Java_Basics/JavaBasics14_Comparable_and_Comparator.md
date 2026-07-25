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