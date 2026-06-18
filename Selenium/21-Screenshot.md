# Capturing Screenshots in Selenium

## What is a Screenshot in Selenium?

A screenshot is an image of the current browser screen captured during test execution.

Screenshots are commonly used to:

* Debug failed test cases
* Capture application state
* Store evidence of successful test execution
* Generate test reports

Selenium provides the **TakeScreenshot** interface to capture screenshots.

---

## Why Use the TakesScreenshot Interface?

The `WebDriver` itself does not directly provide screenshot functionality.

To capture screenshots, Selenium uses the `TakesScreenshot` interface, which contains the `getScreenshotAs()` method.

```java
public interface TakesScreenshot
```

---

## getScreenshotAs() Method

The `getScreenshotAs()` method captures the current browser screen and returns it in the specified format.

### Syntax

```java
getScreenshotAs(OutputType.FILE);
```

### Common Output Types

| Output Type         | Description                         |
| ------------------- | ----------------------------------- |
| `OutputType.FILE`   | Returns screenshot as a file        |
| `OutputType.BYTES`  | Returns screenshot as byte array    |
| `OutputType.BASE64` | Returns screenshot as Base64 string |

Most automation frameworks use `OutputType.FILE`.

---

## Steps to Capture a Screenshot

### Step 1: Open Browser

```java
WebDriver driver = new ChromeDriver();
```

### Step 2: Navigate to a Website

```java
driver.get("https://example.com");
```

### Step 3: Type Cast Driver to TakesScreenshot

```java
TakesScreenshot ts = (TakesScreenshot) driver;
```

### Step 4: Capture Screenshot

```java
File sourceFile = ts.getScreenshotAs(OutputType.FILE);
```

### Step 5: Save Screenshot

```java
File destinationFile =
        new File("screenshots/homepage.png");
```

### Step 6: Copy Screenshot to Desired Location

```java
Files.copy(
        sourceFile.toPath(),
        destinationFile.toPath()
);
```

---

## Complete Example

```java
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;

import java.io.File;
import java.nio.file.Files;

public class ScreenshotDemo {

    public static void main(String[] args) throws Exception {

        WebDriver driver = new ChromeDriver();

        driver.get("https://www.google.com");

        TakesScreenshot ts =
                (TakesScreenshot) driver;

        File sourceFile =
                ts.getScreenshotAs(OutputType.FILE);

        File destinationFile =
                new File("google_homepage.png");

        Files.copy(
                sourceFile.toPath(),
                destinationFile.toPath()
        );

        System.out.println("Screenshot captured successfully");

        driver.quit();
    }
}
```

---

## Capturing Screenshot in One Line

```java
File screenshot =
        ((TakesScreenshot) driver)
                .getScreenshotAs(OutputType.FILE);
```

This combines type casting and screenshot capture into a single statement.

---

## Taking Screenshot When Test Fails

A common practice is to capture screenshots only when a test case fails.

```java
try {

    driver.findElement(By.id("invalidElement"));

} catch (Exception e) {

    File screenshot =
            ((TakesScreenshot) driver)
                    .getScreenshotAs(OutputType.FILE);

    System.out.println("Failure screenshot captured");
}
```

This helps identify the exact state of the application during failure.

---

## Capturing Screenshot of a Specific WebElement

Selenium 4 allows screenshots of individual elements.

```java
WebElement logo =
        driver.findElement(By.id("logo"));

File screenshot =
        logo.getScreenshotAs(OutputType.FILE);
```

Instead of capturing the entire page, only the selected element is saved.

---

## Best Practices

1. Capture screenshots for failed test cases.
2. Store screenshots in a dedicated folder such as `screenshots/`.
3. Use meaningful file names.
4. Include timestamps to avoid overwriting files.
5. Attach screenshots to test reports for easier debugging.

---

## Common Methods

| Method                               | Purpose                                   |
| ------------------------------------ | ----------------------------------------- |
| `getScreenshotAs(OutputType.FILE)`   | Returns screenshot as file                |
| `getScreenshotAs(OutputType.BYTES)`  | Returns screenshot as byte array          |
| `getScreenshotAs(OutputType.BASE64)` | Returns screenshot as Base64 string       |
| `WebElement.getScreenshotAs()`       | Captures screenshot of a specific element |

---

## Summary

Selenium uses the `TakesScreenshot` interface to capture screenshots. The `getScreenshotAs()` method takes a screenshot of the current browser screen and returns it in different formats such as File, Bytes, or Base64. Screenshots are widely used for debugging, reporting, and analyzing test failures.
