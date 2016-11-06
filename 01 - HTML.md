[&laquo; Introduction](00 - Introduction.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [CSS &raquo;](02 - CSS.md)

---

# HTML

HTML should be clean and free of unnecessary clutter. This includes layers of wrapper elements, div soup, and controls that are better suited to CSS or JavaScript.

SymbioCSS tackles this issue by following these rules:

1. HTML tags should be chosen based on their semantic value to the user.
2. No unnecessary wrapper elements should be used.
3. HTML should contain all the context necessary to describe the document to the user, and NO MORE.
4. `class` attributes should be used to add missing semantics. The class should be named in the context of the user.
5. `id` attributes should only be added for JavaScript targeting or CSS targeting of container elements that do not have meaningful context to the user.

Let's take an example. Consider this basic document:

---
### News

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
	<div>News</div>
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
	<div class="news-title">News</div>
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
	<h1 class="news-title">News</h1>
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

This is getting better. Some developers might choose to stop and move on at this point, but that's not the SymbioCSS way. Notice how there is a great deal of repetition here? It is causing the HTML to be quite cluttered and hard to read. Let's remove all the redundant information:

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
There we go; Now we have all the semantics we need without any repetition or clutter: 

- We know that this block of code represents a `section` of our document, and we know that `section` relates to "news" thanks to the class attribute we added.

- We know the first-child `h1` represents the title of this `section` (since that is the purpose of the `h1` tag)

- Inside, we have `article` tags. We know they represent news articles because they are inside `section.news`. 

- We know the `h1` inside each `article` represents the title of the article, and we know it is the title of a news article because it is inside an `article` tag. 

- The summary of the news article is described as a paragraph or `p` with the added class attribute of "summary." Its parent elements provide the remaining needed context.

There are a few other things to notice here:

1. We did not use any `id` attributes.
2. All class names are **semantic in the context of the user**. For example, we did not employ class names like "container" or "wrapper" because those names are meaningless to the user.
3. We're relying on the **Parent-Child Relationship** of the individual elements to provide scope. In other words, each element is inheriting context from its parent.

---
[&laquo; Introduction](00 - Introduction.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [CSS &raquo;](02 - CSS.md)
