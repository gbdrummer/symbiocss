[&laquo; Previous](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](/)

---
# Interfacing with JavaScript

Cluttered HTML and indecipherable CSS are bad enough as it is, but throw JavaScript into the mix and a bad situation becomes worse. If you need to target an HTML node in your JavaScript, which scenario would you prefer to see:

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

The `id` fully describes exactly what the element is: an input that receives the data "first name." you can then easily target and manipulate this element with JavaScript:

```HTML
document.getElementById('first_name_input')
```

It is immediately apparent what is being targeted in the JavaScript code; There is no guesswork involved because we have clearly defined the element with our `id`. 

In the event more context is needed, you can still add parent context to an id in your JavaScript:

```JS
document.querySelector('form.signup #first_name_input')
```

In SymbioCSS, `id`s should ALWAYS contain ALL the necessary semantic and structural information needed to clearly define the element (but not its parent context) in a single string. For example, if you need to add a wrapper to a block of HTML specifically for the purpose of targeting it with JavaScript, the `id` given to that wrapper element should indicate this:

`#news_section_wrapper`

This element would not need a class attrbute as it is not used for visual styling. However, it CAN be used for structural CSS, ie

```CSS
#news_section_wrapper {
	display: flex;
}
```

This approach should be used whenever it becomes necessary to add DOM elements which do not have semantic context for the user, like wrapper elements. This should be avoided if at all possible, however.

Note that `id`s should NEVER be included in contextual selectors!

---
[&laquo; Previous](02 - CSS.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Next &raquo;](/)
