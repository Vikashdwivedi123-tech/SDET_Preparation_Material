# Priority in TestNG

## What is Priority?

In TestNG, the `priority` attribute is used to control the execution order of test methods.

* Lower priority values execute first.
* Higher priority values execute later.
* If no priority is specified, the default value is **0**.

---

## Syntax

```java
@Test(priority = 1)
public void testMethod() {
    // Test code
}
```

---

## Example

```java
import org.testng.annotations.Test;

public class PriorityExample {

    @Test(priority = 2)
    public void payment() {
        System.out.println("Payment");
    }

    @Test(priority = 0)
    public void login() {
        System.out.println("Login");
    }

    @Test(priority = 1)
    public void addToCart() {
        System.out.println("Add to Cart");
    }
}
```

### Output

```text
Login
Add to Cart
Payment
```

---

## Default Priority

If no priority is assigned, TestNG considers it as **priority = 0**.

```java
@Test
public void login() {
    System.out.println("Login");
}

@Test(priority = 1)
public void payment() {
    System.out.println("Payment");
}
```

### Output

```text
Login
Payment
```

---

## Negative Priority

TestNG also supports negative priority values.

```java
@Test(priority = -1)
public void setup() {
    System.out.println("Setup");
}

@Test(priority = 0)
public void login() {
    System.out.println("Login");
}
```

### Output

```text
Setup
Login
```

---

## Same Priority

If multiple test methods have the **same priority**, TestNG executes them in **alphabetical order of their method names**.

```java
@Test(priority = 1)
public void addToCart() {
    System.out.println("Add to Cart");
}

@Test(priority = 1)
public void login() {
    System.out.println("Login");
}

@Test(priority = 1)
public void payment() {
    System.out.println("Payment");
}
```

### Output

```text
Add to Cart
Login
Payment
```

---

## Key Points

* Default priority is **0**.
* Lower priority executes first.
* Negative priorities are allowed.
* Methods with the same priority execute in **alphabetical order**.
* Priority controls execution order **within the same test class**.

---

## Interview One-Liner

> **Priority in TestNG** is used to define the execution order of test methods. Lower priority values run first, the default priority is **0**, and methods with the same priority are executed in alphabetical order.
