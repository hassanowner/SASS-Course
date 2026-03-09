## What is Interpolation in Sass?

#### Definition and Basic Concept:

Interpolation is a feature in Sass that allows you to embed variables
and expressions inside strings, selectors, property names, and values. 
It's denoted by the #{} syntax.

#### Main Benefits:

· Create dynamic class names
· Use variables in property names
· Insert values into strings (like URLs)
· Build flexible and reusable code
· Generate multiple similar rules efficiently

#### How It Works:

When Sass encounters #{}, it evaluates the content inside the curly braces, converts it to a string, and inserts it into the surrounding text.

Basic Syntax:

```scss
// Variable inside a string
$name: "header";
.#{$name} { }  // Becomes: .header { }

// Variable inside a property name
$side: "left";
margin-#{$side}: 10px;  // Becomes: margin-left: 10px;
```

Simple Examples:

```scss
// Example 1: Basic interpolation in selectors
$size: "large";
.box-#{$size} {
  width: 200px;
}
// Compiles to: .box-large { width: 200px; }

// Example 2: Interpolation in property names
$position: "top";
padding-#{$position}: 20px;
// Compiles to: padding-top: 20px;

// Example 3: Interpolation in strings
$image: "logo";
background-image: url("images/#{$image}.png");
// Compiles to: background-image: url("images/logo.png");
```

---

## Second: Detailed Examples of Interpolation

### Example 1: Dynamic Class Names with Company Names

```scss
// Variables for different companies
$company: "microsoft";
$product: "windows";

// Creating a dynamic class for company products
.product-#{$company}-#{product} {
  font-family: Arial, sans-serif;
  border: 1px solid #ccc;
  padding: 20px;
  
  .#{$company}-logo {
    background-image: url("logos/#{$company}.svg");
    width: 100px;
    height: 50px;
  }
}

// This creates: .product-microsoft-windows { ... }
```

### Example 2: Dynamic Positioning System

```scss
// Variables for positioning
$position-type: "absolute";
$horizontal: "left";
$vertical: "top";
$distance: 20px;

.floating-element {
  position: #{$position-type};
  #{$horizontal}: $distance;
  #{$vertical}: $distance;
  
  // Dynamic corner name
  .corner-#{$horizontal}-#{$vertical} {
    content: "Element placed at #{$horizontal}:#{$vertical}";
  }
}

// Compiles to:
.floating-element {
  position: absolute;
  left: 20px;
  top: 20px;
}
.floating-element .corner-left-top {
  content: "Element placed at left:top";
}
```

### Example 3: Dynamic Icon System with URLs

```scss
// Variables for icon system
$icon-set: "social";
$icon-name: "facebook";
$icon-size: "32";

.social-link {
  display: inline-block;
  
  .icon-#{$icon-name} {
    width: #{$icon-size}px;
    height: #{$icon-size}px;
    background-image: url("icons/#{$icon-set}/#{$icon-name}.png");
    
    &:hover {
      background-image: url("icons/#{$icon-set}/#{$icon-name}-hover.png");
    }
  }
}
```

### Example 4: Using unique-id() for Unique Identifiers

```scss
// unique-id() generates a random unique ID each time you compile
$animation-id: unique-id();
$element-id: unique-id();

// Creates unique class names like .card-u12345abc
.card-#{$element-id} {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  
  &::before {
    content: "Card ID: #{$element-id}";
    font-size: 12px;
    color: #999;
  }
}

// Create unique animation names
@keyframes slide-#{$animation-id} {
  0% { transform: translateX(0); }
  100% { transform: translateX(100px); }
}

.animated-card {
  animation: slide-#{$animation-id} 0.5s ease;
}
```

---

### Third: Complete Practical Example - E-commerce Product Card System

Here's a complete, realistic example of an e-commerce product card system using interpolation:

