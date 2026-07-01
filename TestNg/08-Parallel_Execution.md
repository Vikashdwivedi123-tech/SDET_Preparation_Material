# Parallel Execution in TestNG

## What is Parallel Execution?

Parallel execution in TestNG allows multiple test cases to run simultaneously using multiple threads. It helps reduce test execution time and improves the efficiency of automation suites.

Parallel execution is configured in the **`testng.xml`** file using the `parallel` and `thread-count` attributes.

---

# Syntax

```xml
<suite name="Suite" parallel="methods" thread-count="3">
    ...
</suite>
```

* **parallel** → Defines what runs in parallel.
* **thread-count** → Specifies the maximum number of threads.

---

# Types of Parallel Execution

## 1. Parallel by Methods

Runs multiple **test methods** in parallel.

### testng.xml

```xml
<suite name="Suite" parallel="methods" thread-count="2">
    <test name="MethodExecution">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>
</suite>
```

### Example

```java
@Test
public void test1() {
    System.out.println("Test 1 - " + Thread.currentThread().getId());
}

@Test
public void test2() {
    System.out.println("Test 2 - " + Thread.currentThread().getId());
}
```

**Use Case:** Independent test methods.

---

## 2. Parallel by Classes

Runs different **test classes** in parallel.

### testng.xml

```xml
<suite name="Suite" parallel="classes" thread-count="2">
    <test name="ClassExecution">
        <classes>
            <class name="tests.LoginTest"/>
            <class name="tests.PaymentTest"/>
        </classes>
    </test>
</suite>
```

**Use Case:** Each class has its own WebDriver instance.

---

## 3. Parallel by Tests

Runs multiple **`<test>`** tags in parallel.

### testng.xml

```xml
<suite name="Suite" parallel="tests" thread-count="2">

    <test name="Chrome">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>

    <test name="Firefox">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>

</suite>
```

**Use Case:** Cross-browser testing.

---

## 4. Parallel by Instances

Runs different **instances of the same test class** in parallel.

### testng.xml

```xml
<suite name="Suite" parallel="instances" thread-count="2">
    ...
</suite>
```

**Use Case:** Factory-based tests (`@Factory`) where multiple object instances are created.

---

# Parallel Execution Using DataProvider

A `@DataProvider` can also execute test data in parallel.

```java
@DataProvider(name = "loginData", parallel = true)
public Object[][] getData() {
    return new Object[][]{
        {"user1", "pass1"},
        {"user2", "pass2"},
        {"user3", "pass3"}
    };
}

@Test(dataProvider = "loginData")
public void loginTest(String user, String pass) {
    System.out.println(user + " - " + Thread.currentThread().getId());
}
```

Each dataset can run on a separate thread.

---

# Thread Count

The `thread-count` attribute controls the maximum number of threads used for parallel execution.

```xml
<suite name="Suite" parallel="methods" thread-count="5">
```

If there are more tests than threads, TestNG schedules the remaining tests as threads become available.

---

# Best Practices

* Use **ThreadLocal<WebDriver>** to maintain a separate WebDriver instance for each thread.
* Avoid using shared global variables in parallel tests.
* Ensure test cases are independent.
* Use parallel execution only when tests are thread-safe.
* Prefer `parallel="classes"` or `parallel="tests"` for Selenium WebDriver projects.

---

# Comparison

| Parallel Type                    | Executes in Parallel | Common Use Case          |
| -------------------------------- | -------------------- | ------------------------ |
| `methods`                        | Test methods         | Independent test methods |
| `classes`                        | Test classes         | Multiple test classes    |
| `tests`                          | `<test>` tags        | Cross-browser testing    |
| `instances`                      | Object instances     | `@Factory` execution     |
| `@DataProvider(parallel = true)` | Test data sets       | Data-driven testing      |

---

# Interview Questions

### Q1. How many ways can you achieve parallel execution in TestNG?

There are **five** common ways:

1. `parallel="methods"`
2. `parallel="classes"`
3. `parallel="tests"`
4. `parallel="instances"`
5. `@DataProvider(parallel = true)`

---

### Q2. Which parallel mode is commonly used in Selenium?

* **`parallel="classes"`** – Each class can maintain its own WebDriver instance.
* **`parallel="tests"`** – Commonly used for cross-browser execution.

---

### Q3. Why do we use `ThreadLocal` with Selenium?

Because WebDriver is **not thread-safe**. `ThreadLocal<WebDriver>` ensures each parallel thread gets its own isolated WebDriver instance, preventing conflicts between tests.

---

# Interview One-Liner

> **Parallel execution in TestNG** allows tests to run simultaneously using multiple threads. It can be achieved using **methods, classes, tests, instances, or parallel DataProviders**, significantly reducing execution time for large automation suites.
