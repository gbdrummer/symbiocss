# SymbioCSS...

...is an approach to writing HTML and CSS in a way that maintains separation of concerns while providing for symbiosis between the two technologies. It applies common patterns that allow for better organization and maintainability of User Interfaces.

The key advantages of this approach:

- Maintains separation of concerns (HTML: Document Structure, CSS: Presentation & Style, JS: Behavior & Interaction)
- Creates symbiosis amongst these three technologies by applying the same patterns to each
- Makes CSS easily maintainable by any size development team, large or small:
	- Negates specificity conflicts
	- Provides BEM-level namespacing without the ugly markup
	- Produces the cleanest, most semantic HTML possible
	- Results in a reduced number of CSS rulesets
	- All CSS selectors **read like English**
	- Lends itself to componentization
	- Works in any browser


## Separation of concerns
When building user interfaces, it is vitally important that we understand the intention and limitations of the tools we are using.  The tools of choice for writing user interfaces for the web are HTML, CSS and JavaScript. SymbioCSS focuses on HTML and CSS and the way they interface with JavaScript. **These three technologies will hereafter be collectively referred to as "The Big Three."**

### What HTML actually is
HTML stands for "Hyper Text Markup Language." We all know what it is used for: structuring web pages. But what *is* HTML?

HTML is a markup language, or "a system for annotating a document in a way that is *syntactically distinguishable* from its content." This means it allows you to "mark up" your content, adding meaning and context, without polluting the content itself.

HTML is specifically applied to writing web documents. It is important to remember that **when writing HTML, what you are actually doing is annotating content to add meaningful context.**

### What CSS actually is
CSS stands for "Cascading Style Sheets." We all know what it is used for: styling web pages. But what *is* CSS?

CSS is a style sheet language, or "a language that expresses the presentation of structured documents."

CSS is specifically applied to documents written in a markup language. It is important to remember that **when writing CSS, the whole point is to describe document presentation separately from document content.**

### What JavaScript actually is
JavaScript is a complete programming language. In the context of building a user interface for the web, it is used to add client-side behavior to HTML pages.

It is important to remember that **JavaScript is not intended to replace or mimic the functions of HTML or CSS.**


## Creating symbiosis
**Symbiosis**: any interdependent or mutually beneficial relationship between two persons, groups, or web technologies (That last bit was added by us)

Maintaining separation of concerns is not just a dogma; it is necessary to allow each of The Big Three to work as intended. That said, none of The Big Three operate in a vacuum; they must work together, and they must do so in a *symbiotic* way.

There are numerous popular approaches to writing CSS, all of which have merit. However, none represent a cohesive approach to using The Big Three together in a way that minimizes friction. Some strip bulk from CSS and add it to HTML, some do the opposite. All introduce hard syntactic rules that require time and training to master. All target a particular demon, be it "bloat," "disorganization," or "repetition", to the exclusion of others.

That's where SymbioCSS comes in; it applies common patterns to HTML and CSS that solve many of the maintenance issues UI developers typically run into, and it does so by using the inherent functionality of HTML and CSS.

### HTML:
HTML should be clean and free of unnecessary containers and semantics.

Remember, HTML is meant to annotate content with necessary and appropriate context. It is NOT meant to provide easy "hooks" for CSS or JavaScript. The days of seeing HTML like `<div class="div">` are past.

Let's take an example. Consider this basic document:

---
#### Article Title
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

#### Article Title
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

#### Article Title
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

---

We have a list of news articles. To display this document on the web, we need to add annotations so that browsers can correctly interpret it. Let's start by adding some basic structure:

```HTML
<div>
	<div>
		<div>Article Title</div>
		<div>...</div>
    </div>
	<div>
		<div>Article Title</div>
		<div>...</div>
    </div>
	<div>
		<div>Article Title</div>
		<div>...</div>
    </div>
</div>
```

OK, we've laid out a basic structure for this document. This would certainly work, but to be used in the real world it needs additional context. We can start by adding some classes to these divs:

```HTML
<div class="news-articles">
	<div class="news-article">
		<div class="news-article-title">Article Title</div>
		<div class="news-article-summary">...</div>
    </div>
	<div class="news-article">
		<div class="news-article-title">Article Title</div>
		<div class="news-article-summary">...</div>
    </div>
	<div class="news-article">
		<div class="news-article-title">Article Title</div>
		<div class="news-article-summary">...</div>
    </div>
</div>
```

This is pretty good, but there is still some missing information. For example, we now know the containing div element has news articles in it, but we haven't given it any context within the larger HTML document. We can use HTML5 semantic tags to add that context to all elements:

