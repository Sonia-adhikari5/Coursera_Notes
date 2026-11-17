# Java Programming Fundamentals

| | |
|---|---|
| **Journal** | Journal 1 (Weeks 1–4) |
| **Evidence for** | Section 1, row 1 – Java programming fundamentals |
| **Module** | Fundamental Module 1 – Fundamentals of Programming in Java |
| **Covers** | Program structure, data types, operators, control flow, arrays, methods, strings, debugging |

---

## 1. Structure of a Java program

Every Java program is built from classes. Execution starts at the `main` method.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

| Part | Meaning |
|---|---|
| `public class HelloWorld` | Declares a class. The file must be named `HelloWorld.java`. |
| `public static void main(String[] args)` | Entry point. The JVM calls it to start the program. |
| `System.out.println(...)` | Prints a line to the console. |

**How Java runs:** source code (`.java`) is compiled by `javac` into bytecode (`.class`), and the Java Virtual Machine (JVM) executes that bytecode. This is why the same compiled program can run on different operating systems.

---

## 2. Variables and data types

Java is **statically typed**: the type of every variable must be declared and is checked at compile time.

| Type | Size | Example | Notes |
|---|---|---|---|
| `byte` | 8 bit | `byte b = 10;` | −128 to 127 |
| `short` | 16 bit | `short s = 500;` | |
| `int` | 32 bit | `int age = 20;` | Default whole-number type |
| `long` | 64 bit | `long pop = 8000000000L;` | Needs the `L` suffix |
| `float` | 32 bit | `float f = 3.5f;` | Needs the `f` suffix |
| `double` | 64 bit | `double pi = 3.14159;` | Default decimal type |
| `char` | 16 bit | `char grade = 'A';` | Single quotes |
| `boolean` | logical | `boolean pass = true;` | `true` or `false` |

`String` is not a primitive. It is a class, so it is written with a capital `S` and double quotes: `String name = "Sonam";`.

**Type casting**

```java
int a = 7;
double widened = a;          // implicit (widening): int -> double, safe
double price = 9.99;
int truncated = (int) price; // explicit (narrowing): 9, the decimal part is lost
```

**Naming conventions:** `camelCase` for variables and methods, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants (`final int MAX_SIZE = 100;`).

---

## 3. Operators

| Category | Operators | Example |
|---|---|---|
| Arithmetic | `+ - * / %` | `17 % 5` gives `2` |
| Comparison | `== != < > <= >=` | `age >= 18` |
| Logical | `&&`, `\|\|`, `!` | `age > 18 && hasId` |
| Assignment | `= += -= *= /=` | `total += 5;` |
| Increment | `++ --` | `count++` |

**Common trap:** integer division. `7 / 2` is `3`, not `3.5`. Use `7 / 2.0` to get `3.5`.

---

## 4. Control structures

### Decisions

```java
int marks = 72;
if (marks >= 80) {
    System.out.println("Distinction");
} else if (marks >= 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}

int day = 3;
switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    case 3: System.out.println("Wednesday"); break;
    default: System.out.println("Other day");
}
```

### Loops

```java
for (int i = 1; i <= 5; i++) {          // known number of repetitions
    System.out.print(i + " ");
}

int n = 3;
while (n > 0) {                          // repeat while condition is true
    System.out.println(n--);
}

int x = 0;
do {                                     // body always runs at least once
    x++;
} while (x < 3);

int[] nums = {4, 8, 15};
for (int value : nums) {                 // enhanced for loop
    System.out.println(value);
}
```

`break` leaves a loop early. `continue` skips to the next iteration.

---

## 5. Arrays

An array stores a fixed number of values of the same type. Indexes start at `0`.

```java
int[] scores = new int[5];        // five zeros
int[] marks = {70, 85, 60};       // initialised directly
marks[1] = 90;                    // update an element
System.out.println(marks.length); // 3
```

Accessing `marks[3]` throws `ArrayIndexOutOfBoundsException` because the last valid index is `length - 1`.

---

## 6. Methods

A method groups reusable logic. It has a return type, a name, parameters and a body.

```java
static int square(int n) {
    return n * n;
}

static double average(int[] values) {
    int sum = 0;
    for (int v : values) sum += v;
    return (double) sum / values.length;
}

// Method overloading: same name, different parameter lists
static int add(int a, int b)          { return a + b; }
static double add(double a, double b) { return a + b; }
```

Java passes arguments **by value**. For objects and arrays, the value that is copied is the reference, so changes made to an array's elements inside a method are visible to the caller.

---

## 7. Strings and input

```java
String s = "Software Engineering";
s.length();            // 20
s.charAt(0);           // 'S'
s.substring(0, 8);     // "Software"
s.toUpperCase();       // "SOFTWARE ENGINEERING"
s.equals("software");  // false  (compare content with equals, not ==)
s.contains("Eng");     // true
```

Reading keyboard input:

```java
import java.util.Scanner;

Scanner in = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = in.nextLine();
```

---

## 8. Worked example – marks analyser

This program combines arrays, loops, methods and decisions.

```java
public class MarksAnalyser {

    static double average(int[] marks) {
        int sum = 0;
        for (int m : marks) sum += m;
        return (double) sum / marks.length;
    }

    static int highest(int[] marks) {
        int max = marks[0];
        for (int m : marks) {
            if (m > max) max = m;
        }
        return max;
    }

    static String grade(double avg) {
        if (avg >= 80) return "Distinction";
        else if (avg >= 50) return "Pass";
        else return "Fail";
    }

    public static void main(String[] args) {
        int[] marks = {72, 85, 64, 91, 58};
        double avg = average(marks);
        System.out.println("Average: " + avg);
        System.out.println("Highest: " + highest(marks));
        System.out.println("Result: " + grade(avg));
    }
}
```

**Expected output**

```
Average: 74.0
Highest: 91
Result: Pass
```

---

## 9. Debugging notes

| Problem | Typical cause | Fix |
|---|---|---|
| `cannot find symbol` | Typo, missing import, variable out of scope | Check spelling and where the variable was declared |
| `incompatible types: possible lossy conversion` | Assigning `double` to `int` without a cast | Add an explicit cast or change the type |
| `ArrayIndexOutOfBoundsException` | Loop runs to `<= length` | Use `< length` |
| `NullPointerException` | Calling a method on an object that is `null` | Initialise the object, or check for `null` first |
| Infinite loop | Loop variable never changes | Make sure the condition can become false |
| `==` on Strings gives the wrong result | `==` compares references | Use `.equals()` |

**Debugging routine:** read the first error line, note the line number, reproduce with a smaller input, print intermediate values, then fix one thing at a time.

---

## 10. Self-check questions

1. What is the difference between `int` and `Integer`?
2. Why does `7 / 2` print `3`?
3. When would you use a `do-while` loop instead of a `while` loop?
4. What does "passed by value" mean when an array is given to a method?
5. Why should `equals()` be used to compare strings?

## References

Oracle. (n.d.). *The Java™ tutorials*. https://docs.oracle.com/javase/tutorial/