# 🚀 Java For SDET → Static Keyword in Java

The **static keyword** is one of the MOST ASKED Java interview topics.

Interviewers ask this in:

* Java Core interviews
* SDET interviews
* Selenium Automation interviews
* Framework Design discussions
* Product-based company interviews

Especially important for:

* Memory management
* Utility classes
* Framework architecture
* Java fundamentals

---

Topics Covered:

1. What is Static Keyword
2. Why Static is Used
3. Static Variable
4. Static Method
5. Static Block
6. Static Nested Class
7. Static Import
8. Static vs Non-Static
9. Real-Time Framework Usage
10. Common Mistakes
11. Common Interview Questions

---

# 🧠 1. What is Static Keyword ⭐

## What is it

The static keyword belongs to the class rather than an object.

Only one copy of a static member exists regardless of how many objects are created.

---

## How to Answer (Interview Style)

Static is a keyword in Java used to create class-level variables, methods, blocks, and nested classes that can be accessed without creating an object.

---

## Key Point

```text
Static Member
     ↓
Belongs to Class
     ↓
Not to Objects
```

---

## Example

```java
class Employee {

    static String company = "Google";
}
```

---

## Expected Interview Questions

* What is static keyword?
* Why is static used?
* Does static belong to class or object?

---

# 🧠 2. Why Static is Used ⭐

## Benefits

* Memory optimization
* Shared data
* Utility methods
* Faster access
* Common framework configuration

---

## Example

Without static:

```text
100 Objects
↓
100 Copies of Variable
```

With static:

```text
100 Objects
↓
1 Shared Copy
```

---

## Interview Answer

Static reduces memory consumption because a single copy is shared across all objects.

---

# 🧠 3. Static Variable ⭐⭐⭐

## What is it

A variable declared using static keyword.

Shared among all objects of a class.

---

## Example

```java
class Employee {

    static String company = "OpenAI";

    String name;
}
```

---

## Usage

```java
Employee e1 = new Employee();
Employee e2 = new Employee();

System.out.println(Employee.company);
```

---

## Output

```text
OpenAI
```

---

## Memory Representation

```text
Class Area

company = OpenAI

Object1
name = Vikash

Object2
name = Rahul
```

---

## Real-Time Framework Example

```java
public class FrameworkConfig {

    public static String ENV = "QA";
}
```

---

## Common Mistakes

❌ Accessing static variables through objects

```java
e1.company;
```

✅ Preferred

```java
Employee.company;
```

---

## Interview Questions

* What is a static variable?
* Where are static variables stored?
* Why are static variables memory efficient?

---

# 🧠 4. Static Method ⭐⭐⭐

## What is it

A method that belongs to the class rather than an object.

Can be called directly using class name.

---

## Example

```java
class MathUtil {

    static int add(int a, int b) {
        return a + b;
    }
}
```

---

## Usage

```java
MathUtil.add(10, 20);
```

---

## Rules

Static methods:

✅ Can access static members

❌ Cannot access non-static members directly

❌ Cannot use this keyword

---

## Example

```java
class Test {

    int id = 10;

    static void display() {

        // Compile Error
        // System.out.println(id);
    }
}
```

---

## Why?

Because static methods belong to class and non-static variables belong to objects.

---

## Real-Time Framework Example

```java
public static void takeScreenshot() {

}
```

```java
public static void waitForElement() {

}
```

---

## Interview Questions

* What is static method?
* Can static methods access non-static variables?
* Why can't static methods use this keyword?

---

# 🧠 5. Static Block ⭐⭐⭐

## What is it

A block that executes once when the class is loaded into memory.

---

## Syntax

```java
class Test {

    static {

        System.out.println("Static Block");
    }
}
```

---

## Output

```text
Static Block
```

Runs before object creation.

---

## Execution Order

```text
Static Block
↓
Main Method
↓
Constructor
```

---

## Real-Time Framework Example

Load configuration files.

