# Selenium WebDriver - Interview Notes

## What is Selenium WebDriver?

Selenium WebDriver is an interface that allows us to automate web browsers.

It provides methods to perform actions such as:

* Click
* Type
* Navigate
* Handle Alerts
* Handle Windows
* Handle Frames

WebDriver directly communicates with browser-specific drivers such as:

* ChromeDriver
* FirefoxDriver
* EdgeDriver

which then communicate with the actual browser.

---

# Selenium WebDriver Architecture

```text
Automation Script
        ↓
WebDriver Interface
        ↓
Browser Driver
(ChromeDriver)
        ↓
Chrome Browser
```

---

# Why Do We Write?

```java
WebDriver driver = new ChromeDriver();
```

This is one of the most commonly asked Selenium interview questions.

---

## Explanation

### Left Side

```java
WebDriver driver
```

WebDriver is an interface.

It provides a reference variable.

---

### Right Side

```java
new ChromeDriver()
```

ChromeDriver is a class that implements the WebDriver interface.

An object of ChromeDriver is created.

---

### Why This Approach?

```java
WebDriver driver = new ChromeDriver();
```

follows the principle:

```text
Program to Interface
Not Implementation
```

This provides:

* Flexibility
* Loose Coupling
* Runtime Polymorphism

---

# Why Not?

```java
WebDriver driver = new WebDriver();
```

Because:

```java
WebDriver
```

is an interface.

Interfaces cannot be instantiated.

❌ Invalid

```java
WebDriver driver = new WebDriver();
```

Compiler Error:

```text
Cannot instantiate the type WebDriver
```

---

# Why Not?

```java
ChromeDriver driver = new ChromeDriver();
```

This is valid.

```java
ChromeDriver driver = new ChromeDriver();
```

But it is not preferred.

---

## Reason

Suppose tomorrow you want to run tests on Firefox.

Current Code:

```java
ChromeDriver driver =
new ChromeDriver();
```

Must be changed to:

```java
FirefoxDriver driver =
new FirefoxDriver();
```

Multiple changes required.

---

Using WebDriver:

```java
WebDriver driver =
new ChromeDriver();
```

Later:

```java
WebDriver driver =
new FirefoxDriver();
```

Only implementation changes.

Reference remains the same.

This is called:

```text
Runtime Polymorphism
```

---

# What Happens Internally?

```java
WebDriver driver =
new ChromeDriver();
```

Step 1:

Create ChromeDriver object.

```java
new ChromeDriver();
```

Step 2:

Store its reference in WebDriver type variable.

```java
WebDriver driver
```

Step 3:

WebDriver methods become available.

```java
driver.get();
driver.findElement();
driver.close();
driver.quit();
```

---

# Is WebDriver a Class or Interface?

Answer:

```text
WebDriver is an Interface.
```

---

# Is ChromeDriver a Class or Interface?

Answer:

```text
ChromeDriver is a Class.
```

---

# Relationship Between WebDriver and ChromeDriver

```java
public class ChromeDriver
implements WebDriver
```

ChromeDriver implements WebDriver.

---

# Why Is WebDriver Called an Interface?

Because it only contains method declarations.

Example:

```java
get()
close()
quit()
findElement()
```

Actual implementation is provided by:

```java
ChromeDriver
FirefoxDriver
EdgeDriver
```

---

# Frequently Asked Interview Questions

## Q1. What is Selenium WebDriver?

Selenium WebDriver is an interface used to automate web browsers.

---

## Q2. Why do we write?

```java
WebDriver driver =
new ChromeDriver();
```

Because WebDriver is an interface and ChromeDriver is its implementation class. This achieves runtime polymorphism and loose coupling.

---

## Q3. Why can't we write?

```java
WebDriver driver =
new WebDriver();
```

Because WebDriver is an interface and interfaces cannot be instantiated.

---

## Q4. Is this valid?

```java
ChromeDriver driver =
new ChromeDriver();
```

Yes.

But it reduces flexibility and is not preferred in framework design.

---

## Q5. What OOPs concept is used in

```java
WebDriver driver =
new ChromeDriver();
```

Runtime Polymorphism.

---

## Q6. Which browsers are supported by WebDriver?

* ChromeDriver → Chrome
* FirefoxDriver → Firefox
* EdgeDriver → Edge
* SafariDriver → Safari

---

## Q7. What are the advantages of using WebDriver reference?

* Loose Coupling
* Runtime Polymorphism
* Easy Browser Switching
* Better Framework Design

---

# Interview Answer

**WebDriver is an interface in Selenium that defines browser automation methods. ChromeDriver, FirefoxDriver, and EdgeDriver are classes that implement this interface. We write `WebDriver driver = new ChromeDriver();` to achieve runtime polymorphism and loose coupling. We cannot write `new WebDriver()` because WebDriver is an interface and interfaces cannot be instantiated.**
