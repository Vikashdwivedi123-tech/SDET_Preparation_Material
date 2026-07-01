# How Can We Disable or Skip a Test Case in TestNG?

There are multiple ways to disable or skip a test case in TestNG, depending on the requirement.

---

# 1. Disable a Test Using `enabled = false`

The simplest way to prevent a test from executing is by setting the `enabled` attribute to `false`.

## Example

```java id="x3vg8t"
import org.testng.annotations.Test;

public class LoginTest {

    @Test(enabled = false)
    public void loginTest() {
        System.out.println("This test will not execute.");
    }
}
```

**Result:** The test is **not executed** and is marked as **Disabled**.

---

# 2. Skip a Test Using `SkipException`

If you want to skip a test dynamically at runtime, throw a `SkipException`.

## Example

```java id="egkn8t"
import org.testng.SkipException;
import org.testng.annotations.Test;

public class LoginTest {

    @Test
    public void loginTest() {

        throw new SkipException("Skipping the test");
    }
}
```

**Result:** The test is **Skipped** during execution.

---

# 3. Skip Due to Failed Dependency

If a test depends on another test using `dependsOnMethods` and the dependency fails, TestNG automatically skips the dependent test.

```java id="5d2bnm"
@Test
public void login() {
    Assert.fail();
}

@Test(dependsOnMethods = "login")
public void payment() {
    System.out.println("Payment");
}
```

**Result:**

```text id="pjlwm8"
login   → FAILED
payment → SKIPPED
```

---

# Disabled vs Skipped

| Feature       | Disabled (`enabled = false`) | Skipped (`SkipException`)        |
| ------------- | ---------------------------- | -------------------------------- |
| Executed      | ❌ No                         | Starts execution, then skips     |
| Decision Time | Before execution             | During execution                 |
| Use Case      | Temporarily disable a test   | Skip based on runtime conditions |

---

# Best Practices

* Use **`enabled = false`** to temporarily disable incomplete or unnecessary tests.
* Use **`SkipException`** when a test should be skipped based on runtime conditions (e.g., environment unavailable, feature disabled).
* Avoid leaving tests permanently disabled in production test suites.

---

# Interview Questions

### Q1. How do you disable a test case in TestNG?

Using:

```java id="3q5x6s"
@Test(enabled = false)
```

---

### Q2. How do you skip a test during execution?

By throwing a `SkipException`.

```java id="n5j7yx"
throw new SkipException("Skipping test");
```

---

### Q3. What is the difference between disabling and skipping a test?

* **Disabled (`enabled = false`)** → The test is never executed.
* **Skipped (`SkipException`)** → The test begins execution but is skipped based on a runtime condition.

---

# Interview One-Liner

> **A test can be disabled using `@Test(enabled = false)` before execution or skipped dynamically during execution by throwing a `SkipException`. TestNG also automatically skips dependent tests if their prerequisite tests fail.**
