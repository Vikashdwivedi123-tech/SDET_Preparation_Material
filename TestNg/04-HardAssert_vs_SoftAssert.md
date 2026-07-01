# Hard Assert vs Soft Assert in TestNG

| Feature              | Hard Assert                 | Soft Assert                                       |
| -------------------- | --------------------------- | ------------------------------------------------- |
| Execution on Failure | Stops execution immediately | Continues execution even after failure            |
| Test Result          | Test fails instantly        | Test fails only after `assertAll()` is called     |
| Assertion Class      | `Assert`                    | `SoftAssert`                                      |
| Need `assertAll()`   | ❌ No                        | ✅ Yes                                             |
| Best Use Case        | Critical validations        | Multiple independent validations in the same test |

## Hard Assert Example

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class HardAssertExample {

    @Test
    public void testLogin() {

        System.out.println("Step 1");

        Assert.assertEquals("Google", "Facebook");

        System.out.println("Step 2"); // Not executed
    }
}
```

**Output:**

```text
Step 1
Assertion Failed
```

> Since the assertion fails, the test stops immediately and **Step 2** is not executed.

---

## Soft Assert Example

```java
import org.testng.asserts.SoftAssert;
import org.testng.annotations.Test;

public class SoftAssertExample {

    @Test
    public void testLogin() {

        SoftAssert softAssert = new SoftAssert();

        System.out.println("Step 1");

        softAssert.assertEquals("Google", "Facebook");

        System.out.println("Step 2");

        softAssert.assertAll();
    }
}
```

**Output:**

```text
Step 1
Step 2
Assertion Failed
```

> The test continues executing after the failed assertion. The test is marked as failed only when `assertAll()` is called.

---

## Key Differences

* **Hard Assert** → Stops the test immediately when an assertion fails.
* **Soft Assert** → Continues executing the remaining test steps and reports all assertion failures at the end.
* **`assertAll()`** is mandatory for `SoftAssert`; otherwise, failed assertions are ignored.

## When to Use?

* ✅ **Hard Assert**

  * Verify critical functionality (e.g., login success, page load, payment completion).
  * Stop execution if the application is in an invalid state.

* ✅ **Soft Assert**

  * Verify multiple UI elements on the same page.
  * Collect all validation failures in a single test execution.

## Interview One-Liner

> **Hard Assert** stops the test execution as soon as an assertion fails, whereas **Soft Assert** allows the test to continue and reports all failures together when `assertAll()` is invoked.
