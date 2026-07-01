# How Do You Capture a Screenshot in Selenium?

## What is Screenshot Capture?

Selenium provides the **`TakesScreenshot`** interface to capture screenshots of the browser during test execution.

Screenshots are commonly captured:

* When a test fails
* For debugging
* For reporting (Extent Reports, Allure)
* To maintain execution evidence

---

# Steps to Capture a Screenshot

1. Cast the `WebDriver` to `TakesScreenshot`.
2. Capture the screenshot using `getScreenshotAs()`.
3. Save the screenshot to the desired location.

---

# Example

```java id="d2v5sa"
import org.openqa.selenium.*;
import org.openqa.selenium.io.FileHandler;
import java.io.File;
import java.io.IOException;

public class ScreenshotUtil {

    public static void captureScreenshot(WebDriver driver, String fileName)
            throws IOException {

        TakesScreenshot ts = (TakesScreenshot) driver;

        File source = ts.getScreenshotAs(OutputType.FILE);

        File destination = new File("./Screenshots/" + fileName + ".png");

        FileHandler.copy(source, destination);
    }
}
```

---

# Calling the Method

```java id="hjl4i7"
@Test
public void loginTest() throws IOException {

    driver.get("https://example.com");

    ScreenshotUtil.captureScreenshot(driver, "LoginPage");
}
```

The screenshot will be saved as:

```text id="sk6x3d"
Screenshots/
    LoginPage.png
```

---

# Capture Screenshot on Test Failure (Using `ITestListener`)

```java id="0zjlwm"
@Override
public void onTestFailure(ITestResult result) {

    ScreenshotUtil.captureScreenshot(driver, result.getName());

    System.out.println("Screenshot Captured");
}
```

This is the most common implementation in Selenium automation frameworks.

---

# Full Page Screenshot

For browsers that support it (or by using libraries like AShot), you can capture the **entire webpage**, including the portion outside the visible viewport.

```java id="uh8qtk"
Screenshot screenshot = new AShot().takeScreenshot(driver);
```

---

# Best Practices

* Capture screenshots only on **test failure** to save storage.
* Include the test name and timestamp in the file name.
* Store screenshots in a dedicated folder.
* Attach screenshots to reports such as Extent Reports or Allure.
* Delete or archive old screenshots periodically.

---

# Common Naming Convention

```text id="pk0tbm"
LoginTest_20260701_103015.png
```

Using the test name and timestamp helps avoid overwriting existing screenshots.

---

# Interview Questions

### Q1. Which interface is used to capture screenshots?

**`TakesScreenshot`**

---

### Q2. Which method captures the screenshot?

```java id="g4yxp6"
getScreenshotAs(OutputType.FILE)
```

---

### Q3. When do you usually capture screenshots?

* On test failure
* For debugging
* During report generation
* As execution evidence

---

### Q4. How do you capture screenshots automatically when a test fails?

Implement the `ITestListener` interface and capture the screenshot inside the `onTestFailure()` method.

---

# Interview One-Liner

> **Selenium uses the `TakesScreenshot` interface to capture browser screenshots. The screenshot is obtained using `getScreenshotAs(OutputType.FILE)` and is commonly captured in the `onTestFailure()` method of a TestNG `ITestListener` for reporting and debugging.**
