[&laquo; Previous](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](/)

---
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

`id`s have a place in SymbioCSS, but not for styling. `id`s are meant to provide direct access to a specific DOM element. To accomplish this, they are granted a much higher degree of specificity than class or tag selectors, and as a result they can cause a lot of specificity problems. Using an `id` anywhere in the DOM for styling reintroduces the problem of specificity to the developer and will likely break the namespacing and readability of your selectors. It is much easier to simply avoid using them for styling.

Instead, `id`s are the perfect candidate for interfacing with JavaScript. They act as a reference to a specific DOM element, and should be named as such. For example:

```HTML
<input id="first_name_input" name="first-name" type="text">
```

The `id` fully describes exactly what the element is: an input that receives the data "first name." You can then easily target and manipulate this element with JavaScript:

```JS
document.getElementById('first_name_input')
```

---

## One more use case for `id`s

There are occasional circumstances where it is necessary to add a wrapper to a block of HTML for layout purposes. For example, if you have a document with 5 sections on it, but you'd like to (arbitrarily) display three of them in a row with the other two above and below, it would make sense to add a flexbox wrapper around those three sections. Because the wrapper is used purely for visuals and has no contextual meaning to the user, an `id` can be used to set the wrapper's box model to "flex." 

When using an id this way, it makes sense to include information in the `id` name that is out of user context as a way of diffrentiating this container from the rest of the document:

```CSS
#news_section_flex_wrapper {
	display: flex;
}
```

This approach should be used whenever it becomes necessary to add DOM elements which do not have semantic context for the user, like wrapper elements. This should be avoided if at all possible, however, as it is usually possible to add all the necessary styling to elements that DO have user context.

 `id`s should be included at the bottom of your stylesheet and should NEVER be included in contextual selectors! More on this later.

---
[&laquo; Previous](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](/)
