# driver.close() vs driver.quit()

## Introduction

Selenium provides two methods to close browser windows:

```java
driver.close();
driver.quit();
```

Although both are used to close browsers, they behave differently.

---

# driver.close()

## What is driver.close()?

`driver.close()` closes only the current browser window on which WebDriver is focused.

### Syntax

```java
driver.close();
```

### Example

Suppose Selenium opens:

```text
Parent Window
Child Window
```

Current focus is on the Child Window.

```java
driver.close();
```

### Result

```text
Parent Window  → Open
Child Window   → Closed
```

Only the current window is closed.

---

# driver.quit()

## What is driver.quit()?

`driver.quit()` closes all browser windows opened by Selenium and terminates the WebDriver session.

### Syntax

```java
driver.quit();
```

### Example

Suppose Selenium opens:

```text
Parent Window
Child Window
```

```java
driver.quit();
```

### Result

```text
Parent Window  → Closed
Child Window   → Closed
WebDriver Session → Destroyed
```

All browser windows are closed.

---

# Difference Between close() and quit()

| driver.close()                               | driver.quit()                           |
| -------------------------------------------- | --------------------------------------- |
| Closes only the current browser window.      | Closes all browser windows.             |
| Current session may still remain active.     | Entire WebDriver session is terminated. |
| Used when working with multiple windows.     | Used at the end of test execution.      |
| Other browser windows remain open.           | All browser windows are closed.         |
| Does not stop the driver process completely. | Stops the driver process completely.    |

---

# Code Example

## Using close()

```java
WebDriver driver = new ChromeDriver();

driver.get("https://www.google.com");

driver.close();
```

Result:

```text
Current Browser Window Closed
```

---

## Using quit()

```java
WebDriver driver = new ChromeDriver();

driver.get("https://www.google.com");

driver.quit();
```

Result:

```text
All Browser Windows Closed
WebDriver Session Destroyed
```

---

# Real-Time Usage

### Use close()

When:

* Multiple windows/tabs are open.
* You want to close only the current window.

Example:

```java
driver.switchTo().window(childWindow);

driver.close();
```

---

### Use quit()

When:

* Test execution is completed.
* Browser cleanup is required.

Example:

```java
@AfterMethod
public void tearDown() {
    driver.quit();
}
```

---

# Frequently Asked Interview Questions

## Q1. What is the difference between close() and quit()?

**Answer:**

`close()` closes only the current browser window, whereas `quit()` closes all browser windows and terminates the WebDriver session.

---

## Q2. Which method should be used at the end of automation execution?

**Answer:**

`driver.quit()` should be used because it releases all browser and driver resources.

---

## Q3. What happens if multiple windows are open and we call close()?

**Answer:**

Only the currently focused window is closed. Other windows remain open.

---

## Q4. What happens internally when quit() is executed?

**Answer:**

* All browser windows are closed.
* WebDriver session is destroyed.
* Browser driver process is terminated.

---

# Interview Answer

**driver.close() closes only the current browser window, while driver.quit() closes all browser windows and completely terminates the WebDriver session. In automation frameworks, driver.quit() is generally used in teardown methods to ensure proper cleanup of browser resources.**
