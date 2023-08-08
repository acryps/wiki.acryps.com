# Formatting CSS and SCSS
Source files should be sorted in the same order
1. Include of other files
2. Variables (colors, fonts, ...)
3. General styling (`body`, `:root`)
4. Page layout
5. Reused components
6. Pages

For naming guidelines, refer to [html guidelines](html.md).

Avoid `box-sizing`, `float`/`clear` & percentage paddings/margins.

Avoid coping CSS from stack overflow, it's very common to find very outdated solutions.

## Units
Use `rem` wherever possible, but don't set a custom font size in `:root`/`html`.
Use `px` for borders.

Use lowercase hex for colors, use 3 digit form when possible (`#cccccc` → `#ccc`).
Define colors in variables, not in styles.

Don't remove leading zeroes in numbers (use `0.5rem` instead of `.5rem`)

## Nesting & Block Ordering
When using SCSS, selectors should be nested.
Properties should be listed before children.

```scss
ui-card {
    // own styles first
    display: block;

    border: 1px solid #000;

    // modifiers
    &[ui-danger] {
        border-color: $danger;
    }

    // own pseudo classes
    &:before {
        ...
    }

    &:first-child {
        ...
    }

    // general child pseudo classes
    :first-child {

    }

    // children, in the order that they usually appear within in html
    img {
        ...
    }

    ui-name {
        font-weight: bold;
    }
}
```

## Property Order
Most CSS is not ordered, which leads to a lot of wasted development time. 
The ordering principle is based on property severity. 

The severity groups should be grouped and should contain a space in between.
```scss
ui-test {
    display: block; 
    max-height: 4rem; // width & height > margin & padding
    overflow: auto; // near max-height - they belong together
    margin-inline: 1rem;

    color: $primary;
    background: $primary-inverse;

    &:after {
        content: counter(test-counter);
        counter-increment: test-counter;

        display: inline-block;
    }
}

ui-test {
    --weight: bold;

    display: flex;
    align-items: center;

    position: relative;
    margin: 1rem;
    padding: 0.5rem;

    color: $primary;
    border: 1px solid $primary;
    border-bottom: none; // expanded property (border-bottom) after shorthand (border)

    transition: 0.5s;
}

ui-test {
    display: block;
    whitespace: nowrap;
    padding; 1rem;

    position: absolute;
    top: 0;
    left: 1rem;
    right: 3rem;
    bottom: 5rem;
    z-index: 1rem;

    line-height: 1.25;
    background: $primary;

    animation: 0.2s fade-test;
}
```
