# Core Java — Study Notes

A structured collection of beginner-friendly Core Java notes covering fundamental concepts from the ground up. Each topic is documented with explanations, examples, and tables to support learning and quick revision.

---

## Java_Basics

Foundational Java topics organized sequentially, from how the JVM works to advanced beginner concepts like wrapper classes.

- [JavaBasics_01.md](./Java_Basics/JavaBasics_01.md) — **Compiler vs Interpreter | JVM | Bytecode**
  Covers the Java compilation and execution pipeline: writing `.java` source code, compiling with `javac`, generating `.class` bytecode, and running it on the JVM.

- [JavaBasics02.md](./Java_Basics/JavaBasics02.md) — **Platform Independence | Classes & Objects**
  Explains platform dependence vs independence, the Write Once Run Anywhere (WORA) principle, introduction to classes and objects, and the Java execution flow.

- [JavaBasics03_java-data-types-and-variables-notes.md](./Java_Basics/JavaBasics03_java-data-types-and-variables-notes.md) — **Data Types & Variables**
  Covers all 8 primitive data types and their memory sizes, non-primitive (reference) types, variable declaration and initialization, and static vs non-static variables.

- [JavaBasics04_java-methods-notes.md](./Java_Basics/JavaBasics04_java-methods-notes.md) — **Methods**
  Covers method syntax and components, access modifiers (`public`, `private`, `protected`, default), types of methods, parameter passing, return types, and an introduction to method overloading.

- [JavaBasics05_java_strings.md](./Java_Basics/JavaBasics05_java_strings.md) — **Strings**
  Covers String creation, String Pool memory management, immutability, common String methods, concatenation, `StringBuilder` vs `StringBuffer`, formatting, conversion, and regular expressions.

- [JavaBasics06_java-packages-and-naming-conventions-notes.md](./Java_Basics/JavaBasics06_java-packages-and-naming-conventions-notes.md) — **Packages & Naming Conventions**
  Covers Java packages as directory-based code organization, `package` and `import` statements, predefined vs user-defined packages, the `java.lang` default package, and Java naming conventions.

- [JavaBasics07_java-operators-notes.md](./Java_Basics/JavaBasics07_java-operators-notes.md) — **Operators**
  Covers all Java operator types: arithmetic, unary, assignment, relational/comparison, logical/conditional, bitwise, shift, ternary (`? :`), and the `instanceof` operator.

- [JavaBasics08_control-flow-and-switch-statement.md](./Java_Basics/JavaBasics08_control-flow-and-switch-statement.md) — **Control Flow & Switch Statement**
  Covers sequential vs conditional execution, `if`, `if-else`, `if-else-if` chains, and the `switch` statement including enhanced switch expressions.

- [JavaBasics09_java-looping-and-branching-statements-notes.md](./Java_Basics/JavaBasics09_java-looping-and-branching-statements-notes.md) — **Looping & Branching Statements**
  Covers `for`, `while`, and `do-while` loops, and branching/jumping statements: `break`, `continue`, and `return`.

- [JavaBasics10_user-dynamic-input-java-notes.md](./Java_Basics/JavaBasics10_user-dynamic-input-java-notes.md) — **User Dynamic Input**
  Covers reading runtime input from the user using the `Scanner` class, why dynamic input is preferred over hardcoding values, and common `nextInt()`, `nextLine()`, etc. methods.

- [JavaBasics11_arrays-in-java-notes.md](./Java_Basics/JavaBasics11_arrays-in-java-notes.md) — **Arrays**
  Covers arrays as fixed-size reference types, declaration and initialization, single-dimensional and multi-dimensional arrays, array traversal, and common array operations.

- [JavaBasics12_command-line-arguments-java.md](./Java_Basics/JavaBasics12_command-line-arguments-java.md) — **Command Line Arguments**
  Covers passing values to a Java program at runtime via `String[] args` in the `main` method, accessing and using those arguments, and practical use cases.

- [JavaBasics13_wrapper-classes-java.md](./Java_Basics/JavaBasics13_wrapper-classes-java.md) — **Wrapper Classes**
  Covers the 8 wrapper classes (`Integer`, `Double`, `Character`, etc.), why they are needed in Collections, autoboxing and unboxing, null support, and utility methods for conversion and comparison.
