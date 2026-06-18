# Handling iFrames in Selenium

## What is an iFrame?

An **iFrame (Inline Frame)** is an HTML element that embeds another webpage inside the current webpage.

```html
<iframe id="loginFrame" src="login.html"></iframe>
```

Elements inside an iFrame are treated as part of a separate document. Selenium cannot directly interact with elements inside an iFrame unless the driver switches to it first.

---

## Why Switch to an iFrame?

If you try to locate an element inside an iFrame without switching to it, Selenium throws a:

```text
NoSuchElementException
```

This happens because Selenium only searches within the currently active document.

---

## Switching to an iFrame

### 1. Switch by Index

Use the index when multiple iFrames exist and no unique identifier is available.

```java
driver.switchTo().frame(0);
```

* Index starts from `0`.
* Refers to the order of iFrames on the page.

---

### 2. Switch by Name or ID

```java
driver.switchTo().frame("loginFrame");
```

or

```java
driver.switchTo().frame("frameId");
```

---

### 3. Switch Using WebElement

This is the most reliable approach.

```java
WebElement iframe = driver.findElement(By.id("loginFrame"));
driver.switchTo().frame(iframe);
```

---

## Interacting with Elements Inside an iFrame

```java
driver.switchTo().frame("loginFrame");

driver.findElement(By.id("username")).sendKeys("admin");
driver.findElement(By.id("password")).sendKeys("password");
driver.findElement(By.id("loginBtn")).click();
```

---

## Switching Back to Main Page

After working inside an iFrame, switch back to the main document.

### Return to Parent Frame

```java
driver.switchTo().parentFrame();
```

Moves one level up.

### Return to Default Content

```java
driver.switchTo().defaultContent();
```

Returns directly to the main webpage.

---

## Handling Nested iFrames

When an iFrame contains another iFrame:

```java
driver.switchTo().frame("parentFrame");
driver.switchTo().frame("childFrame");
```

To return:

```java
driver.switchTo().parentFrame();
```

or

```java
driver.switchTo().defaultContent();
```

---

## Complete Example

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class IFrameExample {
    public static void main(String[] args) {

        WebDriver driver = new ChromeDriver();

        driver.get("https://example.com");

        WebElement frame =
                driver.findElement(By.id("loginFrame"));

        driver.switchTo().frame(frame);

        driver.findElement(By.id("username"))
                .sendKeys("admin");

        driver.findElement(By.id("password"))
                .sendKeys("password");

        driver.findElement(By.id("loginBtn"))
                .click();

        driver.switchTo().defaultContent();

        driver.quit();
    }
}
```

---

## Best Practices

1. Prefer switching using `WebElement` rather than index.
2. Use explicit waits before switching to dynamic iFrames.
3. Always switch back using `defaultContent()` after completing actions.
4. Avoid hardcoded frame indexes because page structure can change.
5. Verify whether the target element is inside an iFrame before locating it.

---

## Common Selenium iFrame Methods

| Method                         | Description                |
| ------------------------------ | -------------------------- |
| `switchTo().frame(index)`      | Switch by frame index      |
| `switchTo().frame(nameOrId)`   | Switch by frame name or ID |
| `switchTo().frame(WebElement)` | Switch using WebElement    |
| `switchTo().parentFrame()`     | Return to parent frame     |
| `switchTo().defaultContent()`  | Return to main page        |

### Summary

Selenium cannot interact with elements inside an iFrame until the WebDriver switches context to that frame. After completing operations, switch back to the main document using `parentFrame()` or `defaultContent()`.
