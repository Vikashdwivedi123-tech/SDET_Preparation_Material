# Selenium Locators

## What are Locators?

Locators are used to identify and locate web elements on a webpage so that Selenium can perform actions such as:

* Click
* Type
* Select
* Verify

Example:

```java
driver.findElement(By.id("username"));
```

Here, Selenium uses the locator to find the element.

---

# Types of Locators in Selenium

Selenium provides **8 Locators**:

1. id
2. name
3. className
4. tagName
5. linkText
6. partialLinkText
7. cssSelector
8. xpath

---

# 1. ID Locator

## Syntax

```java
driver.findElement(By.id("username"));
```

### HTML

```html
<input id="username">
```

### Advantages

* Fastest locator
* Unique in most cases
* Highly reliable

### Interview Tip

✅ Always prefer ID when available.

---

# 2. Name Locator

## Syntax

```java
driver.findElement(By.name("email"));
```

### HTML

```html
<input name="email">
```

### Advantages

* Easy to use
* Commonly available

### Limitation

Name may not always be unique.

---

# 3. Class Name Locator

## Syntax

```java
driver.findElement(By.className("login-btn"));
```

### HTML

```html
<button class="login-btn">
Login
</button>
```

### Advantages

* Easy to identify elements

### Limitation

Class names are often shared by multiple elements.

---

# 4. Tag Name Locator

## Syntax

```java
driver.findElement(By.tagName("input"));
```

### HTML

```html
<input type="text">
```

### Usage

Mostly used when finding multiple elements.

Example:

```java
List<WebElement> links =
driver.findElements(By.tagName("a"));
```

### Interview Tip

Rarely used for locating a single element.

---

# 5. Link Text Locator

## Syntax

```java
driver.findElement(
By.linkText("Forgot Password"));
```

### HTML

```html
<a href="/forgot">
Forgot Password
</a>
```

### Advantages

Easy for hyperlinks.

### Limitation

Text must match exactly.

---

# 6. Partial Link Text Locator

## Syntax

```java
driver.findElement(
By.partialLinkText("Forgot"));
```

### HTML

```html
<a href="/forgot">
Forgot Password
</a>
```

### Advantages

No need to provide complete text.

### Limitation

May match multiple links.

---

# 7. CSS Selector

## Syntax

### By ID

```java
driver.findElement(
By.cssSelector("#username"));
```

### By Class

```java
driver.findElement(
By.cssSelector(".login-btn"));
```

### By Attribute

```java
driver.findElement(
By.cssSelector("input[name='email']"));
```

### HTML

```html
<input id="username"
       name="email">
```

### Advantages

* Faster than XPath
* Flexible
* Recommended in modern frameworks

### Limitation

Cannot traverse from child to parent.

---

# 8. XPath

## Syntax

### Absolute XPath

```java
driver.findElement(
By.xpath("/html/body/div/input"));
```

### Relative XPath

```java
driver.findElement(
By.xpath("//input[@id='username']"));
```

### HTML

```html
<input id="username">
```

### Advantages

* Most powerful locator
* Handles dynamic elements
* Can navigate parent-child relationships

### Limitation

Slightly slower than CSS Selector.

---

# Absolute XPath vs Relative XPath

## Absolute XPath

```java
/html/body/div/input
```

### Disadvantages

* Very fragile
* Breaks easily when UI changes

---

## Relative XPath

```java
//input[@id='username']
```

### Advantages

* More stable
* Preferred in automation frameworks

---

# Locator Priority (Interview Perspective)

Preferred order:

```text
1. ID
2. Name
3. CSS Selector
4. XPath
5. Class Name
6. Link Text
7. Partial Link Text
8. Tag Name
```

---

# Frequently Asked Interview Questions

## Q1. What are locators in Selenium?

Locators are used to identify web elements on a webpage.

---

## Q2. How many locators are available in Selenium?

There are 8 locators:

* id
* name
* className
* tagName
* linkText
* partialLinkText
* cssSelector
* xpath

---

## Q3. Which locator is the fastest?

```text
ID
```

because it is generally unique and directly accessible.

---

## Q4. Which locator is the most powerful?

```text
XPath
```

because it can handle complex and dynamic elements.

---

## Q5. Which is preferred: CSS Selector or XPath?

Generally:

```text
CSS Selector
```

because it is faster and simpler.

However:

```text
XPath
```

is preferred when dealing with complex dynamic elements or parent-child traversal.

---

## Q6. Why is Absolute XPath not recommended?

Because even a small UI change can break the locator.

---

## Q7. Can CSS Selector move from child to parent?

No.

XPath can move from child to parent, but CSS Selector cannot.

---

# Interview Answer

**Selenium provides 8 locators: id, name, className, tagName, linkText, partialLinkText, cssSelector, and xpath. ID is the most preferred locator because it is usually unique and fast. CSS Selector and XPath are the most commonly used locators in automation frameworks, with XPath being more powerful for handling dynamic elements and complex DOM structures.**
