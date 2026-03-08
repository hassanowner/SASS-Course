What is @use in Sass?

The @use rule is a modern way to load and organize Sass files.
It allows you to split your code into multiple small files (called partials)
and import them into a main file.

Main Benefits:

· Code Organization: Split your code into small, manageable files instead of one large file
· Reusability: Use the same code in multiple places
· Easy Maintenance: Find and modify code easily
· Clean Structure: Each file has its own purpose

Simple Example

Folder Structure:

```
project/
│
├── main.scss
│
└── sass/
    ├── layout/
    │   └── _global.scss
    │
    └── pages/
        └── _home.scss
```

1. File: sass/layout/_global.scss

```scss
* {
  margin: 0;
  padding: 0;
}

body {
  background: #f0f0f0;
  font-family: Arial, sans-serif;
}
```

2. File: sass/pages/_home.scss

```scss
.home {
  padding: 20px;
  
  h1 {
    color: blue;
    font-size: 24px;
  }
  
  p {
    color: gray;
  }
}
```

3. File: main.scss

```scss
// Import layout files
@use "sass/layout/global";

// Import page files
@use "sass/pages/home";
```


## How to Use @use Step by Step ##

Step 1: Create Partial Files

· Start filenames with underscore _ (example: _global.scss)
· These are called "partials"
· They won't be compiled to CSS on their own

Step 2: Write Your Code

Write normal SCSS code in each partial file:

```scss
// _header.scss
.header {
  background: black;
  color: white;
}
```

Step 3: Import in Main File

Use @use in your main file:

```scss
// main.scss
@use "sass/layout/header";
@use "sass/pages/home";
```

Step 4: Compile

Compile only the main file. All imported files will be combined automatically.


** What Happens When You Compile?
- When you compile main.scss, all imported files are combined into one CSS file:

Compiled CSS (main.css):

```css
* {
  margin: 0;
  padding: 0;
}

body {
  background: #f0f0f0;
  font-family: Arial, sans-serif;
}

.home {
  padding: 20px;
}
.home h1 {
  color: blue;
  font-size: 24px;
}
.home p {
  color: gray;
}
```



** Important Rules to Remember **

1. File Naming Convention

```scss
// ✓ Correct: Start with underscore
_global.scss
_header.scss
_footer.scss

// X Wrong: No underscore (will compile separately)
global.scss
```

2. Import Syntax

```scss
// ✓ Correct: No underscore, no extension
@use "sass/layout/global";

// X Wrong: Don't include _ or .scss
@use "sass/layout/_global.scss";
```

3. Path Writing

```scss
// Current folder
@use "header";

// Subfolders
@use "layout/header";
@use "pages/home";

// Parent folder (using ../)
@use "../abstracts/variables";
```

Common Folder Structure Examples

Simple Structure:

```
styles/
├── main.scss
├── _header.scss
├── _footer.scss
└── _buttons.scss
```

Organized Structure:

```
styles/
├── main.scss
│
├── layout/
│   ├── _header.scss
│   └── _footer.scss
│
└── components/
    ├── _buttons.scss
    └── _cards.scss
```

Complete Simple Example

All Files Together:

File: _reset.scss

```scss
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

File: _typography.scss

```scss
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

h1 {
  font-size: 32px;
}
```

File: _buttons.scss

```scss
.button {
  padding: 10px 20px;
  background: blue;
  color: white;
  border: none;
}
```

File: main.scss

```scss
@use "reset";
@use "typography";
@use "buttons";
```

Resulting CSS:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

h1 {
  font-size: 32px;
}

.button {
  padding: 10px 20px;
  background: blue;
  color: white;
  border: none;
}
```

Key Points Summary

1. Partial Files: Always start with underscore _
2. Import Without Extension: Don't write .scss or underscore in @use
3. One Main File: Compile only the main file that contains all @use rules
4. Organization: Group related styles in separate files
5. Clean Output: All files combine into one CSS file automatically

Common Mistakes to Avoid

```scss
// Don't do these:
@use "_header.scss";     // Wrong: includes underscore and extension
@use "header.scss";      // Wrong: includes extension
@use "sass/_header";     // Wrong: includes underscore

// Do this:
@use "header";           // Correct: simple name
@use "sass/layout/header"; // Correct: with folder path
```

This is the basic concept of @use in Sass.
It's simply a way to split your code into multiple files and combine them into one!
