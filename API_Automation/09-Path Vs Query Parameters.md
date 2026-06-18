# Path Parameters vs Query Parameters in Rest Assured

## Introduction

While testing APIs, we often need to pass values in the URL.

There are two common ways to do this:

1. Path Parameters
2. Query Parameters

This is one of the most frequently asked Rest Assured interview questions.

---

# Real-Life Analogy

Imagine you are searching for a book in a library.

### Path Parameter

You know the exact Book ID.

```text
/library/books/101
```

Here, **101** uniquely identifies the book.

---

### Query Parameter

You want to search books using filters.

```text
/library/books?author=James&year=2025
```

Here, you are filtering the results.

---

# What is a Path Parameter?

A Path Parameter is a value that becomes part of the URL path.

It is generally used to identify a specific resource.

## URL Example

```text
https://api.example.com/users/101
```

Here:

```text
101
```

is the Path Parameter.

The API is asking:

> "Give me the details of User 101."

---

## Path Parameter Syntax

```text
/users/{id}
```

where:

```text
id = 101
```

Final URL:

```text
/users/101
```

---

# Path Parameter in Rest Assured

## Example 1

```java
given()
    .pathParam("id", 2)
.when()
    .get("https://reqres.in/api/users/{id}")
.then()
    .statusCode(200);
```

---

## How It Works

Rest Assured replaces:

```java
{id}
```

with

```java
2
```

Final URL becomes:

```text
https://reqres.in/api/users/2
```

---

# Multiple Path Parameters

URL:

```text
/orders/100/products/200
```

Here:

```text
100 = Order ID
200 = Product ID
```

### Rest Assured

```java
given()
    .pathParam("orderId", 100)
    .pathParam("productId", 200)
.when()
    .get("/orders/{orderId}/products/{productId}")
.then()
    .statusCode(200);
```

---

# What is a Query Parameter?

Query Parameters are used to filter, sort, or search data.

They come after the question mark (?).

## URL Example

```text
https://api.example.com/users?page=2
```

Here:

```text
page=2
```

is a Query Parameter.

The API is asking:

> "Give me users from page 2."

---

# Query Parameter Syntax

```text
/users?page=2
```

where:

```text
page = 2
```

---

# Query Parameter in Rest Assured

## Example

```java
given()
    .queryParam("page", 2)
.when()
    .get("https://reqres.in/api/users")
.then()
    .statusCode(200);
```

---

## How It Works

Rest Assured automatically generates:

```text
https://reqres.in/api/users?page=2
```

---

# Multiple Query Parameters

URL:

```text
/users?page=2&status=active
```

### Rest Assured

```java
given()
    .queryParam("page", 2)
    .queryParam("status", "active")
.when()
    .get("/users")
.then()
    .statusCode(200);
```

Generated URL:

```text
/users?page=2&status=active
```

---

# Key Difference

| Path Parameter                 | Query Parameter             |
| ------------------------------ | --------------------------- |
| Identifies a specific resource | Filters or modifies results |
| Part of URL path               | Comes after ?               |
| Usually mandatory              | Usually optional            |
| Used for IDs                   | Used for search/filter/sort |
| Example: /users/101            | Example: /users?page=2      |

---

# Visual Difference

## Path Parameter

```text
/users/101
```

Meaning:

```text
Fetch User 101
```

---

## Query Parameter

```text
/users?page=2
```

Meaning:

```text
Fetch users from page 2
```

---

# Example Comparison

## Path Parameter

```text
GET /employees/123
```

Question:

```text
Which employee?
```

Answer:

```text
Employee 123
```

---

## Query Parameter

```text
GET /employees?department=QA
```

Question:

```text
Which department?
```

Answer:

```text
QA Department Employees
```

---

# Using Both Together

Many APIs use both Path and Query Parameters.

### URL

```text
/users/101/orders?status=completed
```

Meaning:

```text
Get completed orders of User 101
```

---

### Rest Assured Example

```java
given()
    .pathParam("userId", 101)
    .queryParam("status", "completed")
.when()
    .get("/users/{userId}/orders")
.then()
    .statusCode(200);
```

Generated URL:

```text
/users/101/orders?status=completed
```

---

# Common Interview Questions

## Q1. What is a Path Parameter?

A Path Parameter is a value that forms part of the URL path and is generally used to identify a specific resource.

Example:

```text
/users/101
```

---

## Q2. What is a Query Parameter?

A Query Parameter is used to filter, search, sort, or paginate data.

Example:

```text
/users?page=2
```

---

## Q3. Which one is mandatory?

Usually:

* Path Parameter → Mandatory
* Query Parameter → Optional

---

## Q4. How do you pass Path Parameters in Rest Assured?

```java
given()
    .pathParam("id", 101)
.when()
    .get("/users/{id}");
```

---

## Q5. How do you pass Query Parameters in Rest Assured?

```java
given()
    .queryParam("page", 2)
.when()
    .get("/users");
```

---

# Interview Answer (Short Version)

**Path Parameter** is used to identify a specific resource and becomes part of the URL path.

Example:

```text
/users/101
```

**Query Parameter** is used for filtering, searching, sorting, or pagination and appears after the ? symbol.

Example:

```text
/users?page=2
```

In Rest Assured, we use:

```java
pathParam()
```

for Path Parameters and

```java
queryParam()
```

for Query Parameters.

---

# Summary

| Feature             | Path Parameter    | Query Parameter    |
| ------------------- | ----------------- | ------------------ |
| Location            | URL Path          | After ?            |
| Purpose             | Identify Resource | Filter/Search Data |
| Example             | /users/101        | /users?page=2      |
| Rest Assured Method | pathParam()       | queryParam()       |
| Mandatory           | Usually Yes       | Usually No         |

### Quick Rule

👉 If you are identifying **one specific resource**, use a **Path Parameter**.

👉 If you are filtering, searching, sorting, or paginating data, use a **Query Parameter**.
