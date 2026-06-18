# Authentication vs Authorization | 401 vs 403 Status Codes

## Introduction

Authentication and Authorization are two of the most important security concepts in API Testing and are frequently asked in SDET, QA Automation, and API interviews.

Many candidates confuse:

* Authentication vs Authorization
* 401 Unauthorized vs 403 Forbidden

This document explains these concepts in simple terms with real-world examples.

---

# Authentication vs Authorization

## Simple Rule

```text
Authentication = Who are you?

Authorization = What are you allowed to do?
```

---

# Real-Life Example

Imagine you are entering a company office.

### Step 1: Security Guard Checks Your ID Card

The guard verifies your identity.

```text
Authentication
```

Question:

```text
Who are you?
```

---

### Step 2: Access to Different Floors

After entering the office:

* Employee → Floor 1
* Manager → Floor 2
* Admin → All Floors

This is:

```text
Authorization
```

Question:

```text
What are you allowed to access?
```

---

# Authentication

## What is Authentication?

Authentication is the process of verifying a user's identity.

The system checks whether the user is genuine.

### Examples

* Username and Password
* JWT Token
* OAuth Token
* API Key
* Biometric Authentication

---

## API Example

Login Request

```http
POST /login
```

Request Body

```json
{
  "username":"vikash",
  "password":"password123"
}
```

Response

```json
{
  "token":"abc123xyz"
}
```

The server verifies:

```text
Is this user genuine?
```

If yes:

```text
Authentication Successful
```

---

# Authorization

## What is Authorization?

Authorization determines what actions a user can perform after successful authentication.

### Example

User Roles:

```text
Admin
Manager
Employee
Guest
```

---

### Permissions

| Role     | Create User | Delete User |
| -------- | ----------- | ----------- |
| Admin    | Yes         | Yes         |
| Manager  | Yes         | No          |
| Employee | No          | No          |

---

Server checks:

```text
Does this user have permission?
```

This process is called:

```text
Authorization
```

---

# Authentication Flow

```text
User Login
      ↓
Verify Identity
      ↓
Authentication Successful
      ↓
Generate Token
```

---

# Authorization Flow

```text
User Sends Token
      ↓
Server Validates Token
      ↓
Checks User Role
      ↓
Grant / Deny Access
```

---

# Authentication vs Authorization

| Authentication    | Authorization                |
| ----------------- | ---------------------------- |
| Verifies identity | Verifies permissions         |
| Who are you?      | What can you do?             |
| Happens first     | Happens after authentication |
| Uses credentials  | Uses roles/permissions       |
| Example: Login    | Example: Access Admin Panel  |

---

# What is 401 Unauthorized?

## Meaning

```text
Authentication Failed
```

The server could not verify who you are.

---

## Common Reasons

### Missing Token

```http
GET /users
```

No Authorization Header provided.

---

### Invalid Token

```http
Authorization: Bearer xyz123
```

Token is invalid.

---

### Expired Token

```text
Token expired
```

---

### Wrong Username/Password

```text
Invalid Credentials
```

---

# Example Response

```http
401 Unauthorized
```

```json
{
  "message":"Invalid token"
}
```

---

# Real-Life Example

Trying to enter an office without an ID card.

Security Guard says:

```text
I don't know who you are.
```

Result:

```text
401 Unauthorized
```

---

# What is 403 Forbidden?

## Meaning

```text
Authentication Successful
BUT
Authorization Failed
```

The server knows who you are but you don't have permission.

---

## Common Reasons

### User Role Restriction

User:

```text
Employee
```

Trying to access:

```text
Admin Dashboard
```

---

### Permission Missing

User logged in successfully but lacks required privileges.

---

# Example Response

```http
403 Forbidden
```

```json
{
  "message":"Access Denied"
}
```

---

# Real-Life Example

You entered the office successfully.

Security verified your ID.

Now you try to enter the CEO's cabin.

Security says:

```text
You are not allowed here.
```

Result:

```text
403 Forbidden
```

---

# Difference Between 401 and 403

| 401 Unauthorized                | 403 Forbidden            |
| ------------------------------- | ------------------------ |
| Authentication failed           | Authorization failed     |
| Server doesn't know who you are | Server knows who you are |
| Token missing/invalid           | Permission missing       |
| Login required                  | Login already successful |
| Identity issue                  | Access issue             |

---

# Interview Shortcut

## 401

```text
Who are you?
```

Server cannot verify your identity.

---

## 403

```text
I know who you are,
but you cannot access this resource.
```

---

# API Testing Scenarios

## Scenario 1

Request without token

```http
GET /users
```

Expected:

```text
401 Unauthorized
```

Reason:

```text
Authentication failed
```

---

## Scenario 2

Request with invalid token

```http
Authorization: Bearer invalidToken
```

Expected:

```text
401 Unauthorized
```

---

## Scenario 3

Employee trying to delete users

```http
DELETE /users/1
```

Expected:

```text
403 Forbidden
```

Reason:

```text
Insufficient permissions
```

---

## Scenario 4

Admin deleting users

```http
DELETE /users/1
```

Expected:

```text
200 OK
```

or

```text
204 No Content
```

---

# How to Validate in Rest Assured

## Verify 401 Unauthorized

```java
given()
.when()
    .get("/users")
.then()
    .statusCode(401);
```

---

## Verify 403 Forbidden

```java
given()
    .header("Authorization",
            "Bearer employeeToken")
.when()
    .delete("/users/1")
.then()
    .statusCode(403);
```

---

# Frequently Asked Interview Questions

## Q1. What is Authentication?

Authentication is the process of verifying the identity of a user.

---

## Q2. What is Authorization?

Authorization determines what actions a user can perform after authentication.

---

## Q3. What comes first?

```text
Authentication
       ↓
Authorization
```

---

## Q4. What does 401 mean?

Authentication failed.

The server cannot verify the user's identity.

---

## Q5. What does 403 mean?

Authentication succeeded but the user lacks permission to access the resource.

---

## Q6. Can a user get 403 without authentication?

Generally No.

The system must know who you are before checking permissions.

---

## Q7. Which status code is returned when a token is missing?

```text
401 Unauthorized
```

---

## Q8. Which status code is returned when a user lacks permission?

```text
403 Forbidden
```

---

# Quick Interview Answer

**Authentication** verifies a user's identity, while **Authorization** determines what resources that user can access.

**401 Unauthorized** means the server cannot authenticate the user because the credentials or token are missing, invalid, or expired.

**403 Forbidden** means the user is authenticated successfully, but does not have sufficient permissions to access the requested resource.

A simple way to remember:

```text
401 = Who are you?

403 = I know who you are,
      but you are not allowed.
```

---

# Summary

| Concept                 | Meaning                     |
| ----------------------- | --------------------------- |
| Authentication          | Verify Identity             |
| Authorization           | Verify Permissions          |
| 401 Unauthorized        | Authentication Failed       |
| 403 Forbidden           | Authorization Failed        |
| Authentication Question | Who are you?                |
| Authorization Question  | What are you allowed to do? |

### Golden Rule

```text
Authentication = Identity

Authorization = Permission

401 = Not Authenticated

403 = Authenticated but Not Authorized
```
