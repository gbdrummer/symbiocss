# SymbioCSS

[&laquo; Introduction](README.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [How to write CSS &raquo;](02_css.md)

## How to write HTML

1. Choose tags based on their semantic value to the content,
2. use `class` attributes to add missing context, and
3. do not repeat this context on child elements.

Let's take an example. Consider this basic document:

---
### Blog

#### Article 1 Title
Article 1 summary

#### Article 2 Title
Article 2 summary

#### Article 3 Title
Article 3 summary

---

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

OK, we've laid out a basic structure for this document. This would certainly work, but it needs additional context. First, let's choose some more appropriate tags for this content:

```HTML
<section>
  <h1>Blog</h1>
  <article>
    <h2>Article 1 Title</h2>
    <p>Article 1 summary</p>
  </article>
  <article>
    <h2>Article 2 Title</h2>
    <p>Article 2 summary</p>
  </article>
  <article>
    <h2>Article 3 Title</h2>
    <p>Article 3 summary</p>
  </article>
</section>
```

From looking at this HTML, we now understand that we have a section of a larger document which contains articles of some kind. Each article has a heading and paragraph of text.

What we cannot glean from looking at this HTML is that this section of our larger document is a "blog." It's true that we could look inside the first `<h1>` tag and see the word "Blog," but our CSS cannot rely on the content for that information. After all, our CSS will be interacting with the HTML annotations, not directly with the content itself.

In other words, our parent `section` is missing important contextual information. We also have not clearly defined the context of the `p` tags inside each article. Let's add the missing context using `class` attributes:

```HTML
<section class="blog">
  <h1>Blog</h1>
  <article>
    <h2>Article 1 Title</h2>
    <p class="summary">Article 1 summary</p>
  </article>
  <article>
    <h2>Article 2 Title</h2>
    <p class="summary">Article 2 summary</p>
  </article>
  <article>
    <h2>Article 3 Title</h2>
    <p class="summary">Article 3 summary</p>
  </article>
</section>
```

Now, when we look at this HTML we understand that we have a blog, which is a section of a larger document, and it contains articles, each of which has a heading and a summary paragraph. That's all we need to know!

**Important Notes:**

1. We've used HTML5 semantic tags to add most of the context we needed (see HTML Rule #1 above),
2. we used `class` attributes to add the remaining context (see HTML Rule #2 above), and
3. we did not repeat any of this context in the class names of elements inside our blog container (see HTML Rule #3 above).

Next, [let's add some style to our blog](02_css.md).

---
[&laquo; Introduction](README.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [How to write CSS &raquo;](02_css.md)