```scss
// =========================================
// E-COMMERCE PRODUCT CARD SYSTEM
// =========================================

// Step 1: Define base placeholder for product cards
%product-card-base {
  border-radius: 12px;
  overflow: hidden;
  font-family: 'Arial', sans-serif;
  transition: transform 0.3s ease;
  
  &:hover {
    transform: translateY(-5px);
  }
}

// Step 2: Variables for dynamic content
$product-name: "wireless-headphones";
$brand: "sony";
$category: "electronics";
$discount: "20";
$in-stock: "true";
$position-badge: "top-right";

// Step 3: Main product card with dynamic class
.product-card-#{$product-name} {
  @extend %product-card-base;
  width: 300px;
  background-color: white;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  
  // Dynamic header with brand
  .card-header-#{$brand} {
    padding: 15px;
    background-color: #f8f8f8;
    border-bottom: 2px solid #e0e0e0;
    
    &::before {
      content: "#{$brand}";
      font-weight: bold;
      color: #0066cc;
    }
    
    &::after {
      content: " ★ #{$category}";
      font-size: 12px;
      color: #999;
      margin-left: 8px;
    }
  }
  
  // Product image with dynamic path
  .product-image {
    height: 200px;
    background-image: url("https://store.example.com/images/#{$category}/#{$brand}-#{$product-name}.jpg");
    background-size: cover;
    background-position: center;
    position: relative;
    
    // Dynamic discount badge
    @if $discount != "0" {
      .badge-#{$position-badge} {
        position: absolute;
        #{$position-badge}: 10px;
        background-color: #ff4444;
        color: white;
        padding: 5px 10px;
        border-radius: 20px;
        font-weight: bold;
        
        &::before {
          content: "#{$discount}% OFF";
        }
      }
    }
  }
  
  // Product details
  .product-details {
    padding: 20px;
    
    .product-title {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 10px;
      
      // Dynamic title with brand
      &::before {
        content: "#{$brand} ";
        color: #0066cc;
      }
      
      content: "#{$product-name}";
    }
    
    // Dynamic price section
    .price-section {
      margin-bottom: 15px;
      
      @if $discount != "0" {
        .original-price {
          text-decoration: line-through;
          color: #999;
          font-size: 14px;
          margin-right: 10px;
          
          &::before {
            content: "$199.99";
          }
        }
        
        .discounted-price {
          color: #ff4444;
          font-size: 24px;
          font-weight: bold;
          
          &::before {
            $original: 199.99;
            $discounted: $original - ($original * $discount / 100);
            content: "$$discounted";
          }
        }
      } @else {
        .price {
          color: #333;
          font-size: 24px;
          font-weight: bold;
          
          &::before {
            content: "$199.99";
          }
        }
      }
    }
    
    // Stock status with dynamic message
    .stock-status {
      padding: 10px;
      border-radius: 6px;
      margin-bottom: 15px;
      
      @if $in-stock == "true" {
        background-color: #e8f5e8;
        color: #2ecc71;
        
        &::before {
          content: "✓ In Stock";
          font-weight: bold;
        }
      } @else {
        background-color: #fff0f0;
        color: #ff4444;
        
        &::before {
          content: "✗ Out of Stock";
          font-weight: bold;
        }
      }
    }
    
    // Dynamic action buttons
    .action-buttons {
      display: flex;
      gap: 10px;
      
      $button-1: "add-to-cart";
      $button-2: "add-to-wishlist";
      
      .btn-#{$button-1} {
        flex: 2;
        padding: 12px;
        background-color: #0066cc;
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        
        &::before {
          content: "🛒 Add to Cart";
        }
        
        &:hover {
          background-color: darken(#0066cc, 10%);
        }
      }
      
      .btn-#{$button-2} {
        flex: 1;
        padding: 12px;
        background-color: #f0f0f0;
        color: #333;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        
        &::before {
          content: "Like";
        }
        
        &:hover {
          background-color: #e0e0e0;
        }
      }
    }
  }
}

// Step 4: Dynamic section for related products
$related-products: ("speakers", "earbuds", "headphone-stand");
$related-id: unique-id();

.related-products-#{$related-id} {
  margin-top: 40px;
  padding: 20px;
  
  .section-title {
    font-size: 22px;
    font-weight: bold;
    margin-bottom: 20px;
    
    &::before {
      content: "Related to #{brand} #{product-name}";
      color: #333;
    }
  }
  
  .related-grid {
    display: flex;
    gap: 20px;
    
    // Generate related product cards dynamically
    .related-#{nth($related-products, 1)} {
      @extend %product-card-base;
      width: 200px;
      padding: 15px;
      background: white;
      
      .image {
        height: 120px;
        background-image: url("images/related/#{nth($related-products, 1)}.jpg");
        background-size: cover;
      }
      
      .name {
        margin-top: 10px;
        font-weight: bold;
        content: "#{nth($related-products, 1)}";
      }
    }
    
    .related-#{nth($related-products, 2)} {
      @extend .related-speakers;
      .image {
        background-image: url("images/related/#{nth($related-products, 2)}.jpg");
      }
      .name {
        content: "#{nth($related-products, 2)}";
      }
    }
    
    .related-#{nth($related-products, 3)} {
      @extend .related-speakers;
      .image {
        background-image: url("images/related/#{nth($related-products, 3)}.jpg");
      }
      .name {
        content: "#{nth($related-products, 3)}";
      }
    }
  }
}

// Step 5: Dynamic footer with unique tracking ID
$tracking-id: unique-id();
$support-email: "support@store.com";

.footer-#{$tracking-id} {
  margin-top: 50px;
  padding: 30px;
  background-color: #333;
  color: white;
  
  .tracking-info {
    font-size: 14px;
    color: #999;
    
    &::before {
      content: "Your session ID: #{$tracking-id}";
    }
    
    &::after {
      content: " | Contact: #{$support-email}";
    }
  }
  
  .copyright {
    margin-top: 20px;
    font-size: 12px;
    color: #666;
    
    &::before {
      $year: 2024;
      content: "© #{$year} #{$brand} Store. All rights reserved.";
    }
  }
}
```

