# Handling Alert Pop-ups in Selenium

## What is an Alert?
A native browser dialog (not part of the DOM) triggered by JavaScript — `alert()`, `confirm()`, `prompt()`. Selenium can't locate it with `findElement`; you must switch to it via `driver.switchTo().alert()`.

## Types of Alerts

| Type | Trigger | Buttons |
|---|---|---|
| Simple Alert | `alert("message")` | OK only |
| Confirmation Alert | `confirm("message")` | OK / Cancel |
| Prompt Alert | `prompt("message")` | Text input + OK / Cancel |

## Alert Interface Methods

```java
Alert alert = driver.switchTo().alert();

alert.accept();          // clicks OK
alert.dismiss();         // clicks Cancel (or closes alert)
alert.getText();         // returns the alert's message text
alert.sendKeys("text");  // types into a prompt alert's input field
```

## 1. Handling a Simple Alert
```java
driver.findElement(By.id("alertBtn")).click();

Alert alert = driver.switchTo().alert();
System.out.println(alert.getText());  // read message
alert.accept();                       // click OK
```

## 2. Handling a Confirmation Alert
```java
driver.findElement(By.id("confirmBtn")).click();

Alert alert = driver.switchTo().alert();
alert.dismiss();   // click Cancel — use alert.accept() for OK
```

## 3. Handling a Prompt Alert
```java
driver.findElement(By.id("promptBtn")).click();

Alert alert = driver.switchTo().alert();
alert.sendKeys("John Doe");  // enter text
alert.accept();              // submit
```

## 4. Waiting for an Alert (recommended — alerts can be slow to render)
```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
Alert alert = wait.until(ExpectedConditions.alertIsPresent());
alert.accept();
```

## 5. Checking if an Alert is Present (avoids exceptions)
```java
public boolean isAlertPresent(WebDriver driver) {
    try {
        driver.switchTo().alert();
        return true;
    } catch (NoAlertPresentException e) {
        return false;
    }
}
```

## Common Exceptions
- `NoAlertPresentException` — thrown when `switchTo().alert()` is called but no alert exists.
- `UnhandledAlertException` — thrown when trying to interact with the page while an alert is still open and unhandled.

## Common Mistakes (interview traps)
- Trying `driver.findElement()` on an alert — alerts are outside the DOM, this always fails.
- Forgetting to switch back: after `accept()`/`dismiss()`, the alert closes automatically — no need to switch back to default content (unlike frames).
- Not waiting for the alert to appear before switching — causes flaky `NoAlertPresentException` on slower pages.
