## What is @error in Sass?

#### Definition and Basic Concept:

@error is a directive in Sass that allows you to display custom error messages when something goes wrong in your code. It stops the compilation process and shows your custom message to help developers understand what went wrong.

#### Main Benefits:

· Provides clear feedback when conditions aren't met

· Helps prevent invalid or unexpected values

· Makes debugging easier

· Improves code reliability

#### How It Works:

When Sass encounters @error, it immediately stops compiling and displays your custom message in the terminal/command line.

Basic Syntax:

```scss
@error "Your error message here";
// or with variables
@error "This value #{$variable} is not valid";
```

Simple Example:

```scss
$size: "huge";

@if $size == "small" {
  padding: 10px;
} @else if $size == "large" {
  padding: 20px;
} @else {
  @error "Size '#{$size}' is not valid. Use 'small' or 'large'.";
}
// This will stop compilation and show an error
```

---

## Second: Using @error with Different Examples

### Example 1: Color Validation

```scss
// Check if a color value is valid
$theme-color: "purple";  // Try changing to "red" or "blue"

.button {
  @if $theme-color == "red" {
    background-color: #ff0000;
    color: white;
  } @else if $theme-color == "blue" {
    background-color: #0000ff;
    color: white;
  } @else if $theme-color == "green" {
    background-color: #00ff00;
    color: black;
  } @else {
    // If none of the above match, show an error
    @error "Invalid color: '#{$theme-color}'. Please use 'red', 'blue', or 'green'.";
  }
}
```

#### What happens:

· If $theme-color is "purple", compilation stops

· Error message: Invalid color: 'purple'. Please use 'red', 'blue', or 'green'.

· Developer knows exactly what values are accepted

---

### Example 2: Font Size Validation

```scss
// Validate font sizes
$font-size: 25px;  // Try changing to 10px, 18px, or 30px

.heading {
  @if $font-size < 12px {
    @error "Font size #{$font-size} is too small. Minimum size is 12px.";
  } @else if $font-size > 24px {
    @error "Font size #{$font-size} is too large. Maximum size is 24px.";
  } @else {
    font-size: $font-size;
    font-weight: bold;
  }
}
```

#### What happens:

· With 25px: Error - too large

· With 10px: Error - too small

· With 18px: Works - font-size: 18px;

---

### Example 3: Multiple Conditions with Meaningful Errors

```scss
// Validate user input for a card component
$card-type: "featured";  // Try: "basic", "premium", "featured", or "gold"

.card {
  @if $card-type == "basic" {
    background: #f0f0f0;
    padding: 15px;
    border: 1px solid #ccc;
  } @else if $card-type == "premium" {
    background: #ffd700;
    padding: 20px;
    border: 2px solid gold;
  } @else if $card-type == "featured" {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 25px;
    color: white;
  } @else {
    @error "Unknown card type: '#{$card-type}'. Available types: 'basic', 'premium', 'featured'.";
  }
}
```

---

## Third: Advanced Button Style Example

Let's break down this button styling example step by step:

Full Code with Explanations:

```scss
// Variable controlling the button style
// Try changing this to: "primary", "success", "danger", "warning", or "invalid"
$button-type: "primary";

.button { 
  // Basic styling for the button
  font-size: 16px;
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  text-transform: uppercase;
  
  // Control flow to determine button color scheme
  @if $button-type == "primary" {
    // Primary button - blue theme
    background-color: #007bff;
    color: white;
    
    // Nested hover effect specific to primary
    &:hover {
      background-color: #0056b3;
    }
    
  } @else if $button-type == "success" {
    // Success button - green theme
    background-color: #28a745;
    color: white;
    
    &:hover {
      background-color: #1e7e34;
    }
    
  } @else if $button-type == "danger" {
    // Danger button - red theme
    background-color: #dc3545;
    color: white;
    
    &:hover {
      background-color: #bd2130;
    }
    
  } @else if $button-type == "warning" {
    // Warning button - yellow theme
    background-color: #ffc107;
    color: #212529;
    
    &:hover {
      background-color: #e0a800;
    }
    
  } @else {
    // If button type is not one of the four valid values
    @error "This Button Type '#{$button-type}' Is Not Valid. Please use: primary, success, danger, or warning.";
    // Error message shows the invalid value and stops compilation
  }
  
  // Common styles for all button types (applied to all buttons)
  &:active {
    transform: translateY(1px);
  }
  
  &:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }
}
```

