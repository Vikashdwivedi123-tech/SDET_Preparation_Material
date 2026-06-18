# Hard Assert vs Soft Assert in TestNG

## What is Assertion?

Assertions are used to validate whether the actual result matches the expected result.

If the validation fails, the test case is marked as failed.

TestNG provides two types of assertions:

1. Hard Assert
2. Soft Assert

---

# Hard Assert

## What is Hard Assert?

A Hard Assert immediately stops the execution of the test method when an assertion fails.

Any code written after the failed assertion will not execute.

### Syntax

```java
Assert.assertEquals(actual, expected);
```

### Example

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class HardAssertExample {

    @Test
    public void testLogin() {

        System.out.println("Step 1");

        Assert.assertEquals("Google", "Facebook");

        System.out.println("Step 2");
    }
}
```

### Output

```text
Step 1

Assertion Failed
```

```text
Step 2
```

will not execute.

---

# Soft Assert

## What is Soft Assert?

A Soft Assert does not stop test execution when an assertion fails.

All assertions are executed, and failures are reported at the end using:

```java
assertAll();
```

### Syntax

```java
SoftAssert softAssert = new SoftAssert();

softAssert.assertEquals(actual, expected);

softAssert.assertAll();
```

### Example

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

### Output

```text
Step 1
Step 2

Assertion Failed
```

Even though the assertion failed, execution continued.

---

# Why is assertAll() Mandatory?

Consider:

```java
SoftAssert softAssert = new SoftAssert();

softAssert.assertEquals("Google", "Facebook");
```

Without:

```java
softAssert.assertAll();
```

TestNG will not mark the test as failed.

The test may incorrectly appear as passed.

### Correct Usage

```java
SoftAssert softAssert = new SoftAssert();

softAssert.assertEquals("Google", "Facebook");

softAssert.assertAll();
```

---

# Difference Between Hard Assert and Soft Assert

| Hard Assert                                | Soft Assert                                       |
| ------------------------------------------ | ------------------------------------------------- |
| Stops execution immediately after failure. | Continues execution after failure.                |
| No need for assertAll().                   | assertAll() is mandatory.                         |
| Failure is reported instantly.             | Failures are collected and reported at the end.   |
| Suitable for critical validations.         | Suitable for multiple validations.                |
| Less information if first assertion fails. | Provides all validation failures in a single run. |

---

# Real-Time Example

## Hard Assert

Suppose we are validating:

* Page Title
* Logo
* Username

If Page Title validation fails:

```java
Assert.assertEquals(actualTitle, expectedTitle);
```

Remaining validations will not execute.

---

## Soft Assert

```java
SoftAssert softAssert = new SoftAssert();

softAssert.assertEquals(actualTitle, expectedTitle);

softAssert.assertTrue(isLogoDisplayed);

softAssert.assertEquals(actualUser, expectedUser);

softAssert.assertAll();
```

All validations execute even if one fails.

---

# When to Use Hard Assert?

Use Hard Assert when:

* Validation is critical.
* Further execution makes no sense after failure.

Example:

```java
Assert.assertTrue(driver.getTitle().contains("Login"));
```

If Login page itself is not loaded, there is no point proceeding.

---

# When to Use Soft Assert?

Use Soft Assert when:

* Multiple validations need to be performed.
* You want to see all failures in a single execution.

Example:

* Verify Title
* Verify Logo
* Verify Username
* Verify Footer

---

# Frequently Asked Interview Questions

## Q1. What is Hard Assert?

Hard Assert stops test execution immediately when an assertion fails.

---

## Q2. What is Soft Assert?

Soft Assert continues execution even if an assertion fails and reports all failures at the end using assertAll().

---

## Q3. What happens if assertAll() is not used?

The test may be marked as passed even when assertions fail.

---

## Q4. Which assertion is used more frequently?

```text
Hard Assert
```

because most validations are critical.

---

## Q5. What is the biggest advantage of Soft Assert?

It allows multiple validations to execute and reports all failures together.

---

# Interview Answer

**Hard Assert immediately stops test execution when an assertion fails, whereas Soft Assert allows execution to continue and collects all failures until assertAll() is called. Hard Assert is used for critical validations, while Soft Assert is useful when multiple validations need to be performed within the same test case.**
