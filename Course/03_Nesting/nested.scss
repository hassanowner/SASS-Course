
## What is Nesting in Sass?

Definition of Nesting:

- Nesting is a feature in Sass that allows you to write CSS in a hierarchical structure
that mirrors your HTML structure. Instead of repeating selector names over and over, 
you can nest them inside each other.

Main Benefits:

· Write more organized and readable code
· Reduce repetition in writing selectors
· Naturally reflects HTML structure
· Easy maintenance and modification

### How It Works:

When you write a selector inside another selector, Sass combines them 
(adding a space between them) when compiling to regular CSS.

---

** First: Basic Nesting

Example:

Sass Code:

```scss
parent {
  font-weight: bold;
  
  .child {
    font-size: 20px;
    
    .grand-child {
      font-size: 15px;
    }
  }
}
```

Compiled to CSS:

```css
parent {
  font-weight: bold;
}

parent .child {
  font-size: 20px;
}

parent .child .grand-child {
  font-size: 15px;
}
```

Explanation:

· The selector .child becomes parent .child in CSS
· The selector .grand-child becomes parent .child .grand-child
· Sass adds a space between each nesting level

---


** Second: Grouping Multiple Selectors

Example:

Sass Code:

```scss
parent-one,
.parent-two {
  padding: 20px;
  
  .child {
    padding: 10px;
  }
}
```

Compiled to CSS:

```css
parent-one,
.parent-two {
  padding: 20px;
}

parent-one .child,
.parent-two .child {
  padding: 10px;
}
```

Explanation:

· Sass applies the same nesting rules to all selectors in the list
· .child becomes a child of both parent-one and .parent-two
· This saves you from writing the same code twice

---


** Third: Using > for Direct Children

Example:

Sass Code:

```scss
parent > {
  .child {
    font-size: 20px;
  }
  .test {
    font-weight: bold;
  }
}
```

Compiled to CSS:

```css
parent > .child {
  font-size: 20px;
}

parent > .test {
  font-weight: bold;
}
```

Explanation:

· The > symbol means "direct child" only
· Sass puts > before each selector inside the block
· This applies the rule only to direct children, not all nested elements

---


** Fourth: Using > with Multiple Nesting

Example:

Sass Code:

```scss
parent {
  > .child {
    font-size: 20px;
  }
  
  .test {
    font-weight: bold;
  }
  
  + p {
    font-size: 15px;
  }
}
```

Compiled to CSS:

```css
parent > .child {
  font-size: 20px;
}

parent .test {
  font-weight: bold;
}

parent + p {
  font-size: 15px;
}
```

Explanation:

· > .child: Applies only to direct children with class child
· .test: Applies to all test elements inside parent (direct or indirect)
· + p: Applies to p element that comes immediately after parent (adjacent sibling)

---


** Fifth: Organizing Code with >

Example:

Sass Code:

```scss
parent {
  > {
    .element-one {
      font-size: 10px;
    }
    .element-two {
      font-size: 10px;
    }
  }
  
  .not-direct-child {
    font-weight: bold;
  }
}
```

Compiled to CSS:

```css
parent > .element-one {
  font-size: 10px;
}

parent > .element-two {
  font-size: 10px;
}

parent .not-direct-child {
  font-weight: bold;
}
```

Explanation:

· > before the block applies to all elements inside this block
· Both element-one and element-two are direct children
· not-direct-child can be at any level inside parent
· This method organizes code and shows that this group consists of direct children

---


** Sixth: Using & (Parent Selector)

The & symbol represents the parent selector itself. It's used to reference the outer selector.

Comprehensive Example:

Sass Code:

```scss
box {
  .title {
    font-size: 10px;
  }
  
  .description {
    font-size: 8px;
  }
  
  &.red {
    color: red;
  }
  
  &.green {
    color: green;
  }
  
  &:hover {
    background-color: #eee;
  }
  
  &:hover .title {
    font-weight: bold;
  }
  
  :not(&) {
    font-weight: normal;
  }
  
  [dir="rtl"] & {
    direction: rtl;
  }
}
```

Compiled to CSS:

```css
box .title {
  font-size: 10px;
}

box .description {
  font-size: 8px;
}

box.red {
  color: red;
}

box.green {
  color: green;
}

box:hover {
  background-color: #eee;
}

box:hover .title {
  font-weight: bold;
}

:not(box) {
  font-weight: normal;
}

[dir="rtl"] box {
  direction: rtl;
}
```



## Detailed Explanation of Each Part:

1. Regular Nesting:

```scss
.title {
  font-size: 10px;
}
// Becomes: box .title
```

2. Using & with Classes:

```scss
&.red {
  color: red;
}
// Becomes: box.red (no space)
// & here represents box
```

3. Using & with Pseudo-classes:

```scss
&:hover {
  background-color: #eee;
}
// Becomes: box:hover
// & allows adding :hover directly to the parent element
```

4. Using & with Nesting:

```scss
&:hover .title {
  font-weight: bold;
}
// Becomes: box:hover .title
// Applies to .title when box is in hover state
```

5. Using & with :not():

```scss
:not(&) {
  font-weight: normal;
}
// Becomes: :not(box)
// Applies to all elements that are not box
```

6. Using & with Attribute Selector:

```scss
[dir="rtl"] & {
  direction: rtl;
}
// Becomes: [dir="rtl"] box
// Applies to box when direction is rtl
```


** Summary of & Uses **

Usage Meaning Resulting CSS
&.class Same element with class box.class
&:hover Same element with state box:hover
& .child Parent then space then child box .child
.parent & Child before then parent .parent box
:not(&) Everything except parent :not(box)

Important Nesting Rules:

1. Don't Over-Nest: Avoid nesting more than 3-4 levels deep
2. Use & Wisely: The & symbol is very useful but only use it when needed
3. Nesting Increases Specificity: Each nesting level increases selector specificity
4. Organize Your Code: Use nesting to group related properties together

Example of excessive nesting (avoid this):

```scss
// Bad - hard to read
parent {
  .child {
    .grand-child {
      .great-grand-child {
        font-size: 10px;
      }
    }
  }
}

// Good - readable
parent .great-grand-child {
  font-size: 10px;
}
```

This is everything you need to know about Nesting and Parent Selector in Sass!
