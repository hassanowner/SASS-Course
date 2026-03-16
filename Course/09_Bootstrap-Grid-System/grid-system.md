## Creating a Bootstrap Grid System in SCSS

#### What is a Grid System?

A grid system is a structure used in web design to organize and align content on a page. It divides the page into rows and columns, making it easier to create consistent, responsive layouts .

#### How it works:

· The page is divided into 12 columns (most common number)

· Columns can be combined to create wider content areas

· The system uses containers, rows, and columns to structure content 

· Each column has gutters (gaps) between them for spacing 

#### Basic Structure Example:

```html
<div class="container">
  <div class="row">
    <div class="col-6">Half width column</div>
    <div class="col-6">Half width column</div>
  </div>
</div>
```

#### Simple SCSS Example:

```scss
$total-columns: 12;

.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -15px;
}

@for $i from 1 through $total-columns {
  .col-#{$i} {
    width: percentage($i / $total-columns);
    padding: 0 15px;
  }
}
```

#### Explanation: This creates:

· A container that centers content and has max width

· Rows that use flexbox and negative margins to counter column padding

· Column classes from col-1 to col-12 with percentage-based widths 

---

## Main Example: Basic Column System

```scss
// Create simple column width classes
$grid-columns: 12;

@for $column from 1 through $grid-columns {
  .grid-#{$column} {
    width: ($column / $grid-columns) * 100%;
    float: left;
    min-height: 1px;
    padding: 0 10px;
  }
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

#### Result in CSS:

```css
.grid-1 { width: 8.33333%; float: left; min-height: 1px; padding: 0 10px; }
.grid-2 { width: 16.66667%; float: left; min-height: 1px; padding: 0 10px; }
.grid-3 { width: 25%; float: left; min-height: 1px; padding: 0 10px; }
.grid-4 { width: 33.33333%; float: left; min-height: 1px; padding: 0 10px; }
.grid-5 { width: 41.66667%; float: left; min-height: 1px; padding: 0 10px; }
.grid-6 { width: 50%; float: left; min-height: 1px; padding: 0 10px; }
.grid-7 { width: 58.33333%; float: left; min-height: 1px; padding: 0 10px; }
.grid-8 { width: 66.66667%; float: left; min-height: 1px; padding: 0 10px; }
.grid-9 { width: 75%; float: left; min-height: 1px; padding: 0 10px; }
.grid-10 { width: 83.33333%; float: left; min-height: 1px; padding: 0 10px; }
.grid-11 { width: 91.66667%; float: left; min-height: 1px; padding: 0 10px; }
.grid-12 { width: 100%; float: left; min-height: 1px; padding: 0 10px; }

.clearfix::after { content: ""; display: table; clear: both; }
```

#### Explanation: 
This loop creates 12 column width classes from 1 to 12.

Each column width is calculated as a percentage of the total (column number ÷ 12 × 100%) .

The clearfix class prevents container collapse with floated elements.

---

## Three Practical Grid System Examples

### Example 1: Simple - Basic Responsive Grid

```scss
// Simple responsive grid with breakpoints
$columns: 12;
$breakpoint-small: 576px;
$breakpoint-medium: 768px;
$breakpoint-large: 992px;

// Base mobile styles (stack vertically)
[class*="col-"] {
  width: 100%;
  padding: 0 15px;
  box-sizing: border-box;
}

// Create column classes for different breakpoints
@for $i from 1 through $columns {
  // Small screens
  @media (min-width: $breakpoint-small) {
    .col-sm-#{$i} {
      width: percentage($i / $columns);
      float: left;
    }
  }
  
  // Medium screens
  @media (min-width: $breakpoint-medium) {
    .col-md-#{$i} {
      width: percentage($i / $columns);
      float: left;
    }
  }
  
  // Large screens
  @media (min-width: $breakpoint-large) {
    .col-lg-#{$i} {
      width: percentage($i / $columns);
      float: left;
    }
  }
}

// Clearfix for rows
.row::after {
  content: "";
  display: table;
  clear: both;
}
```

#### Result in CSS (partial):

```css
[class*="col-"] { width: 100%; padding: 0 15px; box-sizing: border-box; }

