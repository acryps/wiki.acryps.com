# HTML
Documents should be indented properly.

Each document should contain the following code. The `<html>` tag can be omitted. XML namespace attributes can be omitted.
```html
<!doctype html>
<head>
    <title></title>
</head>
<body>
    ...
</body>
```

## Escaping the &lt;div&gt;
In the early web development, each element had a purpose and a attached style. `<h1>` was used to indicate a header and `<b>` was used to make text bold. Sadly, developers soon started abusing `<h3>` as a `<h1>` because it was smaller - event tho, the element indicated a third tier heading.

CSS was added, which allowed the proper use of `<h1>` as the main heading, but allowed custom font sizes. But developers keept using `<h3>` to do `<h1>`'s work, because "well it was the correct size". 

Applications got bigger, and developers had to add components to their pages which could not be described by html - so people started abusing `<div>`, which indicates a division/block in a page. Today, most web applications are a mess of one thousand `<div>` elements with even more classes to differentiate between them. People never even question, why each entry in their css starts with a `.`.

We developed an alternative system, which allows us to write clean html, while staying standards-compliant (because we add a `-` to custom elements, thus the `ui-` prefix).
```html
<ui-card>
    <img src="header.png" />

    <ui-title>
        Lorem 

        <ui-badge ui-danger>
            Danger
        </ui-badge>
    </ui-title>

    <ui-content>
        Ipsum door net sit amet
    </ui-content>
</ui-card>
```

This results in much cleaner CSS, only using actual tag names and attribute selectors, which can even contain values. Selectors in JavaScript are cleaner too, as they use the same queries as CSS.

Developers can always locate their current location as closing tags contain the tag name too, not just the class in the opening tag.

The HTML is much lighter, omitting the `class=""` notation, which reduces loading times. 

Search engines and screen readers can infer just as little from a `<div>` as they can from `<ui-card>`. Thus, it is important to use standard HTML elements whenever possible, for example wrapping text within a `<article>` tag.

All modern browsers understand this structure, event internet explorer. Popular front end frameworks create the same html when components are used (thats why all component names must contain a `-`, usually a `app-` prefix). You will hear the most criticism towards this technique from avid angular enjoyers, which are mostly unaware of their usage.

Often we see usage of `<ul>` elements that don't even represent a list, or developers using illegal elements such as `<content>` - just don't - use `ui-` instead.

The custom elements do not have any style attached to them. 
No properties have to be reset and browsers will always display the elements without adding varying custom styles.
But having no default style requires setting the `display` property in CSS.

## Naming and nesting
Use standard HTML elements whenever possible. Avoid `<b>` and `<i>` as they are 'descriptive' and not 'declarative': They describe the text as bold and not with emphasis (`<em>`), which is then styled to be bold or italic.

Try to keep the html as slim as possible. Use `<ui-title>` instead of `<ui-card-title>` in the example below. This allows the next developer to just change the `<ui-card>` to another tag if the layout should be changed (for example to a `<ui-item>` within a list)

```html
<ui-card>
    <ui-title>
        Lorem Ipsum
    </ui-title>
</ui-card>
```

The container for cards should be called `<ui-card-collection>`, because the items (`<ui-card>`) can be standalone. A list, which will always only contain items, can be denoted by the more general `<ui-list>` with the items as `<ui-item>`.