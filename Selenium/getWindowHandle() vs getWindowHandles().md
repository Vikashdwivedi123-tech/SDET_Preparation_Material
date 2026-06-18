# getWindowHandle() vs getWindowHandles()

## Difference

| Method | Returns | Use Case |
|---|---|---|
| `getWindowHandle()` | `String` — handle of the **current** window/tab | Store the parent/main window's ID before opening a new one |
| `getWindowHandles()` | `Set<String>` — handles of **all** open windows/tabs | Loop through all windows to find/switch to a specific one |

- `getWindowHandle()` only works on the window currently in focus — calling it after switching gives you the new window's handle, not the original.
- `getWindowHandles()` returns a `Set`, which is unordered in theory, but most browsers return handles in the order they were opened (don't rely on this for production logic — always identify windows by title/URL, not position).
- A handle is a unique alphanumeric string (e.g., `CDwindow-XXXX` or a UUID-like string) assigned by the browser to each window/tab — not the window title or URL.

## Switching to a New Window/Tab

```java
import org.openqa.selenium.WebDriver;
import java.util.Set;
import java.util.Iterator;

// 1. Store the handle of the main/parent window BEFORE the new window opens
String parentWindow = driver.getWindowHandle();

// 2. Perform the action that opens a new window/tab (e.g., click a link)
driver.findElement(By.linkText("Open New Window")).click();

// 3. Get handles of all open windows
Set<String> allWindows = driver.getWindowHandles();

// 4. Loop through and switch to the window that is NOT the parent
for (String windowHandle : allWindows) {
    if (!windowHandle.equals(parentWindow)) {
        driver.switchTo().window(windowHandle);
        break;
    }
}

// 5. Now perform actions on the new window
System.out.println("New window title: " + driver.getTitle());

// 6. Switch back to the original/parent window when done
driver.switchTo().window(parentWindow);
```

## Switching Between Multiple Windows (3+ tabs)

```java
String parentWindow = driver.getWindowHandle();
Set<String> allWindows = driver.getWindowHandles();

for (String handle : allWindows) {
    driver.switchTo().window(handle);
    String title = driver.getTitle();

    if (title.equals("Target Page Title")) {
        // do work on this specific window
        break;
    }
}

driver.switchTo().window(parentWindow); // return to original
```

## Closing Windows

```java
driver.close();  // closes only the CURRENT window (driver stays alive, must switch focus next)
driver.quit();   // closes ALL windows and ends the WebDriver session
```

## Common Mistake (interview trap)
Calling `driver.close()` on a child window leaves the driver focused on a closed window — always `switchTo().window(parentWindow)` immediately after closing a child window, or subsequent commands will throw `NoSuchWindowException`.

```java
driver.close();                          // closes child window
driver.switchTo().window(parentWindow);  // re-focus driver on a valid window
```