#### How the Button System Works:

The Base Structure (common to all buttons):

```scss
border: none;
border-radius: 4px;
cursor: pointer;
font-weight: bold;
text-transform: uppercase;
// These are applied to every button regardless of type
```

#### Different Button Types Create Different Themes:

· Primary button: Blue theme → Used for main actions

· Success button: Green theme → Used for positive actions

· Danger button: Red theme → Used for destructive actions

· Warning button: Yellow theme → Used for cautionary actions

#### Visual Representation of Button Types:

```
Primary Button:     Success Button:     Danger Button:      Warning Button:
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   PRIMARY       │    │     SUCCESS     │    │     DANGER      │   │    WARNING      │
│   (Blue)        │    │     (Green)     │    │     (Red)       │   │    (Yellow)     │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
      ↓ hover                ↓ hover                ↓ hover                ↓ hover
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   Darker        │    │      Darker     │    │      Darker     │   │     Darker      │
│    Blue         │    │      Green      │    │       Red       │   │     Yellow      │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

#### How Each Button Type Affects the Styles:

1. Primary Button ($button-type: "primary"):
 
   · Background: Bright blue (#007bff)
   
   · Text: White
   
   · Hover: Darker blue (#0056b3)
   
2. Success Button ($button-type: "success"):

   · Background: Green (#28a745)
   
   · Text: White
   
   · Hover: Darker green (#1e7e34)
   
4. Danger Button ($button-type: "danger"):
   
   · Background: Red (#dc3545)
   
   · Text: White
   
   · Hover: Darker red (#bd2130)
   
6. Warning Button ($button-type: "warning"):

   · Background: Yellow (#ffc107)
   
   · Text: Dark gray (#212529)
   
   · Hover: Darker yellow (#e0a800)

#### What Happens When You Change the Variable:

When $button-type: "primary":

```css
.button {
  font-size: 16px;
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  text-transform: uppercase;
  background-color: #007bff;
  color: white;
}
.button:hover {
  background-color: #0056b3;
}
.button:active {
  transform: translateY(1px);
}
.button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
```

When $button-type: "success":

```css
.button {
  font-size: 16px;
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  text-transform: uppercase;
  background-color: #28a745;
  color: white;
}
.button:hover {
  background-color: #1e7e34;
}
/* active and disabled styles same as above */
```

When $button-type: "invalid":

```
Error: This Button Type 'invalid' Is Not Valid. Please use: primary, success, danger, or warning.
Compilation stops immediately with this helpful message.
```

### Key Concepts Demonstrated:

1. @if / @else if chains for multiple options
2. Nested selectors (&:hover) within each condition
3. Common styles outside the conditional blocks (applied to all buttons)
4. @error for invalid values
5. String interpolation #{$button-type} in error message
6. Different styling based on a single variable

This example shows how one variable can control an entire button theme system!

---

## Fourth: Best Practices with @error

1. Be Descriptive:

```scss
// Bad - Not helpful
@error "Wrong value";

// Good - Helpful and clear
@error "Invalid color value: '#{$color}'. Available colors: red, blue, green, yellow";
```

2. Include the Invalid Value:

```scss
// Always show what went wrong
$size: "xl";
@error "Size '#{$size}' is not recognized. Use 'sm', 'md', 'lg'.";
```

3. Suggest Valid Options:

```scss
// Help users fix the error
$theme: "dark";
@if $theme == "light" {
  background: white;
  color: black;
} @else if $theme == "dark" {
  background: black;
  color: white;
} @else {
  @error "Theme '#{$theme}' doesn't exist. Available themes: 'light', 'dark'";
}
```

---

## Summary Table

Directive Purpose Example
@if Check a condition @if $direction == "top"
@else if Check another condition @else if $direction == "right"
@else Default case @else { }
@error Stop with error message @error "Invalid value";

Key Points:

1. @error stops compilation immediately
2. Always show what value caused the error
3. Tell users what values are acceptable
4. Use string interpolation #{$variable} to show values
5. Place @error in the @else block as a catch-all for invalid values

This guide covers everything about @error and basic control flow (if/else) in Sass!
