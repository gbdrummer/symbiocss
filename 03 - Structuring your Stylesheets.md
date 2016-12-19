#SymbioCSS

[&laquo; CSS](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Building Reusable Components &raquo;](04 - Building Reusable Components.md)

---

# Structuring your Stylesheets

Let's examine in more detail the way a SymbioCSS style sheet is constructed:

CSS documents should be arranged by two criteria: Specificity and Component Context.

In SymbioCSS, rulesets are arranged from least specific to most specific, as in [ITCSS](http://itcss.io/). However, it is broken down a bit further. Rather than structuring your entire stylesheet from least-specific to most-specific, SymbioCSS recommends breaking it up into components and applying the ITCSS approach to specificity to those. This way you can organize your CSS and specificity in chunks instead of one monolithic stylesheet.

In other words, your stylesheet will look something like this:

```CSS
/***** Global utility classes *****/

.hidden {
	display: none !important;
	visibility: hidden !important;
	opacity: 0 !important; 
}

.show {
	display: block !important;
	visibility: visible !important;
	opacity: 1 !important;
}

/***** Component-specific styles *****/

/* Component 1 Context */
.component-1 {...}

.component-1 .sub-component {...}

.component-1.modifier .sub-component {...}

/* Component 2 Context */
.component-2 {...}

.component-2 .sub-component {...}

.component-2.modifier .sub-component {...}

/* Singletons */
main {
	display: flex;
}

#component-1_flex_wrapper {
	display: flex;
}

```

In the Component-specific styles section, notice how the specificity increases as you descend through the document, but "resets" when you move from one component to the next.

This approach is analogous to ITCSS in that where ITCSS structures CSS in an inverted triangle, SymbioCSS structures it more like an inverted Christmas Tree. This allows for much more modular style sheets.

Next, let's look at [building the components themselves](04 - Building Reusable Components.md).

---
[&laquo; CSS](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Building Reusable Components &raquo;](04 - Building Reusable Components.md)
