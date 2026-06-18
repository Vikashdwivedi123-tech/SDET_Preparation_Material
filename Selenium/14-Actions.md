# Actions Class in Selenium

## What is Actions Class?

The Actions class in Selenium is used to perform advanced user interactions that cannot be handled using normal WebDriver methods.

Examples:

* Mouse Hover
* Right Click
* Double Click
* Drag and Drop
* Click and Hold
* Keyboard Actions

The Actions class belongs to:

```java
org.openqa.selenium.interactions.Actions
```

---

# Why Do We Need Actions Class?

Some web elements become visible only after a mouse hover or require complex user interactions.

Example:

```text
Move Mouse → Menu Appears
```

Normal Selenium commands cannot handle such scenarios effectively.

---

# Creating an Actions Object

### Syntax

```java
Actions actions = new Actions(driver);
```

### Example

```java
WebDriver driver = new ChromeDriver();

Actions actions = new Actions(driver);
```

---

# Common Methods of Actions Class

## 1. moveToElement() - Mouse Hover

Used to move the mouse pointer over an element.

### Syntax

```java
actions.moveToElement(element).perform();
```

### Example

```java
WebElement menu =
driver.findElement(By.id("menu"));

actions.moveToElement(menu).perform();
```

### Use Case

* Dropdown menus
* Hidden options appearing on hover

---

# 2. click()

Performs a mouse click action.

### Syntax

```java
actions.click(element).perform();
```

### Example

```java
actions.click(loginButton).perform();
```

---

# 3. doubleClick()

Performs a double-click action.

### Syntax

```java
actions.doubleClick(element).perform();
```

### Example

```java
actions.doubleClick(button).perform();
```

---

# 4. contextClick()

Performs a right-click action.

### Syntax

```java
actions.contextClick(element).perform();
```

### Example

```java
actions.contextClick(file).perform();
```

### Use Case

* Context menus
* File operations

---

# 5. dragAndDrop()

Used to drag an element from one location and drop it onto another.

### Syntax

```java
actions.dragAndDrop(source, target)
       .perform();
```

### Example

```java
actions.dragAndDrop(sourceElement,
                    targetElement)
       .perform();
```

### Use Case

* Kanban Boards
* Drag-and-Drop Applications

---

# 6. clickAndHold()

Clicks and holds the mouse button without releasing it.

### Syntax

```java
actions.clickAndHold(element)
       .perform();
```

### Example

```java
actions.clickAndHold(slider)
       .perform();
```

---

# 7. release()

Releases the held mouse button.

### Syntax

```java
actions.release().perform();
```

### Example

```java
actions.clickAndHold(element)
       .release()
       .perform();
```

---

# Keyboard Actions

## sendKeys()

Used to type text using Actions class.

### Syntax

```java
actions.sendKeys("Hello")
       .perform();
```

---

## keyDown() and keyUp()

Used for keyboard combinations.

### Example: CTRL + A

```java
actions.keyDown(Keys.CONTROL)
       .sendKeys("a")
       .keyUp(Keys.CONTROL)
       .perform();
```

### Example: CTRL + C

```java
actions.keyDown(Keys.CONTROL)
       .sendKeys("c")
       .keyUp(Keys.CONTROL)
       .perform();
```

---

# perform() vs build().perform()

## perform()

Executes a single action immediately.

```java
actions.click(element).perform();
```

---

## build().perform()

Builds a chain of multiple actions and executes them together.

```java
actions.moveToElement(menu)
       .click(subMenu)
       .build()
       .perform();
```

### Interview Tip

In Selenium 4, most actions work fine with only:

```java
.perform()
```

and `build()` is rarely needed.

---

# Real-Time Example

Mouse Hover on Menu and Click Submenu

```java
Actions actions = new Actions(driver);

actions.moveToElement(menu)
       .click(subMenu)
       .perform();
```

---

What is the difference between Action and Actions in Selenium?

Actions Class
---
Actions is a class provided by Selenium.

It is used to build complex user interactions such as:

Mouse Hover
Right Click
Double Click
Drag and Drop
Keyboard Actions

Example
Actions actions = new Actions(driver);

actions.moveToElement(element)
       .click()
       .perform();

Action Interface
---
Action is an interface in Selenium.

It represents a single user interaction that can be executed.

The Actions class internally creates Action objects.

Action action =
new Actions(driver)
        .moveToElement(element)
        .build();

action.perform();

---

# Frequently Asked Interview Questions

## Q1. What is the Actions class?

Actions class is used to perform advanced mouse and keyboard operations in Selenium.

---

## Q2. Which package contains the Actions class?

```java
org.openqa.selenium.interactions.Actions
```

---

## Q3. How do you perform Mouse Hover?

```java
actions.moveToElement(element)
       .perform();
```

---

## Q4. How do you perform Right Click?

```java
actions.contextClick(element)
       .perform();
```

---

## Q5. How do you perform Double Click?

```java
actions.doubleClick(element)
       .perform();
```

---

## Q6. How do you perform Drag and Drop?

```java
actions.dragAndDrop(source, target)
       .perform();
```

---

## Q7. What is the difference between perform() and build().perform()?

* `perform()` executes an action immediately.
* `build().perform()` combines multiple actions and executes them together.

---

# Interview Answer

**The Actions class in Selenium is used to perform advanced user interactions such as mouse hover, right click, double click, drag and drop, and keyboard actions. It is available in the `org.openqa.selenium.interactions.Actions` package. We create an Actions object using `new Actions(driver)` and execute actions using the `perform()` method.**
