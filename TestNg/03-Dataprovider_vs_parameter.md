# `@DataProvider` vs `@Parameters` in TestNG

| Feature                     | `@DataProvider`                                  | `@Parameters`                                |
| --------------------------- | ------------------------------------------------ | -------------------------------------------- |
| Purpose                     | Pass multiple sets of test data to a test method | Pass values from the `testng.xml` file       |
| Data Source                 | Java method returning `Object[][]`               | `testng.xml` configuration file              |
| Number of Executions        | Runs the test once for each data set             | Runs once with the provided parameter values |
| Best Use Case               | Data-driven testing                              | Environment or configuration values          |
| Supports Multiple Data Sets | ✅ Yes                                            | ❌ No                                         |
| Runtime Flexibility         | High                                             | Limited                                      |
| Annotation                  | `@DataProvider`                                  | `@Parameters`                                |

## `@DataProvider` Example

```java
@DataProvider(name = "loginData")
public Object[][] getData() {
    return new Object[][]{
        {"admin", "admin123"},
        {"user", "user123"}
    };
}

@Test(dataProvider = "loginData")
public void loginTest(String username, String password) {
    System.out.println(username + " " + password);
}
```

**Output:**

```text
admin admin123
user user123
```

---

## `@Parameters` Example

**testng.xml**

```xml
<suite name="Suite">
    <test name="Test">
        <parameter name="browser" value="chrome"/>
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>
</suite>
```

**Java Code**

```java
@Parameters("browser")
@Test
public void launchBrowser(String browser) {
    System.out.println(browser);
}
```

**Output:**

```text
chrome
```

---

## When to Use Which?

* Use **`@DataProvider`** when you need to execute the same test with **multiple sets of data** (e.g., different usernames and passwords).
* Use **`@Parameters`** when you need to pass **configuration values** such as browser, environment, or URL from `testng.xml`.

## Interview One-Liner

> **`@DataProvider`** is used for **data-driven testing**, while **`@Parameters`** is used for **configuration values defined in `testng.xml`**.
