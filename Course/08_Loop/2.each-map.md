
## What is Each Loop in SCSS?

Each Loop is a control structure in SCSS that iterates through lists or maps.
It executes a block of code for each item in the list or map,
making it perfect for generating repetitive styles from collections of values.

#### How it works:

· Takes each item from a list or map one by one

· Assigns the item to a variable you specify

· Runs the code block using that variable

· Continues until all items are processed

#### Simple Example:

```scss
$colors: red, blue, green;

@each $color in $colors {
  .text-#{$color} {
    color: $color;
  }
}
```

Result:

```css
.text-red { color: red; }
.text-blue { color: blue; }
.text-green { color: green; }
```

#### Explanation:
The loop takes each color from the list, creates a class name using that color, and sets the text color to that color.

---

### Each Loop with Lists

#### Example 1: Simple - Button Sizes

```scss
$sizes: small, medium, large;

@each $size in $sizes {
  .btn-#{$size} {
    @if $size == small {
      padding: 5px 10px;
      font-size: 12px;
    } @else if $size == medium {
      padding: 10px 20px;
      font-size: 16px;
    } @else {
      padding: 15px 30px;
      font-size: 20px;
    }
    
    border-radius: 4px;
    border: none;
    cursor: pointer;
  }
}
```

#### Explanation: 
This creates three button size classes. For each size in the list, it sets different padding and font size values using conditions.

### Example 2: Medium - Card Themes

```scss
$themes: primary, secondary, success;

@each $theme in $themes {
  .card-#{$theme} {
    border: 2px solid;
    
    @if $theme == primary {
      border-color: #007bff;
      background-color: #e6f2ff;
    } @else if $theme == secondary {
      border-color: #6c757d;
      background-color: #f2f2f2;
    } @else {
      border-color: #28a745;
      background-color: #e6ffe6;
    }
    
    .card-header {
      padding: 15px;
      font-weight: bold;
      @if $theme == primary {
        background-color: #007bff;
        color: white;
      } @else if $theme == secondary {
        background-color: #6c757d;
        color: white;
      } @else {
        background-color: #28a745;
        color: white;
      }
    }
    
    .card-body {
      padding: 20px;
      color: #333;
    }
  }
}
```

#### Explanation: This creates three different card themes. Each theme has:

· Different border colors

· Different header colors

· Consistent structure but theme-specific styling

· Nested elements that inherit the theme context

---

## Each Loop with Key-Value Pairs (Maps)

#### What is Key-Value Each Loop?

This type of Each loop works with maps (collections of key-value pairs).
It allows you to access both the key name and its value in each iteration, 
making it perfect for creating related groups of styles.

#### How it works:

· The map contains pairs like key: value

· You specify two variables: one for key, One for value

· In each loop, key and value are assigned from one pair

· You can use both in your styles

#### Simple Example:

```scss
$colors: (
  "error": #ff4444,
  "warning": #ffaa44,
  "success": #44ff44
);

@each $name, $code in $colors {
  .alert-#{$name} {
    background-color: $code;
    border: 1px solid darken($code, 10%);
    color: white;
  }
}
```

#### Explanation: 
The loop takes each pair from the map. $name gets "error", "warning", "success" and $code gets their color values. Then creates alert classes with those colors.

---

## Key-Value Each Examples

### Example 1: Simple - Social Media Buttons

```scss
$social-colors: (
  "facebook": #3b5998,
  "twitter": #1da1f2,
  "instagram": #e1306c,
  "linkedin": #0077b5
);

@each $platform, $color in $social-colors {
  .btn-#{$platform} {
    background-color: $color;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    
    &:hover {
      background-color: darken($color, 10%);
      cursor: pointer;
    }
    
    &::before {
      content: "#{$platform}";
      margin-right: 5px;
    }
  }
}
```

#### Explanation: Creates social media buttons:

· Button class names match platform names

· Each button gets its brand color

· Hover effect darkens the color

· Pseudo-element shows platform name

### Example 2: Medium-Advanced - Dashboard Widgets

```scss
$widgets: (
  "stats": (
    bg: #2c3e50,
    text: white,
    icon: 📊,
    size: 300px
  ),
  "calendar": (
    bg: #3498db,
    text: white,
    icon: 📅,
    size: 400px
  ),
  "messages": (
    bg: #e74c3c,
    text: white,
    icon: ✉️,
    size: 350px
  ),
  "tasks": (
    bg: #27ae60,
    text: white,
    icon: ✓,
    size: 250px
  )
);

@each $widget-name, $widget-data in $widgets {
  .widget-#{$widget-name} {
    background-color: map-get($widget-data, bg);
    color: map-get($widget-data, text);
    width: map-get($widget-data, size);
    min-height: 200px;
    padding: 20px;
    border-radius: 10px;
    position: relative;
    
    &::before {
      content: map-get($widget-data, icon);
      font-size: 30px;
      position: absolute;
      top: 10px;
      right: 20px;
    }
    
    .widget-title {
      font-size: 24px;
      margin-bottom: 20px;
      border-bottom: 2px solid rgba(255,255,255,0.3);
      padding-bottom: 10px;
    }
    
    @if $widget-name == "stats" {
      .stat-number {
        font-size: 40px;
        font-weight: bold;
      }
    } @else if $widget-name == "calendar" {
      .date {
        background: rgba(255,255,255,0.2);
        padding: 5px;
        border-radius: 5px;
      }
    }
  }
}
```

