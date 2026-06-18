# Running Selenium in Headless Mode

## What is Headless Mode?

**Headless Mode** allows Selenium to execute browser automation without opening a visible browser window.

The browser runs in the background, performing all actions normally while consuming fewer system resources.

---

## Why Use Headless Mode?

Headless execution is useful for:

* Faster test execution
* CI/CD pipelines (Jenkins, GitHub Actions, GitLab CI)
* Server environments without a graphical interface
* Web scraping tasks
* Running automated tests in containers (Docker)

---

## Advantages of Headless Mode

### Faster Execution

Since no browser UI is rendered, tests often execute faster.

### Lower Resource Consumption

Headless browsers use less memory and CPU compared to GUI mode.

### CI/CD Friendly

Perfect for automated pipelines where displaying a browser window is not possible.

### Background Execution

Tests can run on remote servers without requiring a desktop environment.

---

## Running Chrome in Headless Mode

### Selenium 4 (Recommended)

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;

public class HeadlessChromeExample {

    public static void main(String[] args) {

        ChromeOptions options = new ChromeOptions();

        options.addArguments("--headless=new");

        WebDriver driver = new ChromeDriver(options);

        driver.get("https://example.com");

        System.out.println(driver.getTitle());

        driver.quit();
    }
}
```

---

## Running Firefox in Headless Mode

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.firefox.FirefoxOptions;

public class HeadlessFirefoxExample {

    public static void main(String[] args) {

        FirefoxOptions options = new FirefoxOptions();

        options.setHeadless(true);

        WebDriver driver = new FirefoxDriver(options);

        driver.get("https://example.com");

        System.out.println(driver.getTitle());

        driver.quit();
    }
}
```

---

## Setting Browser Window Size

In headless mode, browsers may use a default viewport size that differs from normal execution.

Set the window size explicitly:

```java
ChromeOptions options = new ChromeOptions();

options.addArguments("--headless=new");
options.addArguments("--window-size=1920,1080");

WebDriver driver = new ChromeDriver(options);
```

---

## Taking Screenshots in Headless Mode

Screenshots work the same way as in normal mode.

```java
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import java.io.File;

File screenshot =
        ((TakesScreenshot) driver)
                .getScreenshotAs(OutputType.FILE);
```

This is useful for debugging failed tests.

---

## Running Tests in CI/CD Pipelines

Example Chrome configuration for CI environments:

```java
ChromeOptions options = new ChromeOptions();

options.addArguments("--headless=new");
options.addArguments("--disable-gpu");
options.addArguments("--no-sandbox");
options.addArguments("--disable-dev-shm-usage");

WebDriver driver = new ChromeDriver(options);
```

### Common Arguments

| Argument                  | Purpose                                 |
| ------------------------- | --------------------------------------- |
| `--headless=new`          | Enables modern headless mode            |
| `--disable-gpu`           | Disables GPU acceleration               |
| `--no-sandbox`            | Useful in containerized environments    |
| `--disable-dev-shm-usage` | Prevents shared memory issues in Docker |

---

## Complete Example

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;

public class HeadlessModeDemo {

    public static void main(String[] args) {

        ChromeOptions options = new ChromeOptions();

        options.addArguments("--headless=new");
        options.addArguments("--window-size=1920,1080");

        WebDriver driver = new ChromeDriver(options);

        driver.get("https://www.google.com");

        System.out.println("Title: " + driver.getTitle());
        System.out.println("URL: " + driver.getCurrentUrl());

        driver.quit();
    }
}
```

---

## Challenges in Headless Mode

### Different Element Behavior

Some websites render elements differently in headless mode.

### Viewport Issues

Elements may not appear if the browser window size is too small.

### Timing Problems

Dynamic content may load differently, requiring explicit waits.

```java
WebDriverWait wait =
        new WebDriverWait(driver, Duration.ofSeconds(10));
```

### Bot Detection

Some websites can detect headless browsers and restrict access.

---

## Best Practices

1. Use `--headless=new` with modern Chrome versions.
2. Set a fixed browser window size.
3. Use explicit waits instead of `Thread.sleep()`.
4. Capture screenshots for debugging failures.
5. Validate tests in both headed and headless modes.
6. Use headless execution primarily in CI/CD environments.

---

## Headless vs Headed Mode

| Feature        | Headless    | Headed     |
| -------------- | ----------- | ---------- |
| Browser UI     | ❌ No        | ✅ Yes      |
| Speed          | ✅ Faster    | ❌ Slower   |
| Resource Usage | ✅ Lower     | ❌ Higher   |
| Debugging      | ❌ Harder    | ✅ Easier   |
| CI/CD Support  | ✅ Excellent | ⚠️ Limited |

---

## Summary

Headless Mode allows Selenium to run browser automation without displaying a graphical browser window. It improves execution speed, reduces resource usage, and is ideal for CI/CD pipelines, cloud environments, and automated testing workflows.
