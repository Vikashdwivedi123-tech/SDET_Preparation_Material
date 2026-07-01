# Which Annotation is Used to Run a Single Test Method Multiple Times?

## Answer

In TestNG, the **`invocationCount`** attribute of the `@Test` annotation is used to execute a test method multiple times.

---

## Syntax

```java
@Test(invocationCount = 5)
public void testMethod() {
    // Test code
}
```

The above test method will execute **5 times**.

---

## Example

```java
import org.testng.annotations.Test;

public class InvocationCountExample {

    @Test(invocationCount = 3)
    public void loginTest() {
        System.out.println("Login Test Executed");
    }
}
```

### Output

```text
Login Test Executed
Login Test Executed
Login Test Executed
```

---

## Running Invocations in Parallel

You can execute multiple invocations in parallel by using the `threadPoolSize` attribute.

```java
@Test(invocationCount = 5, threadPoolSize = 2)
public void loginTest() {
    System.out.println(
        "Thread: " + Thread.currentThread().getId()
    );
}
```

In this example:

* `invocationCount = 5` → The test executes **5 times**.
* `threadPoolSize = 2` → Up to **2 threads** execute the invocations concurrently.

---

## Common Use Cases

* Load testing a feature.
* Verifying application stability.
* Repeating flaky scenarios.
* Stress testing APIs.
* Running the same test multiple times without duplicating code.

---

## Related Attributes

| Attribute         | Purpose                                         |
| ----------------- | ----------------------------------------------- |
| `invocationCount` | Number of times a test method should execute    |
| `threadPoolSize`  | Number of threads used for parallel invocations |
| `timeOut`         | Maximum time allowed for the test execution     |

---

## Interview Questions

### Q1. Which annotation is used to run a test method multiple times?

The `@Test` annotation with the **`invocationCount`** attribute.

---

### Q2. Can multiple invocations run in parallel?

**Yes.** By specifying `threadPoolSize` along with `invocationCount`.

Example:

```java
@Test(invocationCount = 10, threadPoolSize = 3)
```

---

### Q3. What is the difference between `invocationCount` and `@DataProvider`?

| `invocationCount`                     | `@DataProvider`                               |
| ------------------------------------- | --------------------------------------------- |
| Executes the same test multiple times | Executes the test with different sets of data |
| Same input every time                 | Different input for each execution            |

---

## Interview One-Liner

> **To execute a single test method multiple times in TestNG, use the `invocationCount` attribute of the `@Test` annotation. For parallel execution of those invocations, combine it with `threadPoolSize`.**
