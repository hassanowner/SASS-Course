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
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  } @else if $card-type == "featured" {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 25px;
    color: white;
    border-radius: 10px;
  } @else {
    @error "Unknown card type: '#{$card-type}'. Available types: 'basic', 'premium', 'featured'.";
  }
}
```

---

## Third: Advanced Button Style Example

#### Let's break down this button styling example step by step:

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
  transition: all 0.3s ease;
  
  // Control flow to determine button color scheme
  @if $button-type == "primary" {
    // Primary button - blue theme
    background-color: #007bff;
    color: white;
    box-shadow: 0 2px 4px rgba(0, 123, 255, 0.3);
    
    // Nested hover effect specific to primary
    &:hover {
      background-color: #0056b3;
      box-shadow: 0 4px 8px rgba(0, 123, 255, 0.4);
    }
    
  } @else if $button-type == "success" {
    // Success button - green theme
    background-color: #28a745;
    color: white;
    box-shadow: 0 2px 4px rgba(40, 167, 69, 0.3);
    
    &:hover {
      background-color: #1e7e34;
      box-shadow: 0 4px 8px rgba(40, 167, 69, 0.4);
    }
    
  } @else if $button-type == "danger" {
    // Danger button - red theme
    background-color: #dc3545;
    color: white;
    box-shadow: 0 2px 4px rgba(220, 53, 69, 0.3);
    
    &:hover {
      background-color: #bd2130;
      box-shadow: 0 4px 8px rgba(220, 53, 69, 0.4);
    }
    
  } @else if $button-type == "warning" {
    // Warning button - yellow theme
    background-color: #ffc107;
    color: #212529;
    box-shadow: 0 2px 4px rgba(255, 193, 7, 0.3);
    
    &:hover {
      background-color: #e0a800;
      box-shadow: 0 4px 8px rgba(255, 193, 7, 0.4);
    }
    
  } @else {
    // If button type is not one of the four valid values
    @error "This Button Type '#{$button-type}' Is Not Valid. Please use: primary, success, danger, or warning.";
    // Error message shows the invalid value and stops compilation
  }
  
  // Common styles for all button types
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

The Base Structure:

```scss
border: none;
border-radius: 4px;
cursor: pointer;
// These are common to all buttons
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
│   PRIMARY       │    │   SUCCESS       │    │    DANGER.      │   │     WARNING     │
│   (Blue)        │    │   (Green)       │    │    (Red)        │   │     (Yellow)    │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
      ↓ hover                ↓ hover                 ↓ hover               ↓ hover
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   Darker        │    │   Darker        │    │   Darker        │    │    Darker      │
│    Blue         │    │   Green         │    │    Red          │    │    Yellow      │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

#### How Each Button Type Affects the Styles:

1. Primary Button $button-type: "primary":

   · Background: Bright blue (#007bff)
   
   · Text: White
   
   · Shadow: Blue-tinted
   
   · Hover: Darker blue with stronger shadow
   
2. Success Button $button-type: "success":
   
   · Background: Green (#28a745)
   
   · Text: White
   
   · Shadow: Green-tinted
   
   · Hover: Darker green with stronger shadow
   
3. Danger Button $button-type: "danger":

   · Background: Red (#dc3545)
   
   · Text: White
   
   · Shadow: Red-tinted
   
   · Hover: Darker red with stronger shadow
   
4. Warning Button $button-type: "warning":
   
   · Background: Yellow (#ffc107)
   
   · Text: Dark gray (#212529)
   
   · Shadow: Yellow-tinted
   
   · Hover: Darker yellow with stronger shadow

#### What Happens When You Change the Variable:

When $button-type: "primary":

```css
.button {
  background-color: #007bff;
  color: white;
  box-shadow: 0 2px 4px rgba(0, 123, 255, 0.3);
}
.button:hover {
  background-color: #0056b3;
  box-shadow: 0 4px 8px rgba(0, 123, 255, 0.4);
}
```

When $button-type: "success":

```css
.button {
  background-color: #28a745;
  color: white;
  box-shadow: 0 2px 4px rgba(40, 167, 69, 0.3);
}
.button:hover {
  background-color: #1e7e34;
  box-shadow: 0 4px 8px rgba(40, 167, 69, 0.4);
}
```

When $button-type: "invalid":

```
Error: This Button Type 'invalid' Is Not Valid. Please use: primary, success, danger, or warning.
Compilation stops immediately with this helpful message.
```

Key Concepts Demonstrated:

1. @if / @else if chains for multiple options
2. Nested selectors (&:hover) within each condition
3. Common styles outside the conditional blocks
4. @error for invalid values
5. String interpolation #{$button-type} in error message
6. Different styling based on a single variable

This example shows how one variable can control an entire theme system!




---

## Fourth: More Examples with @error

### Example 4: Breakpoint Validation

```scss
// Create a responsive system with validation
$breakpoint: "mobile";  // Try: "mobile", "tablet", "desktop", "watch"

@mixin respond-to($size) {
  @if $size == "mobile" {
    @media (max-width: 767px) { @content; }
  } @else if $size == "tablet" {
    @media (min-width: 768px) and (max-width: 1023px) { @content; }
  } @else if $size == "desktop" {
    @media (min-width: 1024px) { @content; }
  } @else {
    @error "Breakpoint '#{$size}' is not defined. Use 'mobile', 'tablet', or 'desktop'.";
  }
}

.container {
  width: 100%;
  
  @include respond-to($breakpoint) {
    // This will only compile if $breakpoint is valid
    padding: 20px;
    background: lightblue;
  }
}
```

### Example 5: Number Validation with Ranges

```scss
// Validate column numbers in a grid system
$columns: 13;  // Try: 1-12 for valid, 13+ for error

@if $columns < 1 {
  @error "Columns cannot be less than 1. You specified: #{$columns}";
} @else if $columns > 12 {
  @error "Maximum columns is 12. You specified: #{$columns}";
} @else {
  .grid {
    display: grid;
    grid-template-columns: repeat($columns, 1fr);
  }
  
  @for $i from 1 through $columns {
    .col-#{$i} {
      grid-column: span $i;
    }
  }
}
```

### Example 6: Type Validation

```scss
// Check if a value is the correct type
$spacing: "20px";  // Try: 20px (number with unit), "20px" (string), 20 (number)

@if type-of($spacing) != "number" {
  @error "Spacing must be a number with units. Got: #{$spacing} (type: #{type-of($spacing)})";
} @else if unitless($spacing) {
  @error "Spacing must have units (px, em, rem). Got: #{$spacing}";
} @else {
  .box {
    margin: $spacing;
    padding: $spacing / 2;
  }
}
```

---

## Fifth: Best Practices with @error

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
  // styles
} @else if $theme == "dark" {
  // styles
} @else {
  @error "Theme '#{$theme}' doesn't exist. Available themes: 'light', 'dark'";
}
```

4. Use with Functions:

```scss
@function validate-padding($value) {
  @if $value < 0 {
    @error "Padding cannot be negative. Got: #{$value}";
  }
  @return $value;
}

.container {
  padding: validate-padding(20px);  // Works
  // padding: validate-padding(-5px);  // Error
}
```

---

## Summary Table

Directive Purpose Example

@if Check a condition @if $direction == "top"

@else if Check another condition @else if $direction == "right"

@else Default case @else { }

@error Stop with error message @error "Invalid value";

### Key Points:

1. @error stops compilation immediately
2. Always show what value caused the error
3. Tell users what values are acceptable
4. Use string interpolation #{$variable} to show values
5. Place @error in the @else block as a catch-all

This comprehensive guide covers everything about @error and control flow in Sass!
