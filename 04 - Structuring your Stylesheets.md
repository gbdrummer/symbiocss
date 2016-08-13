[&laquo; Previous](03 - Interfacing with JavaScript.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](05 - Building Reusable Components.md)

---

# Structuring your Stylesheets

For ideally-functioning CSS, there is a particular structure that can be used. This structure ensures proper cascade and inheritance throughout your CSS file.

Modern UIs call for componentization; Small, encapsulated units of functionality and style that can be used and reused anywhere in your document. In order for these components to work reliably, any HTML, CSS, or JavaScript contained therein needs to be scoped to that component without leaking into the surrounding DOM. HTML and JavaScript can be scoped fairly easily, as can CSS if included inline, but if being loaded from a separate stylesheet more care is necessary.

### Creating a Stylesheet
CSS documents should be arranged by two criteria: Specificity and Component Context.

Rulesets should be ordered from least specific to most specific. In other words, your global, reusable styles go at the top of your stylesheet, and your more specific, component-scoped styles go toward the bottom. This is the approach of [ITCSS](http://itcss.io/) and deserves to be considered best practice when following a modern approach to CSS.

However, there is an additional dimension to this when you enter the world of componentization; Since components are self-contained entities, they have a large amount of CSS that only applies to the component itself. For a UI with a large number of components, a stylesheet can start to become cluttered and difficult to follow if the ITCSS approach is followed correctly.

In SymbioCSS, the ITCSS approach to specificity is retained, but further broken down. Rather than structuring your entire stylesheet from least-specific to most-specific, SymbioCSS recommends breaking it up into components and applying the ITCSS method to those. This way you can organize your CSS and specificity in chunks instead of one monolithic stylesheet.

in other words, your stylesheet will look something like this:

```CSS
/* Global utility classes */
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

/* Component-specific styles */
/* Component 1 Context */
.component-1 {...}

.component-1 .sub-component {...}

.component-1.modifier .sub-component {...}

/* Compoonent 2 Context */
.component-2 {...}

.component-2 .sub-component {...}

.component-2.modifier .sub-component {...}

```

In the Component-specific styles section, notice how the specificity increases as you descend through the document, but "resets" when you move from one component to the next.

This approach is analogous to ITCSS in that where ITCSS structures CSS in an inverted triangle, SymbioCSS structures it more like an inverted Christmas Tree. This allows you to place your component CSS anywhere you wish in your CSS file, or add/remove components at will without worrying about scope conflicts.

---
[&laquo; Previous](03 - Interfacing with JavaScript.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](05 - Building Reusable Components.md)
