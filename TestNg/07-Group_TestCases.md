# Groups in TestNG

## What are Groups?

**Groups** in TestNG allow you to organize test methods into logical categories. You can execute a specific group of tests instead of running the entire test suite.

Common group names include:

* `smoke`
* `sanity`
* `regression`
* `integration`
* `ui`
* `api`

---

## Syntax

```java id="3k9b1a"
@Test(groups = "smoke")
public void loginTest() {
    // Test code
}
```

---

## Example

```java id="1w4d9z"
import org.testng.annotations.Test;

public class GroupExample {

    @Test(groups = "smoke")
    public void loginTest() {
        System.out.println("Login Test");
    }

    @Test(groups = "sanity")
    public void searchTest() {
        System.out.println("Search Test");
    }

    @Test(groups = "regression")
    public void paymentTest() {
        System.out.println("Payment Test");
    }
}
```

---

## Multiple Groups

A single test method can belong to multiple groups.

```java id="8n6r2x"
@Test(groups = {"smoke", "regression"})
public void loginTest() {
    System.out.println("Login Test");
}
```

---

## Running Specific Groups Using `testng.xml`

```xml id="2p7m5q"
<suite name="Suite">
    <test name="Smoke Tests">
        <groups>
            <run>
                <include name="smoke"/>
            </run>
        </groups>

        <classes>
            <class name="tests.GroupExample"/>
        </classes>
    </test>
</suite>
```

Only the test methods belonging to the **smoke** group will be executed.

---

## Excluding a Group

```xml id="7v1x0k"
<groups>
    <run>
        <exclude name="regression"/>
    </run>
</groups>
```

All tests except those in the **regression** group will be executed.

---

## Key Points

* Groups help organize test cases logically.
* A test method can belong to one or more groups.
* Groups can be included or excluded using `testng.xml`.
* Useful for running only **Smoke**, **Sanity**, or **Regression** tests.
* Improves test execution efficiency by avoiding unnecessary test runs.

---

## Common Group Names

| Group         | Purpose                                     |
| ------------- | ------------------------------------------- |
| `smoke`       | Verify critical functionality               |
| `sanity`      | Validate a specific feature after changes   |
| `regression`  | Ensure existing functionality is not broken |
| `integration` | Test interactions between modules           |
| `ui`          | User Interface tests                        |
| `api`         | API/Web Service tests                       |

---

## Interview One-Liner

> **Groups in TestNG** are used to categorize test methods so that specific sets of tests (such as Smoke, Sanity, or Regression) can be executed or excluded without running the entire test suite.
