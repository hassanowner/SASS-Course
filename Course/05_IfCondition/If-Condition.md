## What is Control Flow and If/Else in Sass?

#### Definition and Basic Concept:

Control Flow refers to the ability to execute different code based on certain conditions. Just like in programming languages, Sass allows you to make decisions in your styling using @if, @else if, and @else directives.

#### Main Benefits:

· Create dynamic styles based on conditions
· Generate different CSS for different scenarios
· Reduce code duplication
· Make your Sass smarter and more flexible

#### How It Works:
Sass evaluates a condition (something that returns true or false). If the condition is true, it executes the first block of code. If false, it can execute alternative blocks.

Basic Syntax:

```scss
@if condition {
  // Styles when condition is true
} @else {
  // Styles when condition is false
}
```

Simple One-Line Example:

```scss
// This shows the basic structure
$is_active: true;
@if $is_active { color: green; } @else { color: gray; }
```

---

## Second: Practical Real-World Example

Example with Theme Switching:

```scss
// Step 1: Create a variable to control the theme
// This variable determines which theme styles to apply
$theme: "dark";  // Can be "light" or "dark"

// Step 2: Use @if to check the theme value
// The @if directive evaluates the condition and applies appropriate styles
.page {
  @if $theme == "light" {
    // If $theme equals "light", these styles will be used
    background-color: white;     // Light background
    color: #444;                 // Dark text for contrast
    border: 1px solid #ddd;      // Light border
  } @else {
    // If $theme is anything else (like "dark"), these styles will be used
    background-color: #444;      // Dark background
    color: white;                // Light text for contrast
    border: 1px solid #666;      // Dark border
  }
}

// Step 3: Additional example with more conditions
// You can also use @else if for multiple conditions
.button {
  @if $theme == "light" {
    background: #f0f0f0;
    color: black;
  } @else if $theme == "dark" {
    background: #333;
    color: white;
  } @else {
    // Fallback/default styles
    background: gray;
    color: black;
  }
}
```

Compiled CSS (when $theme: "dark"):

```css
.page {
  background-color: #444;
  color: white;
  border: 1px solid #666;
}

.button {
  background: #333;
  color: white;
}
```

#### How This Works Step by Step:

1. Line 2: $theme: "dark"; - We set our theme variable to "dark"
2. Line 6: @if $theme == "light" - Sass checks if $theme equals "light"
3. Line 7-9: These styles are SKIPPED because condition is false
4. Line 11-14: These styles are EXECUTED because it's the @else block
5. Line 18-24: Similar check happens for the button styles

---

## Third: Using if() Function with Null

Example with Conditional Border Radius:

```scss
// Step 1: Define a placeholder for reusable box styles
// This will be extended by multiple elements
%main-box {
  padding: 20px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  // Notice: border-radius is NOT defined here
  // We'll add it conditionally later
}

// Step 2: Create a variable to control rounded corners
// Set to true if you want rounded corners, false for square corners
$rounded: false;  // Try changing to true to see the difference

// Step 3: Use the if() function to conditionally add border-radius
// The if() function is different from @if - it returns a value, not styles
.box {
  @extend %main-box;  // Get all base styles from placeholder
  
  // if($rounded, 6px, null) works like this:
  // - If $rounded is true → returns 6px
  // - If $rounded is false → returns null (which means no property)
  border-radius: if($rounded, 6px, null);
  
  // Additional box-specific styles
  font-size: 16px;
  color: #333;
}

// Step 4: Another example with multiple conditional properties
$shadow: true;
$border: false;

.card {
  @extend %main-box;
  
  // Adding properties conditionally using if()
  box-shadow: if($shadow, 0 2px 5px rgba(0,0,0,0.1), null);
  border: if($border, 2px solid blue, null);
  
  // You can also combine with @if for more complex logic
  @if $shadow {
    // Additional shadow effects when shadow is enabled
    transform: translateY(-2px);
  }
}
```

Compiled CSS (when $rounded: false):

```css
.box, .card {
  padding: 20px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
}

.box {
  font-size: 16px;
  color: #333;
  /* Note: No border-radius property appears because it was null */
}

.card {
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}
```

Compiled CSS (when $rounded: true):

```css
.box, .card {
  padding: 20px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
}

.box {
  border-radius: 6px;  /* Now appears because $rounded is true */
  font-size: 16px;
  color: #333;
}

.card {
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}
```

## Detailed Explanation of if() Function:

Syntax:

```scss
if(condition, value_if_true, value_if_false)
```

How it Works:

```scss
// Example 1: With true condition
$rounded: true;
border-radius: if($rounded, 6px, null);
// Result: border-radius: 6px;

// Example 2: With false condition  
$rounded: false;
border-radius: if($rounded, 6px, null);
// Result: No border-radius property at all

// Example 3: Using with different values
$theme: "dark";
text-color: if($theme == "dark", white, black);
// Result: text-color: white;

// Example 4: Multiple conditions
$size: large;
padding: if($size == large, 20px, 10px);
// Result: padding: 20px;
```

## Key Differences: @if vs if()

@if Directive if() Function

Controls entire blocks of code Returns a single value

Can contain multiple properties Used for one property value

Uses curly braces { } Uses parentheses ( )

Good for complex logic Good for simple conditional values

```scss
// @if - for multiple styles
@if $condition {
  property1: value1;
  property2: value2;
}

// if() - for single values
property: if($condition, value1, value2);
```

---

Complete Practical Example Combining Everything

```scss
// Variables to control the design
$dark-mode: false;
$rounded-corners: true;
$border-style: "solid";

// Base placeholder
%card-base {
  padding: 20px;
  margin: 10px;
  background: white;
}

// Main card component
.card {
  @extend %card-base;
  
  // Conditional border-radius
  border-radius: if($rounded-corners, 8px, null);
  
  // Conditional dark mode styles using @if
  @if $dark-mode {
    background: #222;
    color: white;
    border: 1px solid #444;
  } @else {
    background: white;
    color: #333;
    border: 1px solid #ddd;
  }
  
  // Conditional border style using if()
  border-style: if($border-style == "solid", solid, dashed);
  
  // More complex condition with multiple values
  padding: if($dark-mode, 25px, 20px);
  
  // Nested element with its own conditions
  &__title {
    font-size: if($dark-mode, 22px, 20px);
    color: if($dark-mode, #ff9900, #0066cc);
  }
}
```

## What Gets Compiled (with current variables):

```css
.card {
  padding: 20px;
  margin: 10px;
  border-radius: 8px;
  background: white;
  color: #333;
  border: 1px solid #ddd;
  border-style: solid;
  padding: 20px;
}

.card__title {
  font-size: 20px;
  color: #0066cc;
}
```

## Summary

Feature Purpose Syntax

@if Conditional code blocks @if condition { }

@else Alternative block @else { }

@else if Multiple conditions @else if condition { }

if() Conditional values if(condition, true, false)

#### Best Practices:

1. Use @if for multiple style declarations
2. Use if() for single property values
3. Keep conditions simple and readable
4. Comment your logic for clarity
5. Use meaningful variable names

This is how Control Flow with If/Else works in Sass!