```HTML
<section class="news-articles">
	<article class="news-article">
		<h1 class="news-article-title">Article Title</h1>
		<p class="news-article-summary">...</p>
    </article>
	<article class="news-article">
		<h1 class="news-article-title">Article Title</h1>
		<p class="news-article-summary">...</p>
    </article>
	<article class="news-article">
		<h1 class="news-article-title">Article Title</h1>
		<p class="news-article-summary">...</p>
    </article>
</section>
```

This is getting better. Some developers might choose to stop and move on at this point, but that's not the SymbioCSS way. Notice how there is a great deal of repetition here? It is causing the HTML to be quite cluttered and hard to read. Let's remove all the duplicate information:

```HTML
<section class="news">
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
There we go; Now we have all the semantics we need without any repetition or clutter: 

- We know that this block of code represents a `section` of our document, and we know that `section` relates to "news" thanks to the class attribute we added.

- Inside, we have `article` tags. We know they represent news articles because they are inside `section.news`. 

- We know the `h1` inside each `article` represents the title of the article (that is the purpose of the `h1` tag), and we know it is the title of a news article because it is inside an `article` tag. 

- The summary of the news article is described as a paragraph or `p` with the added class attribute of "summary." Its parent elements provide the remaining needed context.

There are a few other things to notice here:
1. We did not use any `id` attributes.
2. All class names are **semantic in the context of the user**. For example, we did not employ class names like "container" or "wrapper" because those names are meaningless to the user.
3. We're relying on the **Parent-Child Relationship** of the individual elements to provide scope. In other words, each element is inheriting context from its parent.

Now, we want to add some styling. Let's go to the CSS:

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
5. There is no structural styling (ie box-model, positioning, etc) in any of these rulesets.

Now, let's imagine that previously in our CSS we have applied some styling rules to some of these elements in a global context:

```CSS
h1 {
	font-weight: bold;
}

section {
	margin-bottom: 1em;
}

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
h1 {
	font-weight: bold;
}

section {
	margin-bottom: 1em;
}

.sports.news {
	background: blue;
}

.world.news {
	background: green;
}

.news article {
	border: 1px solid black;
    padding: 1em;
}

.news article .summary {
	font-family: "Comic Sans";
}
```

Now we have two news sections, but rather than adding the "sports" or "world" context directly to each article, we've added it to the parent container, which allows that context to cascade to all elements inside it. If we wanted to add some special styling to "world news articles," for example, we'd write our CSS in just that way:

```CSS
.world.news article {
	font-family: "Wingdings";
}
```

By writing CSS this way, you have accomplished a number of important feats:

1. You no longer have to even think about the specificity of your selectors. It is all taken care of through namespacing.
2. Any developer who looks at your CSS will immediately understand which DOM elements your selectors are referencing. There will be no guesswork or searching through the stylesheet for a vaguely-named selector.
3. ALL articles share the same HTML template, but will be styled appropriately depending on which section they are added to.

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
.hidden {
	display: none !important;
    visibility: hidden !important;
	opacity: 0 !important;
}

.news article.alert {
	background: red;
    color: green;
    text-decoration: blink;
}
```
Global modifiers have `!important` flags on each rule, while local modifiers do not. Note that apart from special circumstances, this is the only case where the `!important` flag should be used.

### Where are all the `id`s?
If you are thinking "this looks an awful lot like BEM but less efficient," you are absolutely correct. This approach is not as efficient to parse as BEM due to the chained CSS selectors. 

However, it is entirely worth the added readability and maintainability of your code, especially if you are working with a large team. There is no specific syntax to learn, and besides, the amount of additional processing overhead required to parse the extra selectors is offset by the need for fewer selectors and declarations within. In fact, **this is how CSS was designed to work in the first place.**

So why not use `id`s?

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

## In a nutshell
SymbioCSS can be summarized in a set of simple-to-follow rules:

### HTML
1. HTML tags should be chosen based on their semantic value to the user.
2. No unnecessary containers or wrappers should be used.
3. HTML should contain all the context necessary to describe the document to the user, and NO MORE.
4. class attributes should be used to add needed semantics. The class name should be **semantic in the context of the user**
5. id attributes should only be added for JavaScript targeting or CSS targeting of container elements that do not have meaningful context to the user.

### CSS
1. Use contextual selectors.
2. Selectors should read like plain English
3. Visual style selectors should only contain the semantics necessary to define the element **in the context of the user**.
4. Style rules should not be reused arbitrarily; repetition of a style rule is OK if being applied to unrelated elements.