Compiled CSS Output (Partial):

```css
.product-card-wireless-headphones {
  border-radius: 12px;
  overflow: hidden;
  font-family: "Arial", sans-serif;
  transition: transform 0.3s ease;
  width: 300px;
  background-color: white;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}
.product-card-wireless-headphones:hover {
  transform: translateY(-5px);
}

.product-card-wireless-headphones .card-header-sony {
  padding: 15px;
  background-color: #f8f8f8;
  border-bottom: 2px solid #e0e0e0;
}
.product-card-wireless-headphones .card-header-sony::before {
  content: "sony";
  font-weight: bold;
  color: #0066cc;
}
.product-card-wireless-headphones .card-header-sony::after {
  content: " ★ electronics";
  font-size: 12px;
  color: #999;
  margin-left: 8px;
}

.product-card-wireless-headphones .product-image {
  height: 200px;
  background-image: url("https://store.example.com/images/electronics/sony-wireless-headphones.jpg");
  background-size: cover;
  background-position: center;
  position: relative;
}
.product-card-wireless-headphones .product-image .badge-top-right {
  position: absolute;
  top-right: 10px;
  background-color: #ff4444;
  color: white;
  padding: 5px 10px;
  border-radius: 20px;
  font-weight: bold;
}
.product-card-wireless-headphones .product-image .badge-top-right::before {
  content: "20% OFF";
}

.related-products-u123456 {
  margin-top: 40px;
  padding: 20px;
}
.related-products-u123456 .related-speakers,
.related-products-u123456 .related-earbuds,
.related-products-u123456 .related-headphone-stand {
  border-radius: 12px;
  overflow: hidden;
  font-family: "Arial", sans-serif;
  transition: transform 0.3s ease;
  width: 200px;
  padding: 15px;
  background: white;
}

.footer-u789abc {
  margin-top: 50px;
  padding: 30px;
  background-color: #333;
  color: white;
}
.footer-u789abc .tracking-info::before {
  content: "Your session ID: u789abc";
}
.footer-u789abc .tracking-info::after {
  content: " | Contact: support@store.com";
}
```

---

## Summary of Interpolation Uses

Use Case Example Result

Dynamic Class Names .card-#{$product} .card-headphones

Property Names #{$position}: 0; top: 0; or right: 0;

URL Building url("imgs/#{$brand}.png") url("imgs/sony.png")

Content Strings content: "#{$name}" content: "John"

Unique Identifiers id="tracking-#{unique-id()}" id="tracking-u12345"

### Key Points to Remember:

1. Syntax: Always use #{} with variables inside
2. Anywhere: Can be used in selectors, properties, strings, and values
3. Evaluation: Content inside #{} is evaluated before insertion
4. String Conversion: Everything becomes a string when interpolated
5. unique-id(): Generates a unique identifier each compilation
6. Combining: Can combine multiple variables in one interpolation

This comprehensive guide covers everything about Interpolation in Sass using only variables, @if, and @extend!