#### Explanation: This creates 4 different dashboard widgets:

· Each widget has nested map data (background, text color, icon, size)

· Uses map-get() to access specific values

· Widgets have different sizes and icons

· Special styling for specific widgets using conditions

· Consistent structure but unique appearance per widget

---

## Multiple Values Each Loop

#### What is Multiple Values Each Loop?

This type of Each loop works with lists of lists where each inner list contains multiple values. You can assign each value to a separate variable, making it perfect for complex, related data.

#### How it works:

· You have a list containing multiple smaller lists

· Each smaller list has several values

· You specify multiple variables matching the number of values

· In each loop, variables get assigned from one inner list

#### Simple Example:

```scss
$buttons: 
  "primary" 16px blue,
  "secondary" 14px gray,
  "success" 16px green;

@each $type, $size, $color in $buttons {
  .btn-#{$type} {
    font-size: $size;
    background-color: $color;
    padding: $size/2 $size;
    color: white;
  }
}
```

#### Explanation: 
The loop takes each set of three values. $type gets the name, $size gets the font size, $color gets the color. Then creates buttons with these properties.

---

## Multiple Values Examples

### Example 1: Simple - Typography System

```scss
$text-styles:
  "h1" 32px bold #333,
  "h2" 28px bold #444,
  "h3" 24px bold #555,
  "body" 16px normal #666,
  "small" 12px normal #777;

@each $element, $size, $weight, $color in $text-styles {
  .text-#{$element} {
    font-size: $size;
    font-weight: $weight;
    color: $color;
    margin-bottom: $size/2;
    
    @if $weight == bold {
      text-transform: uppercase;
      letter-spacing: 1px;
    }
  }
}
```

#### Explanation: Creates a complete typography system:

· Five different text styles

· Each has element name, size, weight, and color

· Bold text gets additional styling

· Margin is calculated based on font size

### Example 2: Medium-Advanced - Product Card Generator

```scss
$products:
  "basic" 299.99 24px #3498db "Standard features included",
  "pro" 499.99 28px #e74c3c "All features + priority support",
  "enterprise" 999.99 32px #2c3e50 "Custom solutions + 24/7 support";

$features:
  "basic" "1 User" "5GB Storage" "Email Support",
  "pro" "5 Users" "50GB Storage" "Priority Support" "Analytics",
  "enterprise" "Unlimited Users" "500GB Storage" "Dedicated Support" "API Access" "Custom Integration";

@each $name, $price, $title-size, $accent, $description in $products {
  .card-#{$name} {
    border: 2px solid $accent;
    border-radius: 10px;
    padding: 20px;
    max-width: 300px;
    position: relative;
    overflow: hidden;
    
    &::before {
      content: "$#{$price}";
      position: absolute;
      top: 10px;
      right: 10px;
      background: $accent;
      color: white;
      padding: 5px 10px;
      border-radius: 5px;
      font-weight: bold;
    }
    
    .card-title {
      font-size: $title-size;
      color: $accent;
      margin-top: 30px;
      margin-bottom: 15px;
      text-transform: uppercase;
    }
    
    .card-description {
      color: #666;
      font-size: 14px;
      padding: 10px 0;
      border-bottom: 1px dashed #ccc;
    }
    
    .card-features {
      margin-top: 20px;
      
      @each $product, $feature1, $feature2, $feature3, $feature4 in $features {
        @if $product == $name {
          ul {
            list-style: none;
            padding: 0;
            
            li {
              padding: 8px;
              margin: 5px 0;
              background: lighten($accent, 45%);
              border-left: 3px solid $accent;
              
              @if $feature4 != "" {
                &:nth-child(4) {
                  background: $accent;
                  color: white;
                  font-weight: bold;
                }
              }
            }
          }
        }
      }
    }
    
    .card-button {
      display: block;
      background: $accent;
      color: white;
      text-align: center;
      padding: 12px;
      margin-top: 20px;
      text-decoration: none;
      border-radius: 5px;
      
      &:hover {
        background: darken($accent, 10%);
      }
    }
    
    @if $name == "enterprise" {
      box-shadow: 0 10px 20px rgba(0,0,0,0.2);
      transform: scale(1.05);
      z-index: 2;
    }
  }
}
```

#### Explanation: This advanced example creates three product cards:

1. First loop ($products): Contains main product data:
   - Product name, price, title size, accent color, description
   - Creates card structure with price badge
   - Sets card styling based on product
2. Second loop ($features): Contains features for each product:
   - Each product has 3-5 features
   - Nested loop matches features to current product
   - Special styling for premium features
3. Dynamic features display:
   - Different number of features per product
   - Special highlight for the last feature in Pro
   - Enterprise card gets extra styling (shadow, scale)
4. Smart conditions:
   - Enterprise card is highlighted as premium
   - Features list adapts to available data
   - Colors and styling consistent with product theme

---

## Summary Table

Type Syntax Use Case
Simple List @each $item in $list Single values, simple iterations
Key-Value @each $key, $value in $map Paired data like names and colors
Multiple Values @each $var1, $var2, $var3 in $list Complex data with multiple attributes

Each loop is powerful for generating repetitive, data-driven styles and maintaining consistency across your design system!
