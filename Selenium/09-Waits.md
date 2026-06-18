# Waits in Selenium

## Why Do We Need Waits?

Modern web applications load elements dynamically.

Sometimes Selenium tries to interact with an element before it is available on the page.

This may result in exceptions such as:

* NoSuchElementException
* ElementNotInteractableException
* ElementClickInterceptedException

To handle these situations, Selenium provides **Waits**.

---

# Types of Waits in Selenium

1. Implicit Wait
2. Explicit Wait
3. Fluent Wait

---

# 1. Implicit Wait

## What is Implicit Wait?

Implicit Wait tells Selenium to wait for a specified amount of time while searching for an element.

If the element is found before the timeout, Selenium proceeds immediately.

### Syntax

```java
driver.manage()
      .timeouts()
      .implicitlyWait(Duration.ofSeconds(10));
```

### Example

```java
driver.manage()
      .timeouts()
      .implicitlyWait(Duration.ofSeconds(10));

driver.findElement(By.id("username"))
      .sendKeys("admin");
```

### How It Works

```text
Element Found in 2 sec
      ↓
Execution Continues
```

```text
Element Not Found in 10 sec
      ↓
NoSuchElementException
```

### Advantages

* Easy to implement
* Applied globally to all elements

### Limitations

* Cannot wait for specific conditions
* Slows down execution if overused

---

# 2. Explicit Wait

## What is Explicit Wait?

Explicit Wait waits for a specific condition to occur before proceeding.

It is the most commonly used wait in Selenium frameworks.

### Syntax

```java
WebDriverWait wait =
new WebDriverWait(driver,
Duration.ofSeconds(10));
```

### Example

```java
WebDriverWait wait =
new WebDriverWait(driver,
Duration.ofSeconds(10));

wait.until(
ExpectedConditions.visibilityOfElementLocated(
By.id("username")));
```

### Common Conditions

#### Element Visible

```java
wait.until(
ExpectedConditions.visibilityOfElementLocated(
By.id("username")));
```

#### Element Clickable

```java
wait.until(
ExpectedConditions.elementToBeClickable(
By.id("login")));
```

#### Alert Present

```java
wait.until(
ExpectedConditions.alertIsPresent());
```

### Advantages

* Waits only when required
* Better performance
* Supports multiple conditions

### Limitation

* Must be applied individually

---

# 3. Fluent Wait

## What is Fluent Wait?

Fluent Wait is an advanced version of Explicit Wait.

It allows:

* Custom timeout
* Custom polling interval
* Ignoring specific exceptions

### Syntax

```java
Wait<WebDriver> wait =
new FluentWait<>(driver)
.withTimeout(Duration.ofSeconds(10))
.pollingEvery(Duration.ofSeconds(2))
.ignoring(NoSuchElementException.class);
```

### Example

```java
Wait<WebDriver> wait =
new FluentWait<>(driver)
.withTimeout(Duration.ofSeconds(10))
.pollingEvery(Duration.ofSeconds(2))
.ignoring(NoSuchElementException.class);

wait.until(
driver ->
driver.findElement(By.id("username")));
```

### How It Works

```text
Timeout = 10 sec

Check after 2 sec
Check after 4 sec
Check after 6 sec
Check after 8 sec
Check after 10 sec
```

### Advantages

* More control over waiting
* Supports polling intervals
* Can ignore exceptions

### Limitation

* More complex than Explicit Wait

---

# Difference Between Implicit, Explicit and Fluent Wait

| Feature            | Implicit Wait | Explicit Wait    | Fluent Wait      |
| ------------------ | ------------- | ---------------- | ---------------- |
| Scope              | Global        | Specific Element | Specific Element |
| Condition Based    | No            | Yes              | Yes              |
| Polling Interval   | Default       | Default          | Customizable     |
| Exception Handling | No            | Limited          | Yes              |
| Flexibility        | Low           | Medium           | High             |
| Most Commonly Used | No            | Yes              | Sometimes        |

---

# Explicit Wait vs Fluent Wait

| Explicit Wait                 | Fluent Wait                 |
| ----------------------------- | --------------------------- |
| Waits for a condition         | Waits for a condition       |
| Uses default polling interval | Custom polling interval     |
| Easier to implement           | More configurable           |
| Most commonly used            | Used for advanced scenarios |

### Example

#### Explicit Wait

```java
WebDriverWait wait =
new WebDriverWait(driver,
Duration.ofSeconds(10));
```

#### Fluent Wait

```java
Wait<WebDriver> wait =
new FluentWait<>(driver)
.withTimeout(Duration.ofSeconds(10))
.pollingEvery(Duration.ofSeconds(2));
```

---

# Which Wait Should We Use?

### Preferred Order

```text
1. Explicit Wait
2. Fluent Wait
3. Implicit Wait
```

### Interview Tip

✅ In real automation frameworks, Explicit Wait is used most frequently.

✅ Fluent Wait is used when custom polling or exception handling is required.

❌ Avoid mixing Implicit Wait and Explicit Wait together.

---

# Frequently Asked Interview Questions

## Q1. Why do we use waits in Selenium?

To synchronize Selenium with the application and avoid failures caused by dynamically loaded elements.

---

## Q2. What are the types of waits in Selenium?

* Implicit Wait
* Explicit Wait
* Fluent Wait

---

## Q3. Which wait is most commonly used?

```text
Explicit Wait
```

because it waits for specific conditions.

---

## Q4. What is the difference between Explicit Wait and Fluent Wait?

Fluent Wait provides additional features such as custom polling intervals and exception handling.

---

## Q5. Can we use Implicit Wait and Explicit Wait together?

Technically yes, but it is not recommended because it can lead to unpredictable wait times.

---

## Q6. Which wait is more flexible?

```text
Fluent Wait
```

because it allows custom polling and exception handling.

---

# Interview Answer

**Selenium provides three types of waits: Implicit Wait, Explicit Wait, and Fluent Wait. Implicit Wait is applied globally and waits while searching for elements. Explicit Wait waits for a specific condition such as visibility or clickability of an element. Fluent Wait is an advanced version of Explicit Wait that allows custom polling intervals and exception handling. In most automation frameworks, Explicit Wait is the preferred synchronization mechanism.**
