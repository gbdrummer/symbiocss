[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Interfacing with JavaScript &raquo;](03 - Interfacing with JavaScript.md)

---
# CSS

CSS is an oft-misunderstood and oft-misused technology. As a developer it is common to find yourself in a situation where you are working on CSS written by another developer. Most of the time, that developer's aproach to naming convention and CSS structure is quite different from yours, and if he/she was a particularly lazy developer, there may be layers of hacks and overrides to compete with as you add to the stylesheet. 

Thankfully, SymbioCSS offers a way of writing CSS that brings clarity to this whole picture. It stipulates that CSS should:

1. use contextual selectors,
2. read like plain English,
3. use naming conventions that contain the semantics necessary to define the element **in the context of the user**,
4. never reuse style rules arbitrarily; repetition of a style rule is OK if being applied to unrelated elements.

## For example

In our previous example, we ended up with this HTML for our News widget:

```HTML
<section class="news">
	<h1>News</h1>
	<article>
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

Let's add some basic styling:

```CSS
.news {
	margin-bottom: 1em;
}

.news article {
	border: 1px solid black;
	padding: 1em;
}

.news article h1 {
	font-weight: bold;
}

.news article .summary {
	font-family: "Comic Sans";
}
```

There are several things to notice here:

1. Each of these selectors reads like English. 
2. It is entirely obvious what each selector refers to in the context of the whole document.
3. Each element is scoped to its parent context through the use of selector chaining.
4. Just like in the HTML, there is no unnecessary repetition of semantic information, and we have not included any semantics that are not important to the context of each element.

Now, let's imagine that we had previously applied some styling rules to some of these elements in a global context:

```CSS
/* Global rules */
h1 {
	font-weight: bold;
}

section {
	margin-bottom: 1em;
}

/* Component-scoped rules */
.news article {
	border: 1px solid black;
	padding: 1em;
}

.news article .summary {
	font-family: "Comic Sans";
}
```

This allows us to take advantage of the cascade. Once we've established a context for the elements we have used, we **only need to add styles that are specific to that context.** Let's expand upon this by adding some different types of news:

```HTML
<section class="sports news">
	<article>
		<h1>Article Title</h1>
		<p class="summary">...</p>
	</article>
</section>

<section class="world news">
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
```CSS
/* Global rules */
h1 {
	font-weight: bold;
}

section {
	margin-bottom: 1em;
}

/* "News" context
.news article {
	border: 1px solid black;
    padding: 1em;
}

.news article .summary {
	font-family: "Comic Sans";
}

/* "Sports News" context */
.sports.news {
	background: blue;
}

/* "World News" context
.world.news {
	background: green;
}
```

Now we have two news sections, but rather than adding the "sports" or "world" context directly to each article, we've added it to the parent container, which allows that context to cascade to all its child elements. If we wanted to add some special styling to "world news articles," for example, we'd write our CSS in just that way:

```CSS
.world.news article {
	font-family: "Wingdings";
}
```

By writing CSS this way, you have accomplished a number of important feats:

1. You no longer have to even think about the specificity of your selectors. It is all taken care of through namespacing.
2. Any developer who looks at your CSS will immediately understand which DOM elements your selectors are referencing. There will be no guesswork or searching through the stylesheet for a vaguely-named selector.
3. ALL articles share the same HTML template, but will be styled appropriately depending on which section they are added to.

## Modifiers

From here, it is a simple matter to tweak individual news articles by adding modifiers: 

`<article class="alert">` or `<article class="special-report">`

At this point you might be thinking "What if I have some global utility classes I want to use? Won't these specific selectors overwrite them?" The answer is yes, so enter the red-headed stepchild of CSS:

```CSS
.hidden {
	display: none !important;
	visibility: hidden !important;
	opacity: 0 !important;
}
```

By adding `!important` to your global modifiers you can rest assured their style rules will override any others. Modifiers can be scoped either globally or locally. For example:

```HTML
<article class="hidden">
	<h1>Article Title</h1>
	<p class="summary">...</p>
</article>
<article class="alert">
	<h1>Article Title</h1>
	<p class="summary">...</p>
</article>
```
```CSS
/* Global Modifier */
.hidden {
	display: none !important;
	visibility: hidden !important;
	opacity: 0 !important;
}

/* Local Modifier */
.news article.alert {
	background: red;
	color: green;
	text-decoration: blink;
}
```
Global modifiers have `!important` flags on each rule, while local modifiers do not. Note that apart from special circumstances, this is the only case where the `!important` flag should be used.

---
[&laquo; HTML](01 - HTML.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Interfacing with JavaScript &raquo;](03 - Interfacing with JavaScript.md)
