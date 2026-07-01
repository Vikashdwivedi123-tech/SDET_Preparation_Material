# TestNG Life Cycle

## Introduction

**TestNG** is a popular testing framework for Java that provides annotations to control the execution flow of test cases. The TestNG lifecycle defines the order in which setup methods, test methods, and cleanup methods are executed.

Understanding the lifecycle helps in writing maintainable and efficient automation test suites.

---

# TestNG Annotation Hierarchy

The execution order of TestNG annotations is:

```text
@BeforeSuite
    ↓
@BeforeTest
    ↓
@BeforeClass
    ↓
@BeforeMethod
    ↓
@Test
    ↓
@AfterMethod
    ↓
@AfterClass
    ↓
@AfterTest
    ↓
@AfterSuite
```

---

# TestNG Lifecycle Annotations

## 1. @BeforeSuite

* Executes once before the entire test suite starts.
* Used for:

  * Initializing reports
  * Loading configuration files
  * Database connection setup
  * Starting Selenium Grid

```java
@BeforeSuite
public void beforeSuite() {
    System.out.println("Before Suite");
}
```

---

## 2. @BeforeTest

* Executes before the `<test>` tag in the TestNG XML.
* Used for:

  * Browser initialization
  * Environment setup
  * Common test configuration

```java
@BeforeTest
public void beforeTest() {
    System.out.println("Before Test");
}
```

---

## 3. @BeforeClass

* Executes once before the first test method of the current class.
* Used for:

  * Creating WebDriver instance
  * Initializing Page Objects
  * Loading test data

```java
@BeforeClass
public void beforeClass() {
    System.out.println("Before Class");
}
```

---

## 4. @BeforeMethod

* Executes before every `@Test` method.
* Used for:

  * Opening browser
  * Logging into application
  * Preparing test data

```java
@BeforeMethod
public void beforeMethod() {
    System.out.println("Before Method");
}
```

---

## 5. @Test

* Contains the actual test case.
* Can have:

  * Priority
  * Groups
  * Dependencies
  * Data Providers
  * Timeouts

```java
@Test
public void loginTest() {
    System.out.println("Executing Test");
}
```

---

## 6. @AfterMethod

* Executes after every test method.
* Used for:

  * Logout
  * Taking screenshots on failure
  * Closing browser tabs
  * Clearing cookies

```java
@AfterMethod
public void afterMethod() {
    System.out.println("After Method");
}
```

---

## 7. @AfterClass

* Executes once after all test methods in a class.
* Used for:

  * Closing WebDriver
  * Cleaning resources

```java
@AfterClass
public void afterClass() {
    System.out.println("After Class");
}
```

---

## 8. @AfterTest

* Executes after all classes inside a `<test>` tag.
* Used for:

  * Cleaning environment
  * Generating reports

```java
@AfterTest
public void afterTest() {
    System.out.println("After Test");
}
```

---

## 9. @AfterSuite

* Executes once after the entire suite finishes.
* Used for:

  * Closing database connection
  * Sending execution report
  * Releasing resources

```java
@AfterSuite
public void afterSuite() {
    System.out.println("After Suite");
}
```

---

# Complete Example

```java
import org.testng.annotations.*;

public class TestNGLifecycle {

    @BeforeSuite
    public void beforeSuite() {
        System.out.println("Before Suite");
    }

    @BeforeTest
    public void beforeTest() {
        System.out.println("Before Test");
    }

    @BeforeClass
    public void beforeClass() {
        System.out.println("Before Class");
    }

    @BeforeMethod
    public void beforeMethod() {
        System.out.println("Before Method");
    }

    @Test
    public void test1() {
        System.out.println("Executing Test 1");
    }

    @Test
    public void test2() {
        System.out.println("Executing Test 2");
    }

    @AfterMethod
    public void afterMethod() {
        System.out.println("After Method");
    }

    @AfterClass
    public void afterClass() {
        System.out.println("After Class");
    }

    @AfterTest
    public void afterTest() {
        System.out.println("After Test");
    }

    @AfterSuite
    public void afterSuite() {
        System.out.println("After Suite");
    }
}
```

---

# Expected Output

```text
Before Suite
Before Test
Before Class

Before Method
Executing Test 1
After Method

Before Method
Executing Test 2
After Method

After Class
After Test
After Suite
```

---

# Lifecycle Flow Diagram

```text
                    Test Suite Starts
                           │
                    @BeforeSuite
                           │
                     @BeforeTest
                           │
                     @BeforeClass
                           │
          ┌────────────────┴────────────────┐
          │                                 │
     @BeforeMethod                    @BeforeMethod
          │                                 │
        @Test 1                          @Test 2
          │                                 │
     @AfterMethod                     @AfterMethod
          └────────────────┬────────────────┘
                           │
                     @AfterClass
                           │
                      @AfterTest
                           │
                     @AfterSuite
                           │
                     Test Suite Ends
```

---

# Best Practices

* Use `@BeforeSuite` for suite-level initialization.
* Initialize the WebDriver in `@BeforeClass` whenever possible.
* Keep `@BeforeMethod` lightweight to reduce execution time.
* Capture screenshots inside `@AfterMethod` for failed tests.
* Always release resources in `@AfterClass` or `@AfterSuite`.
* Avoid placing test logic inside setup or teardown methods.

---

# Quick Revision Table

| Annotation      | Executes                          | Runs           |
| --------------- | --------------------------------- | -------------- |
| `@BeforeSuite`  | Before entire suite               | Once           |
| `@BeforeTest`   | Before `<test>` tag               | Once           |
| `@BeforeClass`  | Before first test method of class | Once per class |
| `@BeforeMethod` | Before every test method          | Every test     |
| `@Test`         | Actual test case                  | Every test     |
| `@AfterMethod`  | After every test method           | Every test     |
| `@AfterClass`   | After all methods in class        | Once per class |
| `@AfterTest`    | After `<test>` tag                | Once           |
| `@AfterSuite`   | After entire suite                | Once           |

---

## Summary

The TestNG lifecycle provides a structured execution flow for test automation. Proper use of lifecycle annotations helps improve test maintainability, ensures reliable setup and cleanup, and keeps automation suites organized and scalable.
