# `@BeforeTest` vs `@BeforeMethod` in TestNG

| Feature          | `@BeforeTest`                                                    | `@BeforeMethod`                                     |
| ---------------- | ---------------------------------------------------------------- | --------------------------------------------------- |
| Execution        | Runs once before the `<test>` tag in `testng.xml`                | Runs before every `@Test` method                    |
| Frequency        | Once per `<test>` tag                                            | Once for each test method                           |
| Scope            | Applies to all classes inside the same `<test>` tag              | Applies only to the current test method             |
| Purpose          | One-time test setup                                              | Fresh setup before each test                        |
| Common Use Cases | Browser initialization, environment setup, loading configuration | Login, test data setup, resetting application state |

---

## Example

### testng.xml

```xml id="0w8ks4"
<suite name="Suite">

    <test name="LoginTests">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>

</suite>
```

### Java Code

```java id="7w52qg"
import org.testng.annotations.*;

public class LoginTest {

    @BeforeTest
    public void beforeTest() {
        System.out.println("Before Test");
    }

    @BeforeMethod
    public void beforeMethod() {
        System.out.println("Before Method");
    }

    @Test
    public void test1() {
        System.out.println("Test 1");
    }

    @Test
    public void test2() {
        System.out.println("Test 2");
    }
}
```

### Output

```text id="m1m3tw"
Before Test

Before Method
Test 1

Before Method
Test 2
```

---

## Execution Flow

```text id="zptqoj"
@BeforeTest
      │
      ▼
@BeforeMethod
      │
      ▼
@Test 1
      │
      ▼
@BeforeMethod
      │
      ▼
@Test 2
```

---

## Key Differences

* **`@BeforeTest`**

  * Executes **once** before all test methods within a `<test>` tag.
  * Suitable for expensive one-time setup.
  * Can be shared across multiple classes in the same `<test>`.

* **`@BeforeMethod`**

  * Executes **before every** `@Test` method.
  * Ensures each test starts with a clean state.
  * Ideal for login, test data preparation, or resetting the application.

---

## When to Use?

### Use `@BeforeTest` for:

* Browser initialization
* Reading configuration files
* Establishing database connections
* Environment setup

### Use `@BeforeMethod` for:

* User login
* Clearing cookies
* Preparing test data
* Navigating to the required page
* Resetting application state before each test

---

## Interview Question

### Q. What is the difference between `@BeforeTest` and `@BeforeMethod`?

**Answer:**
`@BeforeTest` executes **once** before the `<test>` tag in `testng.xml` and is typically used for one-time setup, whereas `@BeforeMethod` executes **before every `@Test` method** and is used to prepare a fresh environment for each test.

---

## Interview One-Liner

> **`@BeforeTest` is executed once before all tests in a `<test>` tag, while `@BeforeMethod` is executed before every individual test method to ensure each test starts with a clean setup.**
