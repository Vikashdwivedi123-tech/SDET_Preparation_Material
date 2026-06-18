# API Chaining in Rest Assured

## What is API Chaining?

API Chaining is a process where the response from one API request is used as input for another API request.

In real-world applications, APIs are often dependent on each other. For example:

1. Create a User
2. Get User Details using User ID
3. Update User using User ID
4. Delete User using User ID

The User ID generated from the Create User API is used in subsequent API calls.

---

## Why Do We Need API Chaining?

* To test complete business workflows.
* To validate data consistency across APIs.
* To simulate real user scenarios.
* To automate end-to-end API testing.

---

## API Chaining Workflow

```text
Create User API
       ↓
 Extract User ID
       ↓
Get User API
       ↓
Update User API
       ↓
Delete User API
```

---

## Ways to Perform API Chaining in Rest Assured

### 1. Using Path Parameters

```java
String userId = response.jsonPath().getString("id");

given()
    .pathParam("id", userId)
.when()
    .get("/users/{id}")
.then()
    .statusCode(200);
```

---

### 2. Using JSONPath

JSONPath is commonly used to extract values from API responses.

```java
Response response =
given()
    .contentType(ContentType.JSON)
    .body(payload)
.when()
    .post("/users");

String userId = response.jsonPath().getString("id");

System.out.println("User ID: " + userId);
```

---

### 3. Using Response Object

```java
Response response =
given()
.when()
    .get("/users/1");

String firstName =
response.jsonPath().getString("first_name");

System.out.println(firstName);
```

---

## Complete Example: API Chaining in Rest Assured

### Step 1: Create User

```java
Response createResponse =
given()
    .contentType(ContentType.JSON)
    .body("""
    {
        "name":"Vikash",
        "job":"QA Engineer"
    }
    """)
.when()
    .post("https://reqres.in/api/users");

createResponse.prettyPrint();

String userId =
createResponse.jsonPath().getString("id");

System.out.println("Created User ID: " + userId);
```

---

### Step 2: Get User Details

```java
given()
    .pathParam("id", userId)
.when()
    .get("https://reqres.in/api/users/{id}")
.then()
    .statusCode(200)
    .log().all();
```

---

### Step 3: Update User

```java
given()
    .contentType(ContentType.JSON)
    .pathParam("id", userId)
    .body("""
    {
        "name":"Vikash Updated",
        "job":"Senior QA Engineer"
    }
    """)
.when()
    .put("https://reqres.in/api/users/{id}")
.then()
    .statusCode(200)
    .log().all();
```

---

### Step 4: Delete User

```java
given()
    .pathParam("id", userId)
.when()
    .delete("https://reqres.in/api/users/{id}")
.then()
    .statusCode(204);
```

---

## API Chaining Using TestNG

```java
public class APIChainingTest {

    String userId;

    @Test(priority = 1)
    public void createUser() {

        Response response =
        given()
            .contentType(ContentType.JSON)
            .body("{\"name\":\"Vikash\",\"job\":\"QA\"}")
        .when()
            .post("/users");

        userId =
        response.jsonPath().getString("id");
    }

    @Test(priority = 2)
    public void getUser() {

        given()
            .pathParam("id", userId)
        .when()
            .get("/users/{id}")
        .then()
            .statusCode(200);
    }

    @Test(priority = 3)
    public void updateUser() {

        given()
            .pathParam("id", userId)
            .body("{\"job\":\"Senior QA\"}")
        .when()
            .put("/users/{id}")
        .then()
            .statusCode(200);
    }

    @Test(priority = 4)
    public void deleteUser() {

        given()
            .pathParam("id", userId)
        .when()
            .delete("/users/{id}")
        .then()
            .statusCode(204);
    }
}
```

---

## Best Practices for API Chaining

### ✅ Store Response Data Properly

Use variables, POJOs, or utility classes to store extracted values.

```java
String token =
response.jsonPath().getString("token");
```

### ✅ Validate Responses at Every Step

```java
.then()
.statusCode(200)
.body("name", equalTo("Vikash"));
```

### ✅ Avoid Hardcoding IDs

Bad:

```java
.get("/users/123")
```

Good:

```java
.get("/users/" + userId)
```

### ✅ Use Test Data Management

Create and clean test data automatically during execution.

---

## Common Interview Questions

### Q1. What is API Chaining?

API Chaining is a technique where data from one API response is used in another API request.

---

### Q2. Why is API Chaining important?

It helps validate end-to-end workflows and real-world business scenarios.

---

### Q3. How do you extract values from a response in Rest Assured?

Using JSONPath.

```java
String id =
response.jsonPath().getString("id");
```

---

### Q4. What are common use cases of API Chaining?

* User Creation → User Update
* Login → Get Token → Access Protected APIs
* Create Order → Fetch Order → Cancel Order
* Create Employee → Update Employee → Delete Employee

---

### Q5. Which methods are commonly used for API Chaining in Rest Assured?

* Response Object
* JSONPath
* Path Parameters
* TestNG Dependency
* POJO Classes

---

## Summary

API Chaining is one of the most important concepts in API Automation. It allows testers to create realistic end-to-end workflows by passing data from one API request to another. In Rest Assured, API Chaining is primarily achieved using Response objects, JSONPath extraction, and dynamic path/query parameters.
