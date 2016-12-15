[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Stylesheets &raquo;](03 - Structuring your Stylesheets.md)

---

## How to write CSS

1. Use contextual (chained) selectors,
2. use the parent-child relationship of the HTML elements to create scoping, and
3. once you have established a context for the elements in your document, only add styles that are specific to that context.

Here are some basic styles for our blog:

```CSS
.blog {
	margin-bottom: 1em;
}

.blog article {
	border: 1px solid black;
	padding: 1em;
}

.blog article h1 {
	font-weight: bold;
}

.blog article .summary {
	font-family: "Comic Sans";
}
```

There are several important things to notice here:

1. Each of these selectors reads like an English phrase,  
2. it is entirely obvious what each selector refers to in the context of the whole document just by reading it, and
3. each element is scoped to its parent context through the use of selector chaining (see CSS Rule #1 above)

It is also important to realize that this structure has created a "component" that we can now reuse. If we wanted to add this blog to another page on our site, we'd simply need to load in this HTML template and css snippet, and the blog will be styled correctly. 

If you're skeptical right now, I get it. We're obviously going to have some global css we need to deal with, so let's consider CSS Rule #3 above: "Once you have established a context for the elements in your document, only add styles that are specific to that context."

Let's say we have global styes for our`h1` and `section` tags. Our stylesheet would need to be updated like so:

```CSS
/* Global rules */
h1 {
	font-weight: bold;
}

section {
	margin-bottom: 1em;
}

/* Component-scoped rules */
.blog article {
	border: 1px solid black;
	padding: 1em;
}

.blog article .summary {
	font-family: "Comic Sans";
}
```

Our global styles go at the top of the stylesheet, and our "component-scoped" css goes underneath. This ensures that the cascade works properly, and our more specific component-scoped css will override any of our less specific global rules. `.blog article` effectively *extends* `section` with its own styles, but only adds the border and padding values; It doesn't re-establish the margin-bottom value (see CSS Rule #3 above).

The net effect is that we don't have to actually think about specificity at all. It is taken care of thanks to the scoping we've added to our selectors via chaining (see CSS Rule #1 above).

If you're worried that chaining selectors will degrade the performance of your CSS, you are correct, however this has not been shown to be a problem worth worrying about in virtually any situation. ** -- CITATION -- ** You are efectively trading a millisecond or two of load/parse time for what could amount to many hours saved on maintenance over time. More on this later.

---
[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Stylesheets &raquo;](03 - Structuring your Stylesheets.md)
