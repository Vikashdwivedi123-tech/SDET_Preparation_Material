# JavascriptExecutor Interface in Selenium

## What is it?
An interface that lets Selenium execute JavaScript code directly in the browser through the WebDriver. Used when native Selenium commands can't perform an action (hidden elements, overlays, scrolling, shadow DOM, etc.).

## Setup
```java
JavascriptExecutor js = (JavascriptExecutor) driver;
```
`driver` must be cast to `JavascriptExecutor` since `WebDriver` itself doesn't expose JS execution methods.

## Core Methods

| Method | Purpose |
|---|---|
| `executeScript(script, args)` | Runs JS synchronously, returns result immediately |
| `executeAsyncScript(script, args)` | Runs JS asynchronously, waits for a callback before returning |

## 1. Click an Element (bypass overlay/visibility issues)
```java
WebElement element = driver.findElement(By.id("submitBtn"));
js.executeScript("arguments[0].click();", element);
```

## 2. Scroll the Page
```java
js.executeScript("window.scrollBy(0,500)");                 // scroll down by pixels
js.executeScript("window.scrollTo(0, document.body.scrollHeight)"); // scroll to bottom
js.executeScript("arguments[0].scrollIntoView(true);", element);    // scroll element into view
```

## 3. Set Value Into a Field (bypass sendKeys issues)
```java
js.executeScript("arguments[0].value='test@example.com';", element);
```

## 4. Get Page Title / URL via JS
```java
String title = (String) js.executeScript("return document.title;");
String url = (String) js.executeScript("return document.URL;");
```

## 5. Highlight an Element (debugging aid)
```java
js.executeScript("arguments[0].style.border='3px solid red';", element);
```

## 6. Get Inner Text (when getText() fails on hidden elements)
```java
String text = (String) js.executeScript("return arguments[0].innerText;", element);
```

## 7. Generate an Alert / Confirm via JS
```java
js.executeScript("alert('Hello from JS');");
```

## 8. Refresh the Page
```java
js.executeScript("history.go(0)");
```

## 9. Remove an Attribute (e.g., disable "readonly")
```java
js.executeScript("arguments[0].removeAttribute('readonly');", element);
```

## 10. Wait for Page Load (check document.readyState)
```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(webDriver ->
    js.executeScript("return document.readyState").equals("complete"));
```

## 11. executeAsyncScript Example (waiting for an async JS callback)
```java
driver.manage().timeouts().scriptTimeout(Duration.ofSeconds(10));

Object result = js.executeAsyncScript(
    "var callback = arguments[arguments.length - 1];" +
    "setTimeout(function(){ callback('done'); }, 2000);"
);
```

## Why/When to Use JavascriptExecutor
- Clicking elements blocked by overlays or off-screen.
- Scrolling to elements before interacting.
- Filling fields where `sendKeys()` triggers unwanted validation/JS events.
- Reading values not exposed properly via standard WebDriver methods.
- Generating synthetic browser events for edge-case testing.

## Common Mistakes (interview traps)
- Overusing JS clicks/sendKeys as a workaround for flaky locators instead of fixing the locator or wait strategy — masks real bugs.
- Forgetting `arguments[0]` refers to the first WebElement passed in, `arguments[1]` the second, etc.
- Not casting `result` correctly — `executeScript` returns `Object`, so you must cast to `String`, `Boolean`, `Long`, `List`, or `Map` depending on what JS returns.
- Using JS to "fake" interactions in tests meant to validate real user behavior (e.g., JS-click bypasses CSS pointer-events checks a real user would hit).