```java
static {

    System.out.println("Loading Configurations");
}
```

---

## Interview Questions

* What is static block?
* When does static block execute?
* Can multiple static blocks exist?

---

# 🧠 6. Static Nested Class ⭐⭐

## What is it

A class declared static inside another class.

---

## Example

```java
class Outer {

    static class Inner {

        void display() {

        }
    }
}
```

---

## Usage

```java
Outer.Inner obj = new Outer.Inner();
```

---

## Benefits

* Better grouping
* Memory optimization
* Cleaner design

---

## Interview Questions

* What is static nested class?
* Difference between inner class and static nested class?

---

# 🧠 7. Static Import ⭐⭐

## What is it

Allows direct access to static members without class name.

---

## Example

```java
import static java.lang.Math.*;

public class Test {

    public static void main(String[] args) {

        System.out.println(sqrt(16));
    }
}
```

---

## Output

```text
4.0
```

---

## Benefits

Cleaner code.

---

## Common Mistakes

Overusing static imports.

---

## Interview Questions

* What is static import?
* When should static import be used?

---

# 🧠 8. Static vs Non-Static ⭐⭐⭐

| Feature           | Static     | Non-Static |
| ----------------- | ---------- | ---------- |
| Belongs To        | Class      | Object     |
| Memory Allocation | Once       | Per Object |
| Access            | Class Name | Object     |
| Can Use this      | ❌ No       | ✅ Yes      |
| Shared Data       | ✅ Yes      | ❌ No       |

---

## Example

```java
class Employee {

    static String company;

    String name;
}
```

---

## Interview Answer

Static members belong to the class and are shared across all objects, whereas non-static members belong to individual objects.

---

# 🧠 9. Real-Time Framework Usage ⭐⭐⭐

## Selenium Framework

### Utility Classes

```java
public static void takeScreenshot() {

}
```

---

### Wait Utilities

```java
public static void waitForVisibility() {

}
```

---

### Framework Constants

```java
public static final String URL =
"https://test.com";
```

---

### Driver Factory

```java
private static WebDriver driver;
```

---

## Why Static is Used

```text
Reusable Methods
Shared Configurations
Framework Utilities
Constants
```

---

# 🧠 10. Common Mistakes ⭐

❌ Accessing static members through objects

❌ Using static everywhere

❌ Accessing non-static variables inside static methods

❌ Using this inside static methods

❌ Making framework state global unnecessarily

---

## Wrong

```java
driver.getTitle();
```

Inside static method without driver being static.

---

## Correct

```java
static WebDriver driver;
```

---

# 🧠 11. Common Interview Questions ⭐⭐⭐

* What is static keyword?
* Why static is used?
* What is static variable?
* What is static method?
* What is static block?
* Can static methods access non-static members?
* Why can't static methods use this keyword?
* What is static import?
* What is static nested class?
* Difference between static and non-static?
* Where are static variables stored?
* Can constructors be static?

---

# 🎯 FINAL INTERVIEW GOLD

## MOST IMPORTANT TOPICS

1. Static Variable ⭐⭐⭐
2. Static Method ⭐⭐⭐
3. Static Block ⭐⭐⭐
4. Static vs Non-Static ⭐⭐⭐
5. Framework Utility Methods ⭐⭐⭐
6. Memory Optimization ⭐⭐⭐

---

# 🚀 SDET FRAMEWORK EXAMPLES

## Screenshot Utility

```java
public class ScreenshotUtil {

    public static void captureScreenshot() {

    }
}
```

---

## Wait Utility

```java
public class WaitUtil {

    public static void waitForElement() {

    }
}
```

---

## Constants Class

```java
public class Constants {

    public static final String URL =
            "https://test.com";
}
```

---

# 💡 INTERVIEW ONE-LINER

"Static members belong to the class rather than objects. They are shared across all instances and can be accessed without creating an object, making them ideal for utility methods, constants, and shared framework resources."
