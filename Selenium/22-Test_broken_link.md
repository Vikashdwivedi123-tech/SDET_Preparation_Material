# Broken Link Testing in Selenium

## What is a Broken Link?

A **broken link** is a hyperlink that does not lead to a valid webpage or resource.

When a user clicks a broken link, the server may return errors such as:

* 404 (Page Not Found)
* 500 (Internal Server Error)
* 403 (Forbidden)
* 400 (Bad Request)

Broken links negatively affect user experience and website quality.

---

## Why Selenium Alone Cannot Verify Broken Links

Selenium can locate and click links, but it cannot directly verify the HTTP response code.

To validate a link, we need to:

1. Extract the URL from the webpage.
2. Send an HTTP request to that URL.
3. Read the response code.
4. Determine whether the link is valid or broken.

This is commonly done using Java's `HttpURLConnection`.

---

## How Broken Link Testing Works

### Step 1: Find All Links

Locate all anchor (`<a>`) tags on the page.

```java
List<WebElement> links =
        driver.findElements(By.tagName("a"));
```

---

### Step 2: Get URL from href Attribute

```java
String url = link.getAttribute("href");
```

Example:

```html
<a href="https://example.com/contact">
    Contact Us
</a>
```

The value of `href` is the URL to validate.

---

### Step 3: Open HTTP Connection

```java
URL linkUrl = new URL(url);

HttpURLConnection connection =
        (HttpURLConnection)
        linkUrl.openConnection();
```

---

### Step 4: Connect to URL

```java
connection.connect();
```

---

### Step 5: Read Response Code

```java
int responseCode =
        connection.getResponseCode();
```

---

### Step 6: Validate Link

```java
if(responseCode >= 400)
{
    System.out.println("Broken Link");
}
else
{
    System.out.println("Valid Link");
}
```

---

## Understanding Response Codes

| Status Code | Meaning               |
| ----------- | --------------------- |
| 200         | OK                    |
| 301         | Moved Permanently     |
| 302         | Redirect              |
| 400         | Bad Request           |
| 403         | Forbidden             |
| 404         | Not Found             |
| 500         | Internal Server Error |

Generally:

```text
Response Code < 400  → Valid Link
Response Code >= 400 → Broken Link
```

---

## Complete Example

```java
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class BrokenLinkChecker {

    public static void main(String[] args) {

        WebDriver driver = new ChromeDriver();

        driver.get("https://example.com");

        List<WebElement> links =
                driver.findElements(By.tagName("a"));

        System.out.println("Total Links: "
                + links.size());

        for (WebElement link : links) {

            String url =
                    link.getAttribute("href");

            try {

                if (url == null || url.isEmpty()) {
                    continue;
                }

                URL linkUrl = new URL(url);

                HttpURLConnection connection =
                        (HttpURLConnection)
                        linkUrl.openConnection();

                connection.connect();

                int responseCode =
                        connection.getResponseCode();

                if (responseCode >= 400) {

                    System.out.println(
                            url + " --> Broken Link ("
                                    + responseCode + ")");

                } else {

                    System.out.println(
                            url + " --> Valid Link ("
                                    + responseCode + ")");
                }

            } catch (Exception e) {

                System.out.println(
                        url + " --> Error");
            }
        }

        driver.quit();
    }
}
```

---

## Checking a Single Link

If you only want to verify one link:

```java
String url =
        driver.findElement(
                By.linkText("Contact Us"))
                .getAttribute("href");

HttpURLConnection connection =
        (HttpURLConnection)
        new URL(url).openConnection();

connection.connect();

System.out.println(
        connection.getResponseCode());
```

---

## Common Issues During Broken Link Testing

### Null href Values

Some links may not contain an `href` attribute.

```java
if(url == null)
{
    continue;
}
```

---

### JavaScript Links

Some links use JavaScript instead of actual URLs.

```html
<a href="javascript:void(0)">
```

Such links should be skipped.

```java
if(url.startsWith("javascript"))
{
    continue;
}
```

---

### Redirect URLs

A response code like:

```text
301
302
```

usually indicates a redirect and should not be considered broken.

---

## Best Practices

1. Validate all links present on critical pages.
2. Ignore null and JavaScript-based links.
3. Treat response codes below 400 as valid.
4. Log broken links with their response codes.
5. Run broken-link validation regularly in regression testing.

---

## Common Classes Used

| Class               | Purpose                        |
| ------------------- | ------------------------------ |
| `WebDriver`         | Opens webpage                  |
| `WebElement`        | Represents links               |
| `URL`               | Creates URL object             |
| `HttpURLConnection` | Sends HTTP request             |
| `getResponseCode()` | Retrieves server response code |

---

## Summary

Broken Link Testing in Selenium involves collecting all webpage links, extracting their URLs, sending HTTP requests using `HttpURLConnection`, and checking the response codes. If the response code is 400 or greater, the link is generally considered broken. This helps ensure users do not encounter invalid or inaccessible pages.