@media (min-width: 576px) {
  .col-sm-1 { width: 8.33333%; float: left; }
  .col-sm-2 { width: 16.66667%; float: left; }
  .col-sm-3 { width: 25%; float: left; }
  .col-sm-4 { width: 33.33333%; float: left; }
  .col-sm-5 { width: 41.66667%; float: left; }
  .col-sm-6 { width: 50%; float: left; }
  .col-sm-7 { width: 58.33333%; float: left; }
  .col-sm-8 { width: 66.66667%; float: left; }
  .col-sm-9 { width: 75%; float: left; }
  .col-sm-10 { width: 83.33333%; float: left; }
  .col-sm-11 { width: 91.66667%; float: left; }
  .col-sm-12 { width: 100%; float: left; }
}

@media (min-width: 768px) {
  .col-md-1 { width: 8.33333%; float: left; }
  .col-md-2 { width: 16.66667%; float: left; }
  /* ... continues to col-md-12 */
}

@media (min-width: 992px) {
  .col-lg-1 { width: 8.33333%; float: left; }
  .col-lg-2 { width: 16.66667%; float: left; }
  /* ... continues to col-lg-12 */
}

.row::after { content: ""; display: table; clear: both; }
```

#### HTML Usage Example:

```html
<div class="row">
  <div class="col-sm-12 col-md-6 col-lg-4">Column 1</div>
  <div class="col-sm-12 col-md-6 col-lg-4">Column 2</div>
  <div class="col-sm-12 col-md-6 col-lg-4">Column 3</div>
</div>
```

#### Explanation: This grid has three breakpoints :

· Mobile (<576px): All columns stack vertically (100% width)

· Small (≥576px): Columns can be from 1-12 width

· Medium (≥768px): New set of classes for medium screens

· Large (≥992px): New set for large screens

---

### Example 2: Medium - Flexbox Grid with Offset Classes

```scss
// Flexbox-based grid system with offsets
$grid-columns: 12;
$gutter-width: 30px;

.container {
  max-width: 1140px;
  margin: 0 auto;
  padding: 0 $gutter-width / 2;
}

.container-fluid {
  width: 100%;
  padding: 0 $gutter-width / 2;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -$gutter-width / 2;
}

[class^="col-"] {
  padding: 0 $gutter-width / 2;
  box-sizing: border-box;
}

// Generate column classes
@for $i from 1 through $grid-columns {
  .col-#{$i} {
    flex: 0 0 percentage($i / $grid-columns);
    max-width: percentage($i / $grid-columns);
  }
}

// Generate offset classes
@for $i from 0 through $grid-columns - 1 {
  .offset-#{$i} {
    margin-left: percentage($i / $grid-columns);
  }
}

// Auto-layout columns
.col-auto {
  flex: 0 0 auto;
  width: auto;
  max-width: 100%;
}

// Equal width columns
.col {
  flex: 1 0 0%;
  max-width: 100%;
}
```

#### Result in CSS (partial):

```css
.container { max-width: 1140px; margin: 0 auto; padding: 0 15px; }
.container-fluid { width: 100%; padding: 0 15px; }
.row { display: flex; flex-wrap: wrap; margin: 0 -15px; }
[class^="col-"] { padding: 0 15px; box-sizing: border-box; }

.col-1 { flex: 0 0 8.33333%; max-width: 8.33333%; }
.col-2 { flex: 0 0 16.66667%; max-width: 16.66667%; }
.col-3 { flex: 0 0 25%; max-width: 25%; }
.col-4 { flex: 0 0 33.33333%; max-width: 33.33333%; }
/* ... continues to col-12 */

.offset-0 { margin-left: 0%; }
.offset-1 { margin-left: 8.33333%; }
.offset-2 { margin-left: 16.66667%; }
.offset-3 { margin-left: 25%; }
/* ... continues to offset-11 */

.col-auto { flex: 0 0 auto; width: auto; max-width: 100%; }
.col { flex: 1 0 0%; max-width: 100%; }
```

#### HTML Usage Example:

```html
<div class="container">
  <!-- Equal width columns -->
  <div class="row">
    <div class="col">Auto equal width</div>
    <div class="col">Auto equal width</div>
    <div class="col">Auto equal width</div>
  </div>
  
  <!-- Specific widths with offset -->
  <div class="row">
    <div class="col-4">Width 4 columns</div>
    <div class="col-6 offset-2">Width 6 columns, offset by 2</div>
  </div>
  
  <!-- Mixed column types -->
  <div class="row">
    <div class="col-auto">Auto width based on content</div>
    <div class="col-8">Fixed width 8 columns</div>
  </div>
