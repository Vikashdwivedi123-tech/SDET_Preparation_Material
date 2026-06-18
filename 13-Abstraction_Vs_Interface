# 🚀 Java For SDET → Abstract Class vs Interface

This is one of the MOST FREQUENTLY ASKED Java OOPS interview topics.

Interviewers ask this in:

* Java Core interviews
* SDET interviews
* Selenium Automation interviews
* Framework Design discussions
* Product-based company interviews

Especially important for:

* OOPS concepts
* Framework architecture
* Design patterns
* Real-world automation frameworks

---

Topics Covered:

1. What is an Abstract Class
2. Features of Abstract Class
3. Advantages of Abstract Class
4. What is an Interface
5. Features of Interface
6. Advantages of Interface
7. Abstract Class vs Interface
8. Real-Time Framework Examples
9. When to Use Abstract Class
10. When to Use Interface
11. Common Mistakes
12. Common Interview Questions

---

# 🧠 1. What is an Abstract Class ⭐

## What is it

An abstract class is a class that cannot be instantiated and may contain both abstract and concrete methods.

---

## Key Components

* Abstract methods
* Concrete methods
* Instance variables
* Constructors

---

## How to Answer (Interview Style)

An abstract class provides partial abstraction and allows common functionality to be shared among subclasses.

---

## Practical Example

```java
abstract class Browser {

    public void launchBrowser() {
        System.out.println("Launching Browser");
    }

    abstract void openUrl();
}
```

---

## Common Mistakes

* Creating objects of abstract classes
* Assuming all methods must be abstract

---

## Expected Interview Questions

* What is an abstract class?
* Why can't abstract classes be instantiated?
* Can abstract classes have constructors?

---

# 🧠 2. Features of Abstract Class ⭐

## Features

* Can contain abstract methods
* Can contain concrete methods
* Can have constructors
* Supports inheritance
* Can have instance variables

---

## Practical Example

```java
abstract class Employee {

    String company = "ABC";

    abstract void work();

    void login() {
        System.out.println("Login Successful");
    }
}
```

---

## Expected Interview Questions

* Can abstract class have implemented methods?
* Can abstract class contain variables?
* Can abstract class have constructors?

---

# 🧠 3. Advantages of Abstract Class ⭐

## Advantages

* Code reusability
* Common implementation sharing
* Better maintainability
* Supports partial abstraction

---

## How to Answer (Interview Style)

Abstract classes are useful when multiple child classes share common functionality while still requiring custom implementations.

---

## Real-Time Example

```text
BasePage
→ Common methods

LoginPage
HomePage
ProfilePage
```

---

# 🧠 4. What is an Interface ⭐

## What is it

An interface defines a contract that implementing classes must follow.

---

## Key Components

* Method declarations
* Loose coupling
* Multiple inheritance
* Behavior definition

---

## How to Answer (Interview Style)

An interface defines what a class should do without specifying how it should do it.

---

## Practical Example

```java
interface Browser {

    void launch();

    void close();
}
```

---

## Common Mistakes

* Thinking interfaces cannot have default methods
* Using interfaces for code sharing

---

## Expected Interview Questions

* What is an interface?
* Why use interfaces?
* What is a contract in Java?

---

# 🧠 5. Features of Interface ⭐

## Features

* Supports multiple inheritance
* Achieves abstraction
* Defines behavior contracts
* Enables loose coupling
* Can have default and static methods

---

## Practical Example

```java
interface Payment {

    void pay();

    default void printReceipt() {
        System.out.println("Receipt Generated");
    }
}
```

---

## Expected Interview Questions

* Can interface have methods with implementation?
* Can interface have variables?
* What are default methods?

---

# 🧠 6. Advantages of Interface ⭐

## Advantages

* Loose coupling
* Better scalability
* Flexible architecture
* Multiple inheritance support

---

## How to Answer (Interview Style)

Interfaces make applications flexible by allowing multiple implementations without changing client code.

---

## Practical Example

```text
WebDriver Driver

ChromeDriver
FirefoxDriver
EdgeDriver
```

---

# 🧠 7. Abstract Class vs Interface ⭐⭐⭐

| Feature              | Abstract Class      | Interface                 |
| -------------------- | ------------------- | ------------------------- |
| Abstraction          | Partial             | Full (Contract Based)     |
| Methods              | Abstract + Concrete | Abstract, Default, Static |
| Constructor          | Yes                 | No                        |
| Instance Variables   | Yes                 | No                        |
| Multiple Inheritance | No                  | Yes                       |
| Access Modifiers     | Any                 | Public by default         |
| Keyword              | extends             | implements                |

---

## How to Answer (Interview Style)

An abstract class is used when classes share common state and behavior, whereas an interface is used to define a contract that multiple unrelated classes can implement.

---

## Example

```java
abstract class Animal {
    abstract void sound();
}

interface Flyable {
    void fly();
}
```

---

# 🧠 8. Real-Time Framework Examples ⭐

## Selenium WebDriver

```java
WebDriver driver = new ChromeDriver();
```

WebDriver is an Interface.

ChromeDriver implements WebDriver.

---

## Page Object Model

```java
BasePage
LoginPage
HomePage
```

BasePage is commonly designed as an Abstract Class.

---

## API Framework

```text
Common API methods
→ Abstract Class

Request Behavior
→ Interface
```

---

# 🧠 9. When to Use Abstract Class ⭐

Use Abstract Class when:

* Classes share common code
* Common variables are required
* Constructors are needed
* Partial abstraction is sufficient

---

## Example

```java
BasePage
```

Shared methods:

```java
click()
type()
waitForElement()
```

---

# 🧠 10. When to Use Interface ⭐

Use Interface when:

* Multiple implementations are expected
* Loose coupling is required
* Behavior contracts are needed
* Multiple inheritance is required

---

## Example

```java
WebDriver
SearchContext
JavascriptExecutor
```

---

# 🧠 11. Common Mistakes ⭐

* Saying interfaces provide 100% abstraction (not fully true after Java 8)
* Using abstract class when only behavior contract is needed
* Forgetting interfaces support default methods
* Confusing inheritance with implementation
* Not giving real-world examples

---

# 🧠 12. Common Interview Questions ⭐

* What is an abstract class?
* What is an interface?
* Difference between abstract class and interface?
* Can an abstract class have constructors?
* Can interfaces have implemented methods?
* Why is WebDriver an interface?
* Why is BasePage usually an abstract class?
* Can a class implement multiple interfaces?
* Can a class extend multiple abstract classes?

---

# 🎯 FINAL INTERVIEW GOLD

## MOST IMPORTANT TOPICS

1. Abstract Class ⭐⭐⭐
2. Interface ⭐⭐⭐
3. Abstract Class vs Interface ⭐⭐⭐
4. WebDriver Interface ⭐⭐⭐
5. BasePage Abstract Class ⭐⭐⭐
6. Real-Time Framework Examples ⭐⭐⭐

---

# 💡 INTERVIEW ONE-LINER

"Use an Abstract Class when you want to share common implementation among related classes. Use an Interface when you want to define a contract that multiple classes can implement."
