# What is `testng.xml` and Why is it Used?

## What is `testng.xml`?

`testng.xml` is the **configuration file** of TestNG. It controls how test cases are executed without modifying the Java test code.

It allows you to define:

* Which test classes to execute
* Test execution order
* Parallel execution
* Browser/environment parameters
* Test groups
* Listeners
* Suite configuration

---

# Why is `testng.xml` Used?

It provides flexibility to manage test execution from a single configuration file.

Common uses include:

* Running specific test classes or packages
* Executing Smoke, Sanity, or Regression suites
* Passing parameters (e.g., browser, URL)
* Enabling parallel execution
* Setting thread count
* Registering listeners
* Organizing multiple test suites

---

# Basic Structure of `testng.xml`

```xml id="4zox0j"
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">

<suite name="Automation Suite">

    <test name="Login Tests">

        <classes>
            <class name="tests.LoginTest"/>
            <class name="tests.HomePageTest"/>
        </classes>

    </test>

</suite>
```

---

# Common Features of `testng.xml`

## 1. Run Multiple Test Classes

```xml id="ecg4vd"
<classes>
    <class name="tests.LoginTest"/>
    <class name="tests.PaymentTest"/>
</classes>
```

---

## 2. Pass Parameters

```xml id="c5gvc0"
<parameter name="browser" value="chrome"/>

<test name="Tests">
    <classes>
        <class name="tests.LoginTest"/>
    </classes>
</test>
```

Java Code

```java id="shbgfh"
@Parameters("browser")
@Test
public void launchBrowser(String browser) {
    System.out.println(browser);
}
```

---

## 3. Run Groups

```xml id="g9azv2"
<groups>
    <run>
        <include name="smoke"/>
    </run>
</groups>
```

Only the **smoke** group will execute.

---

## 4. Parallel Execution

```xml id="jlwmdd"
<suite name="Suite"
       parallel="classes"
       thread-count="3">
```

Runs test classes in parallel using three threads.

---

## 5. Register Listeners

```xml id="yx4b1o"
<listeners>
    <listener class-name="listeners.TestListener"/>
</listeners>
```

Registers a TestNG listener for logging, reporting, screenshots, etc.

---

# Advantages

* No need to modify Java code to change execution.
* Supports multiple test suites.
* Enables parameterization.
* Supports parallel execution.
* Allows execution of specific groups.
* Easy integration with CI/CD pipelines like Jenkins.

---

# Interview Questions

### Q1. What is `testng.xml`?

It is the configuration file of TestNG that controls test execution.

---

### Q2. Can TestNG run without `testng.xml`?

**Yes.** You can run individual test classes directly. However, features such as **parallel execution**, **groups**, **parameters**, **listeners**, and **suite management** typically require `testng.xml`.

---

### Q3. What are the main tags in `testng.xml`?

* `<suite>`
* `<test>`
* `<classes>`
* `<class>`
* `<groups>`
* `<parameter>`
* `<listeners>`

---

# Interview One-Liner

> **`testng.xml` is the configuration file of TestNG used to control test execution. It enables features such as suite management, parameterization, group execution, listener registration, and parallel execution without changing the test code.**
