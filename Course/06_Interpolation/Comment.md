## What are Comments in Sass?

#### Definition and Basic Concept:

Comments in Sass are notes or explanations written in the code that are ignored by the compiler. They help developers understand the code better and document the functionality.

#### Main Benefits:

· Document your code for yourself and others
· Explain complex logic or calculations
· Temporarily disable code during testing
· Generate documentation for functions and mixins

#### How It Works:

When Sass compiles your code, it processes comments differently based on how they are written. Some comments are removed completely, some remain in the CSS output, and some are used for documentation purposes.

---

## First: Single-Line Comments (//)

Syntax:

```scss
// This is a single-line comment
```

#### How It Works:

Single-line comments start with // and continue until the end of the line. These comments are completely removed during compilation and will NOT appear in the final CSS file.

Simple Examples:

```scss
// This is a comment about the code below
$primary-color: blue;

// Setting the main background color
body {
  background: white; // This is an inline comment
}

// This entire block is commented out during testing
// .temp-style {
//   display: none;
// }
```

Compiled CSS:

```css
body {
  background: white;
}
/* No comments appear in the CSS */
```

#### Key Points:

· Best for developer notes and explanations

· Safe for internal documentation

· Does not increase CSS file size

· Will not appear in generated CSS

---

## Second: Multi-Line Comments (/* */)

Syntax:

```scss
/* This is a multi-line comment
   that spans multiple lines */
```

#### How It Works:

Multi-line comments start with /* and end with */. These comments WILL appear in the compiled CSS file in normal mode, but will be removed in compressed mode.

Simple Examples:

```scss
/* Main Stylesheet
   Author: John Doe
   Version: 1.0 */

$padding: 20px;

.container {
  padding: $padding;
  /* This comment will appear in CSS */
  margin: 10px;
}

.box /* inline multi-line comment */ {
  width: 100px;
}
```

Compiled CSS (Normal Mode):

```css
/* Main Stylesheet
   Author: John Doe
   Version: 1.0 */
.container {
  padding: 20px;
  /* This comment will appear in CSS */
  margin: 10px;
}
.box {
  width: 100px;
}
```

Compiled CSS (Compressed Mode):

```css
.container{padding:20px;margin:10px}.box{width:100px}
/* All comments removed */
```

#### Key Points:

· Appears in normal CSS output

· Removed in compressed mode

· Good for copyright notices in development

· Not guaranteed to appear in production

---

## Third: Force Comments (/*! */)

Syntax:

```scss
/*! This comment will always appear */
```

#### How It Works:

Force comments start with /*! and end with */. These comments WILL appear in the compiled CSS file in ALL modes, including compressed mode. They are typically used for copyright notices and licenses.

Simple Examples:

```scss
/*! Copyright 2024 Company Name. All rights reserved. */

/*! This library is licensed under MIT */

.button {
  background: blue;
  /*! Critical: Do not remove this style */
  border-radius: 4px;
}
```

Compiled CSS (Any Mode, including compressed):

```css
/*! Copyright 2024 Company Name. All rights reserved. */
/*! This library is licensed under MIT */
.button {
  background: blue;
  /*! Critical: Do not remove this style */
  border-radius: 4px;
}
```

#### Key Points:

· Always appears in CSS output

· Preserved in compressed mode

· Perfect for copyright and licenses

· Important notices that must remain

---

## Fourth: Inline Comments with Code

Syntax:

```scss
.property: value; // inline comment
```

#### How It Works:

You can place single-line comments on the same line as code. Everything after // on that line is ignored by the compiler.

Simple Examples:

```scss
$spacing: 20px; // Default spacing unit

.card {
  padding: $spacing; // Apply default padding
  margin: 10px; // Temporary margin for testing
  // border: 1px solid red; // Disabled border
  color: black; // Text color
}
```

Compiled CSS:

```css
.card {
  padding: 20px;
  margin: 10px;
  color: black;
}
/* All inline comments removed */
```

#### Key Points:

· Great for explaining specific lines

· Useful for temporarily disabling properties

· Keeps documentation close to the code

