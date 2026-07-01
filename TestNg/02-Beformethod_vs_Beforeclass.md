# `@BeforeMethod` vs `@BeforeClass` in TestNG

| Feature          | `@BeforeMethod`                                         | `@BeforeClass`                                                              |
| ---------------- | ------------------------------------------------------- | --------------------------------------------------------------------------- |
| Execution        | Runs before **every** `@Test` method                    | Runs **once** before the first `@Test` method in the class                  |
| Frequency        | Once per test method                                    | Once per test class                                                         |
| Purpose          | Prepare each test with a fresh setup                    | Perform one-time initialization for the class                               |
| Common Use Cases | Login, test data setup, browser refresh, cookie cleanup | WebDriver initialization, Page Object initialization, configuration loading |
| Performance      | Slower (executes multiple times)                        | Faster (executes only once)                                                 |

## Example

```java
public class DemoTest {

    @BeforeClass
    public void beforeClass() {
        System.out.println("Browser launched");
    }

    @BeforeMethod
    public void beforeMethod() {
        System.out.println("User logged in");
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

```text
Browser launched

User logged in
Test 1

User logged in
Test 2
```

## Key Difference

* **`@BeforeClass`** → Executes **once** before all test methods in a class.
* **`@BeforeMethod`** → Executes **before every** test method, ensuring each test starts with a fresh setup.

> **Interview Tip:**
> Use **`@BeforeClass`** for expensive one-time setup (e.g., launching the browser) and **`@BeforeMethod`** for actions that must run before each test (e.g., logging in or resetting test data).
