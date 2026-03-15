
## What is For Loop in SCSS?

For Loop is a control structure in SCSS that repeats a block of code a specific number of times.
It helps you create multiple CSS classes with different values without writing them manually.

#### How it works:

· It runs code from a start number (from) to an end number

· There are two types: through (includes the last number) and to (excludes the last number)

· The variable $i changes its value in each loop

Simple Example:

```scss
@for $i from 1 through 3 {
  .box-#{$i} {
    width: 50px * $i;
  }
}
```

Result:

```css
.box-1 { width: 50px; }
.box-2 { width: 100px; }
.box-3 { width: 150px; }
```

---

## For Loop Examples

### Example 1: Simple - Basic Margin Classes

```scss
// Create margin classes from 0 to 20px
@for $i from 0 through 4 {
  .m-#{$i} {
    margin: $i * 5px;
  }
  
  .mt-#{$i} {
    margin-top: $i * 5px;
  }
  
  .mb-#{$i} {
    margin-bottom: $i * 5px;
  }
}
```

#### Explanation: This creates margin utility classes:

· .m-0 to .m-4 for all margins

· .mt-0 to .mt-4 for top margin

· .mb-0 to .mb-4 for bottom margin

  Each step increases by 5px.

---

### Example 2: Medium - Font Size System

```scss
// Create font sizes for text from small to large
$base-size: 12px;

@for $i from 1 through 6 {
  .text-size-#{$i} {
    font-size: $base-size + ($i * 2px);
    
    @if $i <= 3 {
      color: #333;  // darker for smaller text
      font-weight: normal;
    } @else {
      color: #666;  // lighter for larger text
      font-weight: bold;
    }
    
    line-height: 1.2 + ($i * 0.1);
  }
}
```

#### Explanation: This creates 6 text size classes:

· Size 1: 14px, dark color, normal weight

· Size 2: 16px, dark color, normal weight

· Size 3: 18px, dark color, normal weight

· Size 4: 20px, light color, bold

· Size 5: 22px, light color, bold

· Size 6: 24px, light color, bold

  Line height increases with font size.

---

### Example 3: Advanced - Progress Bar Generator

```scss
// Create progress bars with different percentages
$colors: (#ff0000, #ff9900, #00ff00, #0000ff);

@for $i from 1 through 10 {
  $percentage: $i * 10%;
  
  .progress-#{$percentage} {
    width: 100%;
    height: 30px;
    background-color: #f0f0f0;
    border-radius: 15px;
    position: relative;
    
    &::after {
      content: "#{$percentage} Complete";
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: $percentage;
      background-color: nth($colors, $i);
      border-radius: 15px;
      color: white;
      text-align: center;
      line-height: 30px;
      font-size: 14px;
    }
    
    @if $i <= 3 {
      &::after {
        background-color: #ff4444; // red for low progress
      }
    } @else if $i <= 6 {
      &::after {
        background-color: #ffaa44; // orange for medium progress
      }
    } @else {
      &::after {
        background-color: #44ff44; // green for high progress
      }
    }
  }
}

// Example with TO (excludes last number)
$steps: 1;
@for $i from 1 to 5 {
  .step-#{$steps} {
    padding: $i * 5px;
    border: 1px solid #ccc;
  }
  $steps: $steps + 1;
}
```

#### Explanation: This creates 10 progress bar classes:

1. 10% to 100% progress bars - each with a different color
2. Color changes based on progress level:

   · 10-30%: Red (low progress)
   
   · 40-60%: Orange (medium progress)
   
   · 70-100%: Green (high progress)
3. Text inside shows percentage complete
4. Second loop shows to - creates steps 1-4 only (excludes 5)

---

## Important Notes:

Through vs To

```scss
// Through - includes the last number
@for $i from 1 through 3 {
  .through-#{$i} { } // Creates: 1, 2, 3
}

// To - excludes the last number
@for $i from 1 to 3 {
  .to-#{$i} { } // Creates: 1, 2 only
}
```

Using Variables in For Loop

```scss
$start: 0;
$end: 5;
$increase: 10px;

@for $i from $start through $end {
  .space-#{$i} {
    margin: $i * $increase;
    
    @if $i == 0 {
      display: none;
    } @else if $i == 5 {
      display: block;
      background: yellow;
    }
  }
}
```

Practical Use Cases:

```scss
// Animation delays
@for $i from 1 through 5 {
  .delay-#{$i} {
    animation-delay: 0.2s * $i;
  }
}

// Z-index layers
@for $i from 1 through 10 {
  .layer-#{$i} {
    z-index: $i;
    position: relative;
  }
}

// Border radius sizes
@for $i from 1 through 4 {
  .rounded-#{$i} {
    border-radius: 4px * $i;
  }
}
```

The For loop in SCSS is very useful for creating repetitive CSS patterns, saving time,
and making your code more maintainable!
