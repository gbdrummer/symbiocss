# SymbioCSS

[&laquo; CSS](02_css.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Building Reusable Components &raquo;](04_building-reusable-components.md)

## Structuring your Style Sheets

Let's examine in more detail the way a SymbioCSS style sheet is constructed:

CSS documents should be arranged by two criteria: Specificity and Component Context.

In SymbioCSS, rulesets are arranged from least specific to most specific, as in [ITCSS](http://itcss.io/). However, it is broken down a bit further. Rather than structuring your entire stylesheet from least-specific to most-specific, SymbioCSS recommends breaking it up into components and applying the ITCSS approach to those. This way you can organize your CSS in chunks instead of one monolithic stylesheet.

In other words, your stylesheet will look something like this:

```CSS
/***** Global styles *****/

html {
  font-family: 'Comic Sans';
}

h1, h2, h3 {
  font-weight: bold;
}

/***** Global Modifiers *****/

.hidden {
  display: none !important;
  visibility: hidden !important;
  opacity: 0 !important;
}

/***** Component-specific styles *****/

/* Component 1 Context */
.component-1 {...}

.component-1 .child {...}

.component-1.modifier .child {...}

/* Component 2 Context */
.component-2 {...}

.component-2 .child {...}

.component-2.modifier .child {...}

/***** Singletons *****/

main {
  display: flex;
}

```

In the Component-specific styles section, notice how the specificity increases as you descend through the document, but "resets" when you move from one component to the next.

This approach is an extension of the ITCSS concept, but instead of structuring CSS in an inverted triangle, SymbioCSS structures it more like an inverted Christmas Tree. This allows for much more modular style sheets.

Next, let's look at [building the components themselves](04_building-reusable-components.md).

---
[&laquo; CSS](02_css.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Building Reusable Components &raquo;](04_building-reusable-components.md)