</div>
```

#### Explanation: This flexbox grid includes :

· Flexbox layout: More powerful than floats

· Offset classes: Push columns to the right (margin-left)

· Auto columns: Width based on content

· Equal width columns: All columns share available space equally

---

### Example 3: Advanced - Complete Bootstrap-like Grid System

```scss
// Complete grid system with mixins, breakpoints, and utilities
$grid-columns: 12 !default;
$grid-gutter-width: 30px !default;

$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px
) !default;

$container-max-widths: (
  sm: 540px,
  md: 720px,
  lg: 960px,
  xl: 1140px,
  xxl: 1320px
) !default;

// Mixins
@mixin make-container() {
  width: 100%;
  padding-right: $grid-gutter-width / 2;
  padding-left: $grid-gutter-width / 2;
  margin-right: auto;
  margin-left: auto;
}

@mixin make-row() {
  display: flex;
  flex-wrap: wrap;
  margin-right: -$grid-gutter-width / 2;
  margin-left: -$grid-gutter-width / 2;
}

@mixin make-col-ready() {
  position: relative;
  width: 100%;
  padding-right: $grid-gutter-width / 2;
  padding-left: $grid-gutter-width / 2;
}

@mixin make-col($size, $columns: $grid-columns) {
  flex: 0 0 percentage($size / $columns);
  max-width: percentage($size / $columns);
}

// Container classes
.container {
  @include make-container();
}

.container-fluid {
  @include make-container();
}

// Responsive containers
@each $breakpoint, $max-width in $container-max-widths {
  $infix: -#{$breakpoint};
  
  @media (min-width: map-get($grid-breakpoints, $breakpoint)) {
    .container#{$infix} {
      @include make-container();
      max-width: $max-width;
    }
  }
}

// Row class
.row {
  @include make-row();
}

// Column ready class
[class*="col-"] {
  @include make-col-ready();
}

// Generate grid classes for each breakpoint
@each $breakpoint, $min-width in $grid-breakpoints {
  $infix: -#{$breakpoint};
  
  @if $min-width == 0 {
    $infix: "";
  }
  
  @media (min-width: $min-width) {
    // Column classes
    @for $i from 1 through $grid-columns {
      .col#{$infix}-#{$i} {
        @include make-col($i, $grid-columns);
      }
    }
    
    // Auto column
    .col#{$infix}-auto {
      flex: 0 0 auto;
      width: auto;
      max-width: 100%;
    }
    
    // Equal width column
    .col#{$infix} {
      flex: 1 0 0%;
      max-width: 100%;
    }
    
    // Offset classes
    @for $i from 0 through $grid-columns - 1 {
      .offset#{$infix}-#{$i} {
        margin-left: percentage($i / $grid-columns);
      }
    }
    
    // Order classes
    @for $i from 1 through $grid-columns {
      .order#{$infix}-#{$i} {
        order: $i;
      }
    }
    
    .order#{$infix}-first { order: -1; }
    .order#{$infix}-last { order: $grid-columns + 1; }
  }
}

// Gutter utilities
.g-0, .gx-0 {
  --gutter-x: 0;
}

.g-0, .gy-0 {
  --gutter-y: 0;
}

.g-1, .gx-1 {
  --gutter-x: 10px;
}

// Row with gutters
.row {
  --gutter-x: #{$grid-gutter-width};
  --gutter-y: 0;
  
  margin-right: calc(-.5 * var(--gutter-x));
  margin-left: calc(-.5 * var(--gutter-x));
  margin-top: calc(-1 * var(--gutter-y));
  
  > * {
    padding-right: calc(var(--gutter-x) * .5);
    padding-left: calc(var(--gutter-x) * .5);
    margin-top: var(--gutter-y);
  }
}

// Column alignment
.align-items-start { align-items: flex-start; }
.align-items-center { align-items: center; }
.align-items-end { align-items: flex-end; }

