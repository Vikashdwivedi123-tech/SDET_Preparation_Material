# POJO (Plain Old Java Object) in Java

## What is a POJO?

**POJO (Plain Old Java Object)** is a simple Java class that is not bound to any special framework restrictions. It is primarily used to represent data through fields, constructors, getters, and setters.

A POJO class:

* Contains private instance variables.
* Provides public getter and setter methods.
* May contain constructors.
* Does not need to extend any specific class.
* Does not need to implement any specific interface.

---

## Simple POJO Example

```java
public class Employee {

    private int id;
    private String name;

    public Employee() {
    }

    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

---

# Why Do We Use POJOs?

POJOs provide:

* Better code readability
* Encapsulation of data
* Easy maintenance
* Object-oriented representation of data
* API request and response mapping

Common use cases:

* API Automation
* Data Transfer Objects (DTOs)
* Database Entities
* Configuration Objects

---

# Components of a POJO Class

## 1. Private Variables

```java
private int id;
private String name;
```

These variables store the object's data.

---

## 2. Getter Methods

Used to retrieve field values.

```java
public String getName() {
    return name;
}
```

---

## 3. Setter Methods

Used to update field values.

```java
public void setName(String name) {
    this.name = name;
}
```

---

## 4. Constructors

### Default Constructor

```java
public Employee() {
}
```

### Parameterized Constructor

```java
public Employee(int id, String name) {
    this.id = id;
    this.name = name;
}
```

---

# Creating and Using a POJO Object

```java
Employee emp = new Employee();

emp.setId(101);
emp.setName("Vikash");

System.out.println(emp.getName());
```

### Output

```text
Vikash
```

---

# POJO in API Automation

POJOs are extensively used in Rest Assured for handling request and response payloads.

---

## Request Serialization

### POJO Class

```java
public class User {

    private String name;
    private String job;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }
}
```

### Creating Request Payload

```java
User user = new User();

user.setName("John");
user.setJob("QA Engineer");
```

### Rest Assured Request

```java
given()
    .body(user)
.when()
    .post("/users");
```

Generated JSON:

```json
{
  "name": "John",
  "job": "QA Engineer"
}
```

This process is called **Serialization**.

---

# Serialization

## Definition

Serialization is the process of converting a Java object into JSON.

### Example

```java
User user = new User();

user.setName("John");
user.setJob("QA Engineer");
```

Converted JSON:

```json
{
  "name": "John",
  "job": "QA Engineer"
}
```

---

# Deserialization

## Definition

Deserialization is the process of converting JSON into a Java object.

### API Response

```json
{
  "name": "John",
  "job": "QA Engineer"
}
```

### Conversion to POJO

```java
User user = response.as(User.class);

System.out.println(user.getName());
```

### Output

```text
John
```

---

# Nested POJO Example

API Response:

```json
{
  "name": "Vikash",
  "address": {
    "city": "Delhi",
    "pin": "110001"
  }
}
```

---

## Address POJO

```java
public class Address {

    private String city;
    private String pin;

    public String getCity() {
        return city;
    }

    public void setCity(String city) {
        this.city = city;
    }

    public String getPin() {
        return pin;
    }

    public void setPin(String pin) {
        this.pin = pin;
    }
}
```

---

## Employee POJO

```java
public class Employee {

    private String name;
    private Address address;

    public String getName() {
        return name;
    }

    public Address getAddress() {
        return address;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAddress(Address address) {
        this.address = address;
    }
}
```

---

## Accessing Nested Data

```java
Employee emp = response.as(Employee.class);

System.out.println(emp.getAddress().getCity());
```

### Output

```text
Delhi
```

---

# POJO vs JavaBean

| Feature                 | POJO     | JavaBean         |
| ----------------------- | -------- | ---------------- |
| Simple Java Class       | Yes      | Yes              |
| Private Fields          | Optional | Required         |
| Getter/Setter Methods   | Optional | Required         |
| No-Argument Constructor | Optional | Required         |
| Serializable            | Optional | Usually Required |

### Key Point

Every JavaBean is a POJO, but every POJO is not a JavaBean.

---

# POJO vs DTO

## DTO (Data Transfer Object)

DTO is used specifically to transfer data between application layers.

```java
public class EmployeeDTO {

    private String name;
    private String email;
}
```

### Difference

| POJO                       | DTO                        |
| -------------------------- | -------------------------- |
| General-purpose object     | Used for data transfer     |
| May contain business logic | Usually contains only data |
| Broader concept            | Specific use case          |

---

# Advantages of POJO

* Easy to understand and maintain
* Supports encapsulation
* Reusable across applications
* Framework independent
* Ideal for API request and response modeling
* Improves code readability

---

# POJO Interview Questions

### 1. What is a POJO?

A POJO (Plain Old Java Object) is a simple Java class used to represent data through fields, constructors, getters, and setters without depending on any framework-specific requirements.

---

### 2. Why is POJO used in API Automation?

POJOs are used to create request payloads and convert API responses into Java objects through serialization and deserialization.

---

### 3. What is Serialization?

Serialization is the process of converting a Java object into JSON.

---

### 4. What is Deserialization?

Deserialization is the process of converting JSON into a Java object.

---

### 5. Can a POJO contain methods?

Yes. A POJO can contain business methods in addition to variables, constructors, getters, and setters.

---

### 6. Is every JavaBean a POJO?

Yes.

---

### 7. Is every POJO a JavaBean?

No. JavaBeans have additional requirements such as private fields, public getters/setters, and a no-argument constructor.

---

# SDET Interview Answer

**POJO stands for Plain Old Java Object. It is a simple Java class that contains variables, constructors, getters, and setters. In API automation, POJOs are commonly used for serialization and deserialization. Serialization converts Java objects into JSON request payloads, while deserialization converts JSON responses into Java objects. POJOs improve code readability, maintainability, and type safety, making them an essential part of Rest Assured API automation frameworks.**
