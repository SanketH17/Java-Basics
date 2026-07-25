# Comparable Example (Sort by Roll Number)

In this example, the `Student` class implements `Comparable`, so the **default (natural) sorting** is by **Roll Number**.

## Student.java

```java
class Student implements Comparable<Student> {

    int rollNo;
    String name;
    int marks;
    int age;

    Student(int rollNo, String name, int marks, int age) {
        this.rollNo = rollNo;
        this.name = name;
        this.marks = marks;
        this.age = age;
    }

    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.rollNo, other.rollNo);
    }

    @Override
    public String toString() {
        return rollNo + " " + name + " " + marks + " " + age;
    }
}
```

---

## Main.java

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class ComparableDemo {

    public static void main(String[] args) {

        List<Student> students = new ArrayList<>();

        students.add(new Student(103, "Neha", 90, 19));
        students.add(new Student(101, "Rahul", 95, 22));
        students.add(new Student(104, "Priya", 60, 21));
        students.add(new Student(102, "Amit", 75, 20));

        System.out.println("Before Sorting");
        students.forEach(System.out::println);

        Collections.sort(students);

        System.out.println("\nAfter Sorting (By Roll Number)");
        students.forEach(System.out::println);
    }
}
```

---

## Output

```text
Before Sorting

103 Neha 90 19
101 Rahul 95 22
104 Priya 60 21
102 Amit 75 20

After Sorting (By Roll Number)

101 Rahul 95 22
102 Amit 75 20
103 Neha 90 19
104 Priya 60 21
```

---

# Comparator Example (Sort by Marks and Name)

In this example, the `Student` class **does not implement Comparable**.

Instead, we create different `Comparator` objects whenever we need different sorting rules.

## Student.java

```java
class Student {

    int rollNo;
    String name;
    int marks;
    int age;

    Student(int rollNo, String name, int marks, int age) {
        this.rollNo = rollNo;
        this.name = name;
        this.marks = marks;
        this.age = age;
    }

    @Override
    public String toString() {
        return rollNo + " " + name + " " + marks + " " + age;
    }
}
```

---

## Main.java

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class ComparatorDemo {

    public static void main(String[] args) {

        List<Student> students = new ArrayList<>();

        students.add(new Student(103, "Neha", 90, 19));
        students.add(new Student(101, "Rahul", 95, 22));
        students.add(new Student(104, "Priya", 60, 21));
        students.add(new Student(102, "Amit", 75, 20));

        System.out.println("Original List");
        students.forEach(System.out::println);

        // Sort by Marks
        Comparator<Student> marksComparator = (s1, s2) ->
                Integer.compare(s1.marks, s2.marks);

        Collections.sort(students, marksComparator);

        System.out.println("\nSorted By Marks");
        students.forEach(System.out::println);

        // Sort by Name
        Comparator<Student> nameComparator = (s1, s2) ->
                s1.name.compareTo(s2.name);

        Collections.sort(students, nameComparator);

        System.out.println("\nSorted By Name");
        students.forEach(System.out::println);
    }
}
```

---

## Output

```text
Original List

103 Neha 90 19
101 Rahul 95 22
104 Priya 60 21
102 Amit 75 20

Sorted By Marks

104 Priya 60 21
102 Amit 75 20
103 Neha 90 19
101 Rahul 95 22

Sorted By Name

102 Amit 75 20
103 Neha 90 19
104 Priya 60 21
101 Rahul 95 22
```

---

# What Changed?

## Comparable

```text
Student Class
      │
      ▼
implements Comparable
      │
      ▼
compareTo()
      │
      ▼
Collections.sort(students)
      │
      ▼
Sorted by Roll Number
```

Only **one default sorting rule** is available.

---

## Comparator

```text
Student Class
      │
      ▼
No compareTo()
      │
      ▼
Create Comparator
      │
      ▼
Collections.sort(students, marksComparator)
      │
      ▼
Sorted by Marks

----------------------------

Collections.sort(students, nameComparator)
      │
      ▼
Sorted by Name
```

We can create **multiple Comparator objects**, each providing a different sorting rule.

---

# Key Difference

| Comparable | Comparator |
|------------|------------|
| Sort by Roll Number (default) | Sort by Marks |
| One natural sorting | Multiple custom sortings |
| `Collections.sort(students)` | `Collections.sort(students, comparator)` |
| Uses `compareTo()` | Uses `compare()` |