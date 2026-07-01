# Retry Failed Test Cases in TestNG

## What is Retry Analyzer?

A **Retry Analyzer** in TestNG is used to automatically re-execute a failed test case a specified number of times before marking it as failed.

It is useful when test failures occur due to temporary issues such as:

* Network latency
* Browser synchronization issues
* Slow page loading
* Environment instability

---

# How Does It Work?

TestNG provides the `IRetryAnalyzer` interface.

You need to:

1. Create a class that implements `IRetryAnalyzer`.
2. Override the `retry()` method.
3. Attach the Retry Analyzer to the test using `retryAnalyzer`.

---

# Step 1: Create Retry Analyzer Class

```java id="o1v4mj"
import org.testng.IRetryAnalyzer;
import org.testng.ITestResult;

public class RetryAnalyzer implements IRetryAnalyzer {

    private int count = 0;
    private static final int MAX_RETRY = 2;

    @Override
    public boolean retry(ITestResult result) {

        if (count < MAX_RETRY) {
            count++;
            return true;
        }

        return false;
    }
}
```

> Here, the failed test will be retried **2 additional times** before being marked as failed.

---

# Step 2: Use Retry Analyzer

```java id="2ed75r"
import org.testng.Assert;
import org.testng.annotations.Test;

public class LoginTest {

    @Test(retryAnalyzer = RetryAnalyzer.class)
    public void loginTest() {

        System.out.println("Executing Login Test");

        Assert.fail();
    }
}
```

---

# Execution Flow

```text id="0lkgzs"
Attempt 1
     │
     ▼
 Test Fails
     │
     ▼
Retry?

Yes
 │
 ▼
Attempt 2
 │
 ▼
Still Fails
 │
 ▼
Attempt 3
 │
 ▼
Pass → Test Passed

OR

Fail → Test Failed
```

---

# Retry Using Listener (Recommended)

Instead of adding `retryAnalyzer` to every test, you can use **`IAnnotationTransformer`** to apply it automatically to all test cases.

```java id="khjlwm"
public class RetryListener implements IAnnotationTransformer {

    @Override
    public void transform(ITestAnnotation annotation,
                          Class testClass,
                          Constructor testConstructor,
                          Method testMethod) {

        annotation.setRetryAnalyzer(RetryAnalyzer.class);
    }
}
```

Register the listener in `testng.xml`:

```xml id="6dqm7y"
<listeners>
    <listener class-name="listeners.RetryListener"/>
</listeners>
```

This avoids repeating `retryAnalyzer = RetryAnalyzer.class` in every test.

---

# Best Practices

* Retry only for **intermittent (flaky)** failures.
* Do **not** use retries to hide genuine application defects.
* Keep the retry count low (typically 1–3 retries).
* Log each retry attempt for easier debugging.

---

# Advantages

* Reduces failures caused by temporary issues.
* Improves CI/CD pipeline stability.
* Minimizes manual reruns of failed tests.
* Helps identify flaky tests.

---

# Interview Questions

### Q1. Which interface is used to retry failed tests?

**`IRetryAnalyzer`**

---

### Q2. Which method controls the retry?

The `retry(ITestResult result)` method.

---

### Q3. How do you retry all failed tests without adding `retryAnalyzer` to every test?

Use **`IAnnotationTransformer`** to assign the `RetryAnalyzer` automatically.

---

### Q4. Should every failed test be retried?

**No.** Only transient or flaky failures should be retried. Functional defects should fail immediately so they can be investigated.

---

# Interview One-Liner

> **TestNG provides the `IRetryAnalyzer` interface to automatically rerun failed test cases. The retry logic is implemented in the `retry()` method, and for framework-level implementation, it can be applied globally using `IAnnotationTransformer`.**
