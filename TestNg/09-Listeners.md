# Listeners in TestNG

## What is a Listener?

A **Listener** in TestNG is a mechanism that listens to test execution events and performs custom actions automatically when those events occur.

Listeners are commonly used for:

* Capturing screenshots on test failure
* Logging test execution
* Generating custom reports
* Sending email notifications
* Updating test management tools (Jira, TestRail, etc.)

---

# Why Do We Need Listeners?

Without listeners, you would have to write the same code (e.g., taking screenshots or logging) inside every test.

A listener centralizes this logic, making the framework more maintainable and reusable.

---

# Common Listener Interfaces

| Listener                 | Purpose                                               |
| ------------------------ | ----------------------------------------------------- |
| `ITestListener`          | Listens to test execution events                      |
| `ISuiteListener`         | Listens to suite execution                            |
| `IInvokedMethodListener` | Executes before and after every method invocation     |
| `IExecutionListener`     | Executes before and after the entire TestNG execution |
| `IReporter`              | Generates custom reports                              |
| `IAnnotationTransformer` | Modifies TestNG annotations at runtime                |

---

# ITestListener Methods

| Method                                     | Triggered When               |
| ------------------------------------------ | ---------------------------- |
| `onStart()`                                | Before test execution starts |
| `onTestStart()`                            | Before each test method      |
| `onTestSuccess()`                          | Test passes                  |
| `onTestFailure()`                          | Test fails                   |
| `onTestSkipped()`                          | Test is skipped              |
| `onTestFailedButWithinSuccessPercentage()` | Test partially succeeds      |
| `onFinish()`                               | After all tests complete     |

---

# Example

## Listener Class

```java id="n9g3ep"
import org.testng.ITestListener;
import org.testng.ITestResult;

public class TestListener implements ITestListener {

    @Override
    public void onTestStart(ITestResult result) {
        System.out.println("Test Started : " + result.getName());
    }

    @Override
    public void onTestSuccess(ITestResult result) {
        System.out.println("Test Passed : " + result.getName());
    }

    @Override
    public void onTestFailure(ITestResult result) {
        System.out.println("Test Failed : " + result.getName());
    }
}
```

---

## Register Listener Using Annotation

```java id="cggf0x"
import org.testng.annotations.Listeners;

@Listeners(TestListener.class)
public class LoginTest {

    @Test
    public void login() {
        System.out.println("Executing Login Test");
    }
}
```

---

## Register Listener Using testng.xml

```xml id="vh4y5i"
<suite name="Suite">

    <listeners>
        <listener class-name="listeners.TestListener"/>
    </listeners>

    <test name="Tests">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>

</suite>
```

---

# Screenshot on Failure Example

```java id="v9sqf4"
@Override
public void onTestFailure(ITestResult result) {

    takeScreenshot(result.getName());

    System.out.println("Screenshot Captured");
}
```

This is one of the most common real-world uses of listeners in Selenium automation.

---

# Listener Execution Flow

```text id="wry6kb"
onStart()

    ↓

onTestStart()

    ↓

@Test Executes

    ↓

 ┌──────────────┐
 │              │
Success      Failure
 │              │
 ↓              ↓
onTestSuccess() onTestFailure()

        ↓

     onFinish()
```

---

# Advantages

* Eliminates duplicate code.
* Automatically performs actions during test execution.
* Improves framework maintainability.
* Integrates easily with reporting tools such as Extent Reports and Allure.
* Useful for logging, screenshots, retries, and notifications.

---

# Real-World Use Cases

* Capture screenshots on failure.
* Generate Extent Reports.
* Retry failed tests.
* Log execution details.
* Send email notifications after execution.
* Update Jira or TestRail automatically.

---

# Interview Questions

### Q1. What is a Listener?

A Listener listens to TestNG execution events and performs custom actions automatically.

---

### Q2. Which listener is most commonly used?

**`ITestListener`** because it provides callbacks for test start, success, failure, skipped, and finish events.

---

### Q3. How do you register a listener?

There are two ways:

1. Using `@Listeners` annotation.
2. Using the `<listeners>` tag in `testng.xml`.

---

### Q4. How do you capture screenshots on failure?

Override the `onTestFailure()` method in `ITestListener` and capture the screenshot using Selenium WebDriver.

---

# Interview One-Liner

> **A TestNG Listener is used to listen to test execution events and automatically perform actions such as logging, taking screenshots on failure, generating reports, retrying failed tests, or sending notifications without modifying the test cases.**
