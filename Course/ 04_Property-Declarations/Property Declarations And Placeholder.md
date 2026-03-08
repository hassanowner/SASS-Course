# What are Property Declarations and Placeholders in Sass?

Property Declarations (Nested Properties)

Definition:
Property declarations in Sass allow you to nest properties that share the same namespace. Instead of writing font-size, font-weight, font-family separately, you can nest them under font:.

#### Main Benefits:

· Organizes related properties together

· Reduces repetition of property prefixes

· Makes code more readable and maintainable

· Follows a logical hierarchy

#### How It Works:
When you write a property name followed by a colon and then a block { } instead of a value, Sass treats everything inside as nested properties. The parent property name becomes a prefix for all nested properties.

---

### First: Basic Example of Nested Properties

Example:

Sass Code:

```scss
.box {
  font-size: 20px;
  font: {
    size: 15px;
    weight: bold;
  }
  padding: 10px;
  margin: auto {
    top: 10px;
    bottom: 15px;
  }
}
```

Compiled to CSS:

```css
.box {
  font-size: 20px;
  font-size: 15px;
  font-weight: bold;
  padding: 10px;
  margin: auto;
  margin-top: 10px;
  margin-bottom: 15px;
}
```

#### Detailed Explanation:

1. Regular Property:

```scss
font-size: 20px;
// Normal CSS property
```

2. Nested Font Properties:

```scss
font: {
  size: 15px;
  weight: bold;
}
// Becomes:
// font-size: 15px;
// font-weight: bold;
// The parent "font:" becomes a prefix
```

3. Nested Margin with Base Value:

```scss
margin: auto {
  top: 10px;
  bottom: 15px;
}
// Becomes:
// margin: auto;
// margin-top: 10px;
// margin-bottom: 15px;
```

#### Important Notes About Nested Properties:

· The colon : after the parent property is required
· You can have a value on the parent property (like margin: auto)
· The parent property name acts as a prefix with a hyphen
· You can nest multiple levels deep

Another example:

```scss
.button {
  border: 1px solid black {
    left: none;
    right: 2px solid red;
  }
}
// Compiles to:
// border: 1px solid black;
// border-left: none;
// border-right: 2px solid red;
```

---

### Second: What are Placeholders?

Definition:
Placeholders (also called placeholder selectors) are special types of selectors in Sass that start with %. They are not compiled to CSS on their own. Instead, they are meant to be extended using @extend.

#### Main Benefits:

· Create reusable style blocks
· Reduce code duplication
· Keep your CSS DRY (Don't Repeat Yourself)
· No extra CSS generated unless extended

#### How It Works:
When you define a placeholder with %name { ... }, Sass stores these styles but doesn't output them. When you use @extend %name, Sass copies all the styles from the placeholder to the extending selector.

---

### Third: Defining a Placeholder

Example:

Sass Code:

```scss
%main-box {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
}
```

Compiled to CSS:

```css
/* Nothing! The placeholder itself doesn't generate any CSS */
```

#### Explanation:

· The % symbol defines a placeholder

· The name main-box is the placeholder name

· Contains reusable styles: white background, padding, border

· This code alone produces NO CSS output

· It's like a template waiting to be used

#### Key Characteristics of Placeholders:

1. No Output: Placeholders don't appear in CSS
2. Reusable: Can be extended by multiple selectors
3. DRY: Write once, use many times
4. Abstract: They're like abstract classes in programming

---

### Fourth: Using Placeholders with @extend

Example:

Sass Code:

```scss
%main-box {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
}

.ads {
  @extend %main-box;
  font-size: 20px;
  color: red;
}

.article {
  font-size: 22px;
  @extend %main-box;
  color: green;
}
```

Compiled to CSS:

```css
.ads, .article {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
}

.ads {
  font-size: 20px;
  color: red;
}

.article {
  font-size: 22px;
  color: green;
}
```

#### Detailed Explanation:

1. The Placeholder Definition:

```scss
%main-box {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
}
// Defines reusable styles but no CSS yet
```

2. First Extension:

```scss
.ads {
  @extend %main-box;
  font-size: 20px;
  color: red;
}
// .ads gets all %main-box styles plus its own
```

3. Second Extension:

```scss
.article {
  font-size: 22px;
  @extend %main-box;
  color: green;
}
// .article gets all %main-box styles plus its own
```

4. What @extend Does:

· Takes all styles from %main-box
· Applies them to both .ads and .article
· Groups selectors together that share the same styles
· Adds unique styles to each selector

#### How the CSS is Structured:

Grouped Common Styles:

```css
.ads, .article {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
}
// Both selectors share these styles
```

Individual Styles:

```css
.ads {
  font-size: 20px;
  color: red;
}

.article {
  font-size: 22px;
  color: green;
}
// Each has its own unique styles
```

---

### Comparison: Placeholders vs Regular Classes

Using Regular Class (Without Placeholder):

```scss
.main-box {
  background: white;
  padding: 15px;
  border: 1px solid #ccc;
}

.ads {
  @extend .main-box;  // Extending a regular class
  color: red;
}
// Problem: .main-box appears in CSS even if never used directly
```

Using Placeholder (Better):

```scss
%main-box {
  background: white;
  padding: 15px;
  border: 1px solid #ccc;
}

.ads {
  @extend %main-box;  // Extending a placeholder
  color: red;
}
// Benefit: No extra CSS unless extended
```

---

#### Advanced Example with Multiple Placeholders

Sass Code:

```scss
%shadow {
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

%rounded {
  border-radius: 5px;
}

%main-box {
  @extend %shadow;
  @extend %rounded;
  background: white;
  padding: 20px;
}

.card {
  @extend %main-box;
  color: blue;
}

.notice {
  @extend %main-box;
  @extend %shadow;
  background: yellow;
  color: black;
}
```

Compiled CSS:

```css
.notice, .card {
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.card, .notice {
  border-radius: 5px;
}

.card, .notice {
  background: white;
  padding: 20px;
}

.card {
  color: blue;
}

.notice {
  background: yellow;
  color: black;
}
```

---

### Summary of Key Points

#### Nested Properties:

Feature Description Example
Syntax Property: { nested: value; } font: { size: 16px; }
Result Property becomes prefix font-size: 16px;
Base Values Can have parent value margin: auto { top: 10px; }

##### Placeholders:

Feature Description Example
Definition %name { styles } %btn { padding: 10px; }
Usage @extend %name @extend %btn;
Output Only appears when extended No standalone CSS
Benefit No unused CSS Keeps CSS clean

#### Best Practices:

1. Use Placeholders for:
   · Repeating style patterns
   · Design system components
   · Base styles that multiple elements share
2. Don't Use Placeholders for:
   · Styles used only once
   · Very simple properties
   · When you need the class to exist in HTML
3. Naming Conventions:
   · Use descriptive names: %card, %btn-primary
   · Be consistent with your naming
   · Consider using prefixes: %ui-card, %theme-dark

This comprehensive guide covers everything about Property Declarations and Placeholders in Sass!