.justify-content-start { justify-content: flex-start; }
.justify-content-center { justify-content: center; }
.justify-content-end { justify-content: flex-end; }
.justify-content-between { justify-content: space-between; }
```

#### Result in CSS (abbreviated sample):

```css
.container, .container-fluid, .container-sm, .container-md, .container-lg, .container-xl, .container-xxl {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

@media (min-width: 576px) {
  .container, .container-sm { max-width: 540px; }
}

@media (min-width: 768px) {
  .container, .container-sm, .container-md { max-width: 720px; }
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
  --gutter-x: 30px;
  --gutter-y: 0;
  margin-right: calc(-.5 * var(--gutter-x));
  margin-left: calc(-.5 * var(--gutter-x));
  margin-top: calc(-1 * var(--gutter-y));
}

[class*="col-"] {
  position: relative;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
}

@media (min-width: 576px) {
  .col-sm-1 { flex: 0 0 8.33333%; max-width: 8.33333%; }
  .col-sm-2 { flex: 0 0 16.66667%; max-width: 16.66667%; }
  .col-sm-3 { flex: 0 0 25%; max-width: 25%; }
  .col-sm-4 { flex: 0 0 33.33333%; max-width: 33.33333%; }
  .col-sm-5 { flex: 0 0 41.66667%; max-width: 41.66667%; }
  .col-sm-6 { flex: 0 0 50%; max-width: 50%; }
  .col-sm-7 { flex: 0 0 58.33333%; max-width: 58.33333%; }
  .col-sm-8 { flex: 0 0 66.66667%; max-width: 66.66667%; }
  .col-sm-9 { flex: 0 0 75%; max-width: 75%; }
  .col-sm-10 { flex: 0 0 83.33333%; max-width: 83.33333%; }
  .col-sm-11 { flex: 0 0 91.66667%; max-width: 91.66667%; }
  .col-sm-12 { flex: 0 0 100%; max-width: 100%; }
  .col-sm-auto { flex: 0 0 auto; width: auto; max-width: 100%; }
  .col-sm { flex: 1 0 0%; max-width: 100%; }
  .offset-sm-0 { margin-left: 0%; }
  .offset-sm-1 { margin-left: 8.33333%; }
  .offset-sm-2 { margin-left: 16.66667%; }
  /* ... continues */
}

@media (min-width: 768px) {
  .col-md-1 { flex: 0 0 8.33333%; max-width: 8.33333%; }
  /* ... similar pattern for md breakpoint */
}

/* Continue for lg, xl, xxl breakpoints */

.align-items-start { align-items: flex-start; }
.align-items-center { align-items: center; }
.align-items-end { align-items: flex-end; }
.justify-content-start { justify-content: flex-start; }
.justify-content-center { justify-content: center; }
.justify-content-end { justify-content: flex-end; }
.justify-content-between { justify-content: space-between; }
```

#### HTML Usage Example:

```html
<!-- Responsive grid with different behaviors at breakpoints -->
<div class="container">
  <!-- Three columns that stack on mobile, equal width on tablet -->
  <div class="row">
    <div class="col-12 col-md-4">Column 1</div>
    <div class="col-12 col-md-4">Column 2</div>
    <div class="col-12 col-md-4">Column 3</div>
  </div>
  
  <!-- Offset example -->
  <div class="row">
    <div class="col-md-4">Normal column</div>
    <div class="col-md-4 offset-md-4">Offset by 4 columns</div>
  </div>
  
  <!-- Order example -->
  <div class="row">
    <div class="col order-md-3">First in mobile, last in desktop</div>
    <div class="col order-md-1">Second in mobile, first in desktop</div>
    <div class="col order-md-2">Third in mobile, second in desktop</div>
  </div>
  
  <!-- Gutters example -->
  <div class="row g-1">
    <div class="col-6">Small gutters</div>
    <div class="col-6">Small gutters</div>
  </div>
  
  <!-- Alignment example -->
  <div class="row align-items-center" style="height: 200px;">
    <div class="col-6">Vertically centered</div>
    <div class="col-6">Vertically centered</div>
  </div>
</div>
```

#### Explanation: This advanced grid system includes :

1. Configurable variables: Columns, gutter width, breakpoints, container widths
2. Mixins: Reusable code for containers, rows, and columns
3. Multiple breakpoints: xs, sm, md, lg, xl, xxl with responsive infixes
4. Container types: Fixed containers per breakpoint and fluid containers
5. Column utilities: Auto columns, equal width, specific widths
6. Offset classes: Push columns to the right at different breakpoints
7. Order classes: Change visual order independently of HTML
8. Gutter utilities: Control spacing between columns
9. Alignment utilities: Flexbox alignment (vertical and horizontal)

---

### Key Components of a Grid System 

Component Purpose CSS Properties

Container Wraps the grid, centers content max-width, margin: 0 auto, padding

Row Wraps columns, negative margins display: flex, flex-wrap: wrap, negative margins

Column Content containers, width control flex: 0 0 X%, padding for gutters

Gutter Space between columns padding on columns, negative margin on rows

Breakpoint Responsive behavior changes Media queries with min-width

The beauty of building your own grid system with SCSS is complete control over every aspect while writing minimal code through loops and mixins!
