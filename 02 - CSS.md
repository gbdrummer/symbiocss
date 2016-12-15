# SymbioCSS

[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Stylesheets &raquo;](03 - Structuring your Stylesheets.md)

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
	color: blue;
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

.blog article h1 {
	color: blue;
}

.blog article .summary {
	font-family: "Comic Sans";
}
```

Our global styles go at the top of the stylesheet, and our "component-scoped" css goes underneath. This ensures that the cascade works properly, and our more specific component-scoped css will override any of our less specific global rules. `.blog article h1` effectively *extends* `h1` with its own styles, but only adds the color value; It doesn't re-establish the font-weight value (see CSS Rule #3 above).

The net effect is that we don't have to actually think about specificity at all. It is taken care of thanks to the scoping we've added to our selectors via chaining (see CSS Rule #1 above).

If you're worried that chaining selectors will degrade the performance of your CSS, you are correct, however this has not been shown to be a problem worth worrying about in virtually any situation. ** -- CITATION -- ** You are effectively trading a millisecond or two of parse/interpretation time for what could amount to many man hours saved on maintenance over time. More on this later.

## Taking it further
This blog is clearly much more simplistic than what we are tasked with developing in the real world, so to demonstrate the scalability of SymbioCSS, let's start by adding some different categories of blog articles; how about "health" and "sports" sections:

```HTML
<section class="health blog">
	<article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
</section>

<section class="sports blog">
	<article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
	<article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
    </article>
</section>
```


Instead of adding "health" or "sports" classes to each of our blog articles, we are taking advantage of the parent-child relationship of HTML tags to add this context (see CSS Rule #2 above). Hence, our CSS will look like this:

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

.blog article h1 {
	color: blue;
}

.blog article .summary {
	font-family: "Comic Sans";
}

.health.blog article {
	background: blue;
}

.sports.blog article {
	background: green;
}
```

This means that any article added to the "health blog" container will have a blue background, while the same article added to the "sports blog" container will have a green background. The "health" or "sports" context is *cascading* to the child elements of the container.

This is a purely Object-oriented approach to CSS. Here are just a few benefits:

1. Your style sheet reads like a list of clearly-defined references to elements in your HTML,
2. each selector applies the minimum number of style rules necessary,
3. selectors share style rules in the most efficient way possible (the cascade),
4. specificity is taken care of inherently,
5. your style sheet will naturally become ordered from least-specific to most-specific (ala ITCSS), and
6. it will have the added benefit of being organized from one reusable component to the next. Any of these components could be abstracted into their own style sheet, or used inside a Web Component, etc.
7. Each component is completely self-contained, and the chances of conflicts are drastically minimized due to the specificity introduced with chained selectors.

## Modifiers

A natural question at this point would be "What am I supposed to do if I need to override any of these really specific selectors with a modifier class?" As an example, maybe you have a ".hidden" class that you use to show/hide elements with JavaScript:

```CSS
.hidden {
	display: none;
    visibility: hidden;
	opacity: 0;
}
```

Obviously, if any of your component-scoped CSS includes display, visibility or opacity rules, this class will not work as intended. Thankfully, CSS provides us with a simple workaround:

```CSS
.hidden {
	display: none !important;
    visibility: hidden !important;
	opacity: 0 !important;
}
```

Most methodologies advise against using the `!important` flag, but the reasoning is usually something to the effect of "Using !important can lead to unexpected conflicts that are hard to manage." This is true in the absence of a structured approach to writing CSS, but when you follow logical patterns, this becomes a non-issue. If following the SymbioCSS approach, a global modifier class is the only case where the `!important` flag will ever need to be used. In fact, this is in line with the original intent of the `!important` flag, which was to act as a guaranteed override of document styles so that users could establish their own customized style sheet (which can be used to enlarge fonts or change colors for those with vision troubles, for example).

In SymbioCSS, modifiers can also be scoped locally, in which case the `!important` flag is not needed. For example, let's say we want to be able to mark certain blog articles as "special". We can do so by adding a local modifier:

```HTML
<section class="blog">
	<article class="special">
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
    <article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
    <article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
</section>
```

We'd then add this component-scoped CSS:

```CSS
.blog article.special {
	font-family: Wingdings;
}
```

You can also then use the parent-child cascade to style "special health blog articles" differently from "special sports blog articles":

```CSS
.health.blog article.special {
	text-shadow: 1px 1px 2px pink;
}

.sports.blog article.special {
	text-shadow: 1px 1px 2px orange;
}
```

The key of this approach is *context*. As your website or app grows, you'll find that as your style sheet grows in length, it does not also grow in complexity. These patterns remain consistent and repeatable.

---
[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Stylesheets &raquo;](03 - Structuring your Stylesheets.md)
