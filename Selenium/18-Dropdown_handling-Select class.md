# Select Class — Handling Dropdowns in Selenium

## What is the Select Class?
A wrapper class (`org.openqa.selenium.support.ui.Select`) for interacting with HTML `<select>` elements only. It does NOT work on custom dropdowns built with `<div>`/`<ul>`/`<li>` (common in React/Angular apps) — those are "dynamic dropdowns" and need a different approach (see below).

```java
WebElement dropdownElement = driver.findElement(By.id("country"));
Select select = new Select(dropdownElement);
```

## Static Dropdown (native `<select>` tag)

### Selecting a value (3 ways)
```java
select.selectByVisibleText("India");   // matches the visible text shown to the user
select.selectByValue("IN");            // matches the "value" attribute in HTML
select.selectByIndex(2);               // matches by position (0-based)
```

### Deselecting (only works on multi-select dropdowns)
```java
select.deselectByVisibleText("India");
select.deselectByValue("IN");
select.deselectByIndex(2);
select.deselectAll();
```

### Checking if multi-select
```java
boolean isMulti = select.isMultiple();  // true if <select multiple>
```

## Select Class — Key Methods

| Method | Returns | Purpose |
|---|---|---|
| `getOptions()` | `List<WebElement>` | All `<option>` elements in the dropdown |
| `getAllSelectedOptions()` | `List<WebElement>` | Currently selected option(s) — for multi-select |
| `getFirstSelectedOption()` | `WebElement` | The first/only selected option |
| `isMultiple()` | `boolean` | Whether dropdown allows multiple selections |

### getOptions() example — print all available options
```java
List<WebElement> options = select.getOptions();
for (WebElement option : options) {
    System.out.println(option.getText());
}
```

### getAllSelectedOptions() example — verify multi-select choices
```java
List<WebElement> selected = select.getAllSelectedOptions();
for (WebElement opt : selected) {
    System.out.println("Selected: " + opt.getText());
}
```

### getFirstSelectedOption() example — verify single-select value
```java
String currentValue = select.getFirstSelectedOption().getText();
System.out.println("Currently selected: " + currentValue);
```

### Select multiple options (multi-select dropdown)
```java
select.selectByVisibleText("Red");
select.selectByVisibleText("Blue");  // adds to selection, doesn't replace
```

## Dynamic Dropdown (custom-built, NOT a `<select>` tag)

The `Select` class won't work here — these are typically `<div>` containers that show/hide a `<ul>` of `<li>` items on click. Handle manually:

```java
// 1. Click to open the dropdown
driver.findElement(By.id("custom-dropdown")).click();

// 2. Wait for the options list to be visible
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.className("dropdown-options")));

// 3. Get all option elements and pick the one you want
List<WebElement> options = driver.findElements(By.cssSelector(".dropdown-options li"));
for (WebElement option : options) {
    if (option.getText().equals("India")) {
        option.click();
        break;
    }
}
```

### Dynamic dropdown via XPath text match (shortcut)
```java
driver.findElement(By.id("custom-dropdown")).click();
driver.findElement(By.xpath("//li[text()='India']")).click();
```

### Dynamic dropdown with search/filter input (e.g., autocomplete-style)
```java
driver.findElement(By.id("custom-dropdown")).click();
driver.findElement(By.cssSelector(".dropdown-search-input")).sendKeys("Ind");

wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//li[text()='India']")));
driver.findElement(By.xpath("//li[text()='India']")).click();
```

## Quick Decision Guide
- Inspect the HTML: real `<select>` tag → use `Select` class.
- `<div>`, `<ul>`/`<li>`, or framework-specific component (MUI, React-Select, Angular Material) → treat as dynamic, use click + locate + click pattern.

## Common Mistakes (interview traps)
- Trying to wrap a `Select` object around a non-`<select>` element — throws `UnexpectedTagNameException`.
- Calling `deselectByVisibleText()` on a single-select dropdown — throws `UnsupportedOperationException` (deselect only works on multi-select).
- Not waiting for dynamic dropdown options to render before searching for them — causes `NoSuchElementException` on slower-loading custom components.
- Using hardcoded index-based selection (`selectByIndex`) on dropdowns where the option order can change dynamically (e.g., populated from an API) — leads to flaky tests.
