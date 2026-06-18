# findElement() vs findElements()

## What is findElement()?

`findElement()` is used to locate a single web element on a webpage.

### Syntax

```java
WebElement element =
driver.findElement(By.id("username"));
```

### Return Type

```java
WebElement
```

### Behavior

* Returns the first matching element.
* Throws `NoSuchElementException` if the element is not found.

### Example

HTML:

```html
<input id="username">
```

Selenium:

```java
WebElement username =
driver.findElement(By.id("username"));

username.sendKeys("Vikash");
```

---

# What is findElements()?

`findElements()` is used to locate multiple web elements on a webpage.

### Syntax

```java
List<WebElement> elements =
driver.findElements(By.tagName("a"));
```

### Return Type

```java
List<WebElement>
```

### Behavior

* Returns all matching elements.
* Returns an empty list if no element is found.
* Does not throw `NoSuchElementException`.

### Example

HTML:

```html
<a>Home</a>
<a>About</a>
<a>Contact</a>
```

Selenium:

```java
List<WebElement> links =
driver.findElements(By.tagName("a"));

System.out.println(links.size());
```

Output:

```text
3
```

---

# Difference Between findElement() and findElements()

| findElement()                                       | findElements()                            |
| --------------------------------------------------- | ----------------------------------------- |
| Finds a single element.                             | Finds multiple elements.                  |
| Returns WebElement.                                 | Returns List<WebElement>.                 |
| Returns first matching element.                     | Returns all matching elements.            |
| Throws NoSuchElementException if element not found. | Returns empty list if element not found.  |
| Used when only one element is expected.             | Used when multiple elements are expected. |

---

# What Happens When Element is Not Found?

## findElement()

```java
driver.findElement(By.id("abc"));
```

Output:

```text
NoSuchElementException
```

---

## findElements()

```java
List<WebElement> elements =
driver.findElements(By.id("abc"));
```

Output:

```text
[]
```

Empty List Returned

---

# Real-Time Example

Suppose a page contains:

```html
<a>Home</a>
<a>About</a>
<a>Contact</a>
<a>Services</a>
```

### Using findElement()

```java
WebElement link =
driver.findElement(By.tagName("a"));
```

Result:

```text
Only "Home" element is returned.
```

---

### Using findElements()

```java
List<WebElement> links =
driver.findElements(By.tagName("a"));
```

Result:

```text
All 4 links are returned.
```

---

# When Should We Use findElement()?

Use when:

* Only one element is expected.
* Working with Login button.
* Username textbox.
* Password textbox.

Example:

```java
driver.findElement(By.id("login"));
```

---

# When Should We Use findElements()?

Use when:

* Multiple elements are expected.
* Handling tables.
* Lists.
* Dropdown values.
* Links.

Example:

```java
driver.findElements(By.tagName("a"));
```

---

# Frequently Asked Interview Questions

## Q1. What is the return type of findElement()?

```java
WebElement
```

---

## Q2. What is the return type of findElements()?

```java
List<WebElement>
```

---

## Q3. What happens if findElement() does not find an element?

It throws:

```text
NoSuchElementException
```

---

## Q4. What happens if findElements() does not find any element?

It returns:

```text
Empty List
```

---

## Q5. Which method is safer when checking element existence?

```java
findElements()
```

Because it returns an empty list instead of throwing an exception.

Example:

```java
if(driver.findElements(By.id("login")).size() > 0)
{
    System.out.println("Element Present");
}
```

---

# Interview Answer

**findElement() is used to locate a single element and returns a WebElement. If the element is not found, it throws NoSuchElementException. findElements() is used to locate multiple elements and returns a List<WebElement>. If no matching elements are found, it returns an empty list instead of throwing an exception.**
