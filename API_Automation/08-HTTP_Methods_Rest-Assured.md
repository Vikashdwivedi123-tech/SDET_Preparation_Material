# HTTP Methods in Rest Assured

## Introduction

HTTP (HyperText Transfer Protocol) methods define the type of action that a client wants to perform on a server.

In API Testing, understanding HTTP methods is crucial because every API endpoint is designed to perform specific operations such as creating, reading, updating, or deleting data.

Rest Assured provides built-in methods to send HTTP requests and validate responses.

---

# HTTP Methods Overview

| HTTP Method | Purpose                  | CRUD Operation |
| ----------- | ------------------------ | -------------- |
| GET         | Retrieve data            | Read           |
| POST        | Create new data          | Create         |
| PUT         | Update entire resource   | Update         |
| PATCH       | Update partial resource  | Update         |
| DELETE      | Remove resource          | Delete         |
| HEAD        | Retrieve headers only    | Read           |
| OPTIONS     | Get supported operations | Read           |
| TRACE       | Diagnostic request       | Debugging      |

---

# 1. GET Method

## What is GET?

The GET method is used to retrieve data from the server.

It should never modify existing data.

### Example

Suppose we want to retrieve user details.

```http
GET /users/1
```

### Rest Assured Example

```java
given()
.when()
    .get("https://reqres.in/api/users/2")
.then()
    .statusCode(200)
    .log().all();
```

### Expected Response

```json
{
  "data": {
    "id": 2,
    "first_name": "Janet",
    "last_name": "Weaver"
  }
}
```

### Interview Question

**Q: When do you use GET?**

Answer: Whenever data needs to be fetched without modifying server resources.

---

# 2. POST Method

## What is POST?

POST is used to create a new resource on the server.

### Example

Creating a new user.

```http
POST /users
```

### Request Body

```json
{
  "name":"Vikash",
  "job":"QA Engineer"
}
```

### Rest Assured Example

```java
given()
    .contentType("application/json")
    .body("""
    {
      "name":"Vikash",
      "job":"QA Engineer"
    }
    """)
.when()
    .post("https://reqres.in/api/users")
.then()
    .statusCode(201)
    .log().all();
```

### Typical Status Code

```text
201 Created
```

### Interview Question

**Q: What is the difference between GET and POST?**

GET retrieves data.

POST creates new data.

---

# 3. PUT Method

## What is PUT?

PUT is used to update an entire resource.

If some fields are not provided, they may be overwritten depending on API implementation.

### Example

```http
PUT /users/2
```

### Request Body

```json
{
  "name":"Vikash",
  "job":"Senior QA"
}
```

### Rest Assured Example

```java
given()
    .contentType("application/json")
    .body("""
    {
      "name":"Vikash",
      "job":"Senior QA"
    }
    """)
.when()
    .put("https://reqres.in/api/users/2")
.then()
    .statusCode(200)
    .log().all();
```

### Typical Status Code

```text
200 OK
```

### Interview Question

**Q: What is the difference between PUT and PATCH?**

PUT updates the entire resource.

PATCH updates only specified fields.

---

# 4. PATCH Method

## What is PATCH?

PATCH is used for partial updates.

Only the fields provided in the request are updated.

### Example

Update only job field.

```http
PATCH /users/2
```

### Request Body

```json
{
  "job":"Lead QA"
}
```

### Rest Assured Example

```java
given()
    .contentType("application/json")
    .body("""
    {
      "job":"Lead QA"
    }
    """)
.when()
    .patch("https://reqres.in/api/users/2")
.then()
    .statusCode(200)
    .log().all();
```

### Typical Status Code

```text
200 OK
```

### Real-World Example

Updating only:

* Mobile Number
* Address
* Email

without affecting other user details.

---

# 5. DELETE Method

## What is DELETE?

DELETE removes an existing resource from the server.

### Example

```http
DELETE /users/2
```

### Rest Assured Example

```java
given()
.when()
    .delete("https://reqres.in/api/users/2")
.then()
    .statusCode(204);
```

### Typical Status Code

```text
204 No Content
```

### Interview Question

**Q: Why does DELETE often return 204?**

Because the resource is deleted successfully and no response body is needed.

---

# 6. HEAD Method

## What is HEAD?

HEAD works like GET but returns only response headers.

No response body is returned.

### Why Use It?

* Verify resource existence.
* Validate content type.
* Check content length.
* Improve performance.

### Rest Assured Example

```java
given()
.when()
    .head("https://reqres.in/api/users/2")
.then()
    .statusCode(200);
```

### Example Headers

```text
Content-Type: application/json
Content-Length: 509
```

---

# 7. OPTIONS Method

## What is OPTIONS?

OPTIONS tells which HTTP methods are supported by an API endpoint.

### Example

```http
OPTIONS /users
```

### Rest Assured Example

```java
Response response =
given()
.when()
    .options("https://reqres.in/api/users");

System.out.println(
response.getHeader("Allow"));
```

### Example Response

```text
GET, POST, PUT, PATCH, DELETE
```

### Why Use It?

* API discovery
* Security testing
* Documentation validation

---

# 8. TRACE Method

## What is TRACE?

TRACE is used for debugging and diagnostics.

It returns the same request back to the client.

### Rest Assured Example

```java
given()
.when()
    .request("TRACE",
             "https://example.com");
```

### Why is TRACE Rarely Used?

Most servers disable TRACE due to security concerns.

### Typical Use Cases

* Network debugging
* Request diagnostics

---

# Common HTTP Status Codes

## 2xx Success

| Status Code | Meaning    |
| ----------- | ---------- |
| 200         | OK         |
| 201         | Created    |
| 202         | Accepted   |
| 204         | No Content |

---

## 4xx Client Errors

| Status Code | Meaning            |
| ----------- | ------------------ |
| 400         | Bad Request        |
| 401         | Unauthorized       |
| 403         | Forbidden          |
| 404         | Not Found          |
| 405         | Method Not Allowed |

---

## 5xx Server Errors

| Status Code | Meaning               |
| ----------- | --------------------- |
| 500         | Internal Server Error |
| 502         | Bad Gateway           |
| 503         | Service Unavailable   |

---

# Complete CRUD Example

## Create User

```java
Response response =
given()
    .contentType("application/json")
    .body("{\"name\":\"Vikash\"}")
.when()
    .post("/users");
```

---

## Get User

```java
given()
.when()
    .get("/users/1");
```

---

## Update User

```java
given()
    .body("{\"name\":\"Updated Vikash\"}")
.when()
    .put("/users/1");
```

---

## Delete User

```java
given()
.when()
    .delete("/users/1");
```

---

# Frequently Asked Interview Questions

### 1. Which HTTP methods are most commonly used in API Automation?

* GET
* POST
* PUT
* PATCH
* DELETE

---

### 2. What is the difference between PUT and PATCH?

PUT updates the entire resource.

PATCH updates only specified fields.

---

### 3. Which method should never modify data?

GET

---

### 4. Which status code is returned after successful resource creation?

201 Created

---

### 5. Which method is used to remove data?

DELETE

---

### 6. What is the purpose of the HEAD method?

To retrieve only response headers without the response body.

---

### 7. What is the purpose of OPTIONS?

To identify supported HTTP methods for an endpoint.

---

# Summary

HTTP methods are the foundation of API communication. As an Automation Engineer, you will primarily work with GET, POST, PUT, PATCH, and DELETE methods while automating CRUD operations. Understanding the purpose, behavior, and expected status codes of each method is essential for API testing using Rest Assured.