· Removed from final CSS

---

## Fifth: Multi-Line Comments with Code

Syntax:

```scss
.selector /* comment */ {
  property: value; /* comment */
}
```

#### How It Works:

Multi-line comments can be placed anywhere in the code - between selectors, properties, or values. They follow the same rules as regular multi-line comments.

Simple Examples:

```scss
.navbar /* Main navigation bar */ {
  background: #333;
  padding: /* 15px */ 10px; /* Changed from 15px to 10px */
  
  /* This section handles mobile navigation */
  .mobile-menu {
    display: none;
  }
}

.item {
  width: 100px; /* Fixed width */
  height: 100px; /* Fixed height */
}
```

Compiled CSS:

```css
.navbar {
  background: #333;
  padding: 10px;
}
.navbar .mobile-menu {
  display: none;
}
.item {
  width: 100px;
  height: 100px;
}
/* Comments appear in normal mode */
```

---

## Sixth: Interpolation in Comments

Syntax:

```scss
/* This comment contains #{$variable} */
```

#### How It Works:

You can use interpolation #{} inside comments. The variable will be evaluated and its value will be inserted into the comment in the compiled CSS.

Simple Examples:

```scss
$company: "Acme Inc";
$version: "2.0.5";

/* Styles for #{$company} version #{$version} */

$primary-color: blue;
/* Primary color is now #{$primary-color} */

.button {
  background: $primary-color;
  /* This button uses #{$primary-color} background */
}
```

Compiled CSS:

```css
/* Styles for Acme Inc version 2.0.5 */

/* Primary color is now blue */

.button {
  background: blue;
  /* This button uses blue background */
}
```

#### Key Points:

· Variables are evaluated in comments

· Useful for dynamic documentation

· Shows actual values in generated CSS

· Works in all comment types

---

## Seventh: Documentation Comments (///)

Syntax:

```scss
/// This is a documentation comment
/// @param {type} $name - description
/// @return {type}
```

#### How It Works:

Triple-slash comments /// are special documentation comments used by SassDoc (a documentation generator). They don't appear in CSS but are used to generate API documentation for functions, mixins, and variables.

Simple Examples:

```scss
/// Primary color used throughout the theme
/// @type Color
$primary: #3498db;

/// Calculates the perfect padding based on base size
/// @param {Number} $base - The base size in pixels
/// @return {Number} The calculated padding
/// @example
///   padding: calculate-padding(16px);
@function calculate-padding($base) {
  @return $base * 1.5;
}

/// Creates a responsive container
/// @param {String} $size [medium] - Container size
/// @example scss
///   .wrapper {
///     @include container(large);
///   }
@mixin container($size: medium) {
  max-width: if($size == large, 1200px, 960px);
  margin: 0 auto;
}
```

Compiled CSS:

```css
/* No documentation comments appear in CSS */
/* Only the actual code compiles */

.container {
  max-width: 960px;
  margin: 0 auto;
}
```

#### Key Points:

· Used for documentation generation

· Follows specific syntax rules

· Helps create API documentation

· Never appears in compiled CSS

· Supports tags like @param, @return, @example

#### Common Documentation Tags:

\- Tag Purpose Example

@param Describe a parameter @param {Color} $color - The color value

@return Describe return value @return {Number} The calculated value

@example Show usage example @example scss .class { color: red; }

@type Describe variable type @type Color

@author Specify author @author John Doe

@since Version introduced @since 2.0.0

---

## Summary Table of Comment Types

Comment Type Syntax Appears in CSS Appears in Compressed Use Case

Single-line // text No No Internal notes

Multi-line /* text */ Yes No Development notes

Force /*! text */ Yes Yes Copyright, licenses

Inline code; // text No No Line explanations

Documentation /// text No No API documentation

### Best Practices:

1. Use // for internal developer notes
2. Use /* */ for notes that should appear in development CSS
3. Use /*! */ for copyright and license information
4. Use /// for documentation you want to generate
5. Be descriptive but concise
6. Update comments when code changes

This comprehensive guide covers everything about Comments in Sass!
