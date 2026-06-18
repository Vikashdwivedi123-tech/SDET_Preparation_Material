# Selenium 3 vs Selenium 4 Architecture

## Selenium 3 Architecture

In Selenium 3, WebDriver commands do not directly communicate with the browser.

Communication happens through browser-specific drivers.

### Architecture

```text
Test Script
      ↓
Selenium Client Libraries
      ↓
JSON Wire Protocol
      ↓
Browser Driver
(ChromeDriver/GeckoDriver)
      ↓
Browser
```

### How It Works

1. Test script sends commands.
2. Commands are converted into JSON format.
3. JSON Wire Protocol sends requests to browser drivers.
4. Browser driver converts requests into browser-specific actions.
5. Browser executes the action and sends the response back.

### Drawbacks of Selenium 3

* Communication involved an extra translation layer.
* Slower execution.
* Different browsers implemented the protocol differently.
* Compatibility issues between browsers.

---

# Selenium 4 Architecture

Selenium 4 follows the W3C WebDriver Standard.

JSON Wire Protocol has been removed.

### Architecture

```text
Test Script
      ↓
Selenium Client Libraries
      ↓
W3C WebDriver Protocol
      ↓
Browser Driver
      ↓
Browser
```

### How It Works

1. Test script sends commands.
2. Commands follow the W3C WebDriver standard.
3. Browser driver directly understands the standard request.
4. Browser performs the action.
5. Response is returned.

### Benefits

* No protocol conversion.
* Faster communication.
* Better browser compatibility.
* Standardized behavior across browsers.

---

# Selenium 3 vs Selenium 4

| Selenium 3                            | Selenium 4                        |
| ------------------------------------- | --------------------------------- |
| Uses JSON Wire Protocol               | Uses W3C WebDriver Protocol       |
| Requires protocol conversion          | Direct standardized communication |
| Slower execution                      | Faster execution                  |
| Browser compatibility issues possible | Better browser compatibility      |
| Not fully standardized                | Fully W3C compliant               |
| Older architecture                    | Modern architecture               |

---

# Visual Difference

## Selenium 3

```text
Test Script
      ↓
JSON Wire Protocol
      ↓
ChromeDriver
      ↓
Chrome
```

Extra translation layer exists.

---

## Selenium 4

```text
Test Script
      ↓
W3C Protocol
      ↓
ChromeDriver
      ↓
Chrome
```

Direct standardized communication.

---

# Interview Questions

## Q1. What protocol was used in Selenium 3?

Answer:

```text
JSON Wire Protocol
```

---

## Q2. What protocol is used in Selenium 4?

Answer:

```text
W3C WebDriver Protocol
```

---

## Q3. Why is Selenium 4 faster than Selenium 3?

Because Selenium 4 removes the JSON Wire Protocol translation layer and uses direct W3C communication.

---

## Q4. What was the biggest architectural change in Selenium 4?

Replacement of JSON Wire Protocol with the W3C WebDriver Standard.

---

## Q5. What problem did Selenium 4 solve?

It solved browser compatibility and communication inconsistencies caused by JSON Wire Protocol.

---

# Interview Answer

**In Selenium 3, WebDriver commands were sent using JSON Wire Protocol, which required protocol conversion between Selenium and browser drivers. In Selenium 4, JSON Wire Protocol was removed and replaced with the W3C WebDriver Standard, allowing direct and standardized communication between Selenium and browsers. This makes Selenium 4 faster, more reliable, and more compatible across browsers.**
