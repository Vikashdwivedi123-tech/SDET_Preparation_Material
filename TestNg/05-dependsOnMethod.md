# `dependsOnMethods` and `alwaysRun` in TestNG

## What is `dependsOnMethods`?

`dependsOnMethods` is a TestNG attribute used to define a dependency between test methods. A test method will execute **only if the method it depends on passes successfully**.

---

## Syntax

```java
@Test(dependsOnMethods = "methodName")
```

---

## Example

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class DependsOnMethodsExample {

    @Test
    public void login() {
        System.out.println("Login Successful");
        Assert.assertTrue(true);
    }

    @Test(dependsOnMethods = "login")
    public void addToCart() {
        System.out.println("Product Added to Cart");
    }

    @Test(dependsOnMethods = "addToCart")
    public void payment() {
        System.out.println("Payment Successful");
    }
}
```

### Output

```text
Login Successful
Product Added to Cart
Payment Successful
```

---

## What Happens If the Dependency Fails?

```java
@Test
public void login() {
    Assert.fail("Login Failed");
}

@Test(dependsOnMethods = "login")
public void addToCart() {
    System.out.println("Product Added");
}
```

### Result

```text
login → FAILED
addToCart → SKIPPED
```

> If the dependent method fails or is skipped, the dependent test is **skipped** by default.

---

# `alwaysRun = true`

The `alwaysRun` attribute forces a test method to execute **even if its dependent method fails or is skipped**.

## Syntax

```java
@Test(dependsOnMethods = "login", alwaysRun = true)
```

---

## Example

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class AlwaysRunExample {

    @Test
    public void login() {
        System.out.println("Login");
        Assert.fail("Login Failed");
    }

    @Test(dependsOnMethods = "login", alwaysRun = true)
    public void logout() {
        System.out.println("Logout Executed");
    }
}
```

### Output

```text
Login
Logout Executed
```

> Even though `login()` fails, `logout()` still executes because `alwaysRun = true`.

---

## Key Points

* `dependsOnMethods` creates a dependency between test methods.
* By default, if the dependency fails, the dependent test is **skipped**.
* Setting `alwaysRun = true` overrides this behavior and forces the dependent test to run.
* `alwaysRun` is commonly used for **cleanup tasks**, **logout**, **browser closing**, or **resource release** that should execute regardless of previous test failures.

---

## Comparison

| Feature                  | `dependsOnMethods`        | `alwaysRun = true`         |
| ------------------------ | ------------------------- | -------------------------- |
| Creates dependency       | ✅ Yes                     | Used with dependency       |
| Runs if dependency fails | ❌ No                      | ✅ Yes                      |
| Dependent test status    | Skipped                   | Executed                   |
| Common Use Case          | Sequential test execution | Cleanup and teardown tasks |

---

## Interview One-Liner

> **`dependsOnMethods`** ensures a test runs only after another test passes, while **`alwaysRun = true`** forces the test to execute even if the dependent test fails or is skipped, making it ideal for cleanup or teardown operations.
