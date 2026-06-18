# getText() vs getAttribute() in Selenium

## Introduction

Both `getText()` and `getAttribute()` are used to retrieve information from web elements.

However, they serve different purposes:

* `getText()` → Retrieves visible text displayed on the webpage.
* `getAttribute()` → Retrieves the value of an HTML attribute.

This is one of the most frequently asked Selenium interview questions.

---

# getText()

## What is getText()?

`getText()` is used to retrieve the visible text present between the opening and closing tags of an element.

### Syntax

```java
String text = element.getText();
```

### Example

#### HTML

```html
<button>Login</button>
```

#### Selenium

```java
WebElement button =
driver.findElement(By.tagName("button"));

System.out.println(button.getText());
```

### Output

```text
Login
```

### Use Cases

* Verify labels
* Verify button text
* Verify messages
* Verify headings

Example:

```java
String heading =
driver.findElement(By.tagName("h1"))
      .getText();
```

---

# getAttribute()

## What is getAttribute()?

`getAttribute()` is used to retrieve the value of an HTML attribute.

### Syntax

```java
String value =
element.getAttribute("attributeName");
```

### Example

#### HTML

```html
<input
type="text"
id="username"
value="admin">
```

#### Selenium

```java
WebElement username =
driver.findElement(By.id("username"));

System.out.println(
username.getAttribute("value"));
```

### Output

```text
admin
```

---

# Why Can't We Use getText() Here?

HTML:

```html
<input
type="text"
value="admin">
```

Selenium:

```java
System.out.println(
element.getText());
```

Output:

```text
```

(Empty String)

Reason:

The text is stored inside the `value` attribute, not between opening and closing tags.

Therefore:

```java
element.getAttribute("value");
```

must be used.

---

# Real-Time Example

### Button Text

HTML:

```html
<button>Submit</button>
```

```java
element.getText();
```

Output:

```text
Submit
```

---

### Input Box Value

HTML:

```html
<input value="Vikash">
```

```java
element.getAttribute("value");
```

Output:

```text
Vikash
```

---

# Difference Between getText() and getAttribute()

| getText()                                    | getAttribute()                                               |
| -------------------------------------------- | ------------------------------------------------------------ |
| Retrieves visible text.                      | Retrieves attribute value.                                   |
| Reads text between opening and closing tags. | Reads HTML attributes.                                       |
| Returns displayed text.                      | Returns attribute value.                                     |
| Mostly used for labels, buttons, headings.   | Mostly used for input fields, links, IDs, placeholders, etc. |
| Does not work for input field values.        | Works for input field values.                                |

---

# Example Comparison

### HTML

```html
<input
id="username"
value="admin"
placeholder="Enter Username">
```

### Selenium

```java
WebElement element =
driver.findElement(By.id("username"));

System.out.println(
element.getText());

System.out.println(
element.getAttribute("value"));

System.out.println(
element.getAttribute("placeholder"));
```

### Output

```text
(blank)

admin

Enter Username
```

---

# Common Attributes Used in Selenium

```java
element.getAttribute("id");

element.getAttribute("name");

element.getAttribute("value");

element.getAttribute("class");

element.getAttribute("placeholder");

element.getAttribute("href");
```

---

# Frequently Asked Interview Questions

## Q1. What is the difference between getText() and getAttribute()?

**Answer:**

`getText()` retrieves visible text from a web element, whereas `getAttribute()` retrieves the value of an HTML attribute.

---

## Q2. Why does getText() return blank for input fields?

Because input field values are stored inside the `value` attribute and not between opening and closing tags.

---

## Q3. How do you get the value entered in a textbox?

```java
element.getAttribute("value");
```

---

## Q4. Which method is used to verify a button label?

```java
element.getText();
```

---

## Q5. Which method is used to retrieve placeholder text?

```java
element.getAttribute("placeholder");
```

---

# Interview Answer

**getText() is used to retrieve the visible text displayed on a webpage, such as button labels, headings, and messages. getAttribute() is used to retrieve the value of an HTML attribute such as value, id, name, class, placeholder, or href. For input fields, getAttribute("value") is used because getText() returns an empty string.**
