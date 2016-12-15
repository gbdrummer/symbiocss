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
## How to write HTML

1. Choose tags based on their semantic value to the content,
2. use `class` attributes to add missing context, and
3. do not repeat this context on child elements.

Let's take an example. Consider this basic document:

<pre>
### Blog

#### Article 1 Title
Article 1 summary

#### Article 2 Title
Article 2 summary

#### Article 3 Title
Article 3 summary

</pre>

We have a basic blog. To display this document on the web, we need to add annotations so that browsers can correctly interpret it. Let's start by adding some basic structure:

```HTML
<div>
	<div>Blog</div>
	<div>
		<div>Article 1 Title</div>
		<div>Article 1 summary</div>
	</div>
	<div>
		<div>Article 2 Title</div>
		<div>Article 2 summary</div>
	</div>
	<div>
		<div>Article 3 Title</div>
		<div>Article 3 summary</div>
    </div>
</div>
```

OK, we've laid out a basic structure for this document. This would certainly work, but it needs additional context. First, let's choose some more appropriate tags for these elements:

```HTML
<section>
	<h1>Blog</h1>
	<article>
		<h1>Article 1 Title</h1>
		<p>Article 1 summary</p>
	</article>
	<article>
		<h1>Article 2 Title</h1>
		<p>Article 2 summary</p>
	</article>
	<article>
		<h1>Article 3 Title</h1>
		<p>Article 3 summary</p>
	</article>
</section>
```

From looking at this HTML, we now understand that we have a section of a larger document, and that section contains articles of some kind. Each article has a heading and paragraph of text.

What we cannot glean from looking at this HTML is that this section of our larger document is a blog. It's true that we could look inside the section tag, see `<h1>Blog</h1` and realize that this section is a blog, but our CSS cannot rely on the content itself to get that information. After all, our CSS will be interacting with the HTML annotations, not directly with the content.

In other words, our parent `section` is missing some important context. We also have not clearly defined the context of the `p` tags inside each article. Let's add the remaining context using `class` attributes:

```HTML
<section class="blog">
	<h1>Blog</h1>
	<article>
		<h1>Article 1 Title</h1>
		<p class="summary">Article 1 summary</p>
	</article>
	<article>
		<h1>Article 2 Title</h1>
		<p class="summary">Article 2 summary</p>
	</article>
	<article>
		<h1>Article 3 Title</h1>
		<p class="summary">Article 3 summary</p>
	</article>
</section>
```

Now, when we look at this HTML we understand that we have a blog, which is a section of a larger document, and that blog contains articles, each of which has a heading and a summary paragraph. That's all we need to know!

** Important Notes: **
1. We've used HTML5 semantic tags to add most of the context we needed (see HTML Rule #1 above),
2. we used `class` attributes to add the remaining context (see HTML Rule #2 above), and
3. we did not repeat any of this context inside our blog container as we might with a class-naming convention such as B.E.M., which would stipulate that "blog" be prepended to the articles and "summary" class, ie `.blog__article` and `.blog__article__summary`. (see HTML Rule #3 above).

Now, let's add some style to our blog.


---
[&laquo; Introduction](00 - Introduction.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [CSS &raquo;](02 - CSS.md)
