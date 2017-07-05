# SymbioCSS

[&laquo; Building Reusable Components](04_building-reusable-components.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | Boilerplate &raquo; (Coming Soon)

# Interfacing with JavaScript

Cluttered HTML and indecipherable CSS are bad enough as it is, but throw JavaScript into the mix and a bad situation becomes worse. For instance, if you needed to target an HTML node in your JavaScript, which of the following two examples would you prefer to use?

This:
```js
document.getElementById('content_wrapper');
```
or this:
```js
document.getElementById('news_articles');
```

In the first scenario, it is not at all clear what is being targeted or why. "content_wrapper" could refer to a lot of things, and if another developer needs to work on this in the future, they will probably spend some time scratching their head.

The second scenario is much better. It is clear which element of the UI is being interacted with, and that will save time and headaches going forward.

---

**If you've been following our News Articles example, you may be wondering "where are all the id's?"**

`id`s have a place in SymbioCSS, but not for styling. `id`s are meant to provide direct access to a specific DOM element. To accomplish this, they are granted a much higher degree of specificity than class or tag selectors, and as a result they can cause a lot of specificity problems when combined with other types of selectors. It is much easier to simply avoid using them for styling.

Instead, `id`s are the perfect candidate for interfacing with JavaScript. For example:

```HTML
<input id="first_name_input" name="first-name" type="text">
```

The `id` fully describes exactly what the element is: an input that receives the data "first name." You can then easily target and manipulate this element with JavaScript:

```JS
document.getElementById('first_name_input')
```

---

## One more use case for `id`s

There are occasional circumstances where it is necessary to add an arbitrary wrapper to a block of HTML for layout purposes. For example, take this document with 5 stacked sections:

```HTML
<body class="blog">
	<section>
		...
	</section>
	<section>
		...
	</section>
	<section>
		...
	</section>
	<section>
		...
	</section>
	<section>
		...
	</section>
</body>
```

If we want to group the middle three sections together in columns, it would make sense to add a wrapper around those three sections and set it to `display: flex;`. Because the wrapper is used purely for visuals and has no contextual meaning to the content, we can create a `div` and give it an `id`. Let's be very descriptive in the naming:

```HTML
<body class="blog">
	<section>
		...
	</section>
	<div id="#blog_section_flex_wrapper">
		<section>
			...
		</section>
		<section>
			...
		</section>
		<section>
			...
		</section>
	</div>
	<section>
		...
	</section>
</body>
```

```CSS
#blog_section_flex_wrapper {
	display: flex;
}
```

The integrity of our content outline is unchanged, but we can now display it in any way we choose. It's best to use this technique sparingly to keep your HTML uncluttered, but it is a good way of separating elements that are semantic to the content and those that aren't.

 `id`s should be included at the bottom of your stylesheet and should NEVER be included in contextual selectors. (See [Structuring your Style Sheets](03_structuring-your-style-sheets.md)).
 
That's it for now! Check back later for starter code and more examples. Happy Developing!

- Graham Butler

---
[&laquo; Building Reusable Components](04_building-reusable-components.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | Boilerplate &raquo; (Coming Soon)
