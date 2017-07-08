# SymbioCSS

[&laquo; How to write HTML](01_html.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Style Sheets &raquo;](03_structuring-your-style-sheets.md)

## How to write CSS

1. Use contextual and chained selectors,
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

1. Each CSS selector reads like an English phrase,  
2. each CSS selector makes it clear which part of the document it refers to, and
3. each CSS rule block is scoped to the "blog" `section` or its child `article`s through the use of contextual selector chaining.

It is also important to notice that this structure creates a reusable "CSS Component". If we wanted to display this blog or a similar one elsewhere on our site, we'd simply load in the HTML and this css snippet, and the blog will be styled correctly.

---

We're obviously going to have some global css we need to deal with, so let's consider CSS Rule #3 above: **"Once you have established a context for the elements in your document, only add styles that are specific to that context."**

Let's say we have global styes for our`h1` and `section` tags:

```CSS
/* Global rules --------------------------------- */

h1 {
  font-weight: bold;
}

section {
  margin-bottom: 1em;
}
```

With these styles applied globally, we can now rewrite our blog component styles to include the missing information:

```CSS
/* Blog Component ------------------------------- */

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

Our global styles go at the top of the stylesheet and will be applied to all `h1` and `section` elements across the board. Our "component-scoped" css receives the global styles thanks to the [Cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade), and then applies additional styles to the blog component, leaving the global styles untouched thanks to [Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). 

In other words, `.blog article h1` effectively *extends* `h1` with its own styles, but only adds the `color: blue;` declaration; It doesn't re-establish the font-weight property.

If another section of our document needs to have a green `h1`, we can do so without affecting our blog:

```CSS
.blog article h1 {
  color: blue;
}

.other-section h1 {
  color: green;
}
```

The net effect is that we don't have to actually think about specificity at all. It is taken care of thanks to the scoping we've added to our selectors via chaining (see CSS Rule #1 above).

## Just in case...

If you're worried that chaining selectors will degrade the performance of your CSS, you are correct. However, this has been shown to be a problem not worth worrying about:

[Jordan Walker of CSStricks](https://css-tricks.com/efficiently-rendering-css/) says:
<blockquote>
...the lesson here is not to sacrifice semantics or maintainability for efficient CSS.
</blockquote>

[Ben Frain](https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/) has this to say on the subject:
<blockquote>
Sweating over the selectors used in modern browsers is futile; most selection methods are now so fast it’s really not worth spending much time over. Furthermore, there is disparity across browsers of what the slowest selectors are anyway.
</blockquote>

[Harry from CSSWizardry](http://csswizardry.com/2011/09/writing-efficient-css-selectors/) sums it up like this:
<blockquote>
Is all this really necessary? (referring to effort invested in maximizing CSS selector performance)

The short answer is; probably not.
</blockquote>

Using selector chaining as prescribed by SymbioCSS trades a few milliseconds of parse/interpretation time for what could amount to many man hours saved on maintenance and iteration over time.

## Taking it further
This blog is clearly much more simplistic than what we are tasked with developing in the real world, so to demonstrate the scalability of SymbioCSS, let's start by adding some different categories of blog articles; let's add "Health" and "Sports" categories:

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

Instead of adding "health" or "sports" classes to each of our blog articles, we are taking advantage of the parent-child relationship of HTML tags to add this context (see CSS Rule #2 above). To style these new categories, we can add this CSS:

```CSS
.health.blog article {
  background: blue;
}

.sports.blog article {
  background: green;
}
```

Any article inside the "health blog" `section` will have a blue background, while articles inside the "sports blog" `section` will have a green background. The "health" or "sports" context *cascades* to the article tags.

This is a somewhat Object-Oriented approach to CSS. Here are just a few benefits:

1. Your style sheet will read like a list of clearly-defined references to HTML elements,
2. each CSS rule block will apply the minimum number of style rules necessary to style its *context*,
3. CSS selectors share style rules in the most efficient way possible (the cascade),
4. Specificity is inherently taken care of because of selector chaining,
5. Your style sheet will naturally become ordered from least-specific to most-specific (ala [ITCSS](http://itcss.io/)),
6. it will have the added benefit of being organized from one reusable component to the next (any of which could be abstracted into their own style sheet, or used inside a Web Component, etc.), and 
7. the chances of conflicts between components are practically nil due to the specificity introduced by selector chaining.

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

Most methodologies advise against using the `!important` flag, but the reasoning is usually something to the effect of "Using !important can lead to unexpected conflicts that are hard to manage." This is true in the absence of a structured approach, but when you follow logical patterns, it becomes a non-issue. In SymbioCSS, global modifier classes are the only case where the `!important` flag is used. 

In fact, this is in line with the original intent of the `!important` flag, which was to act as a guaranteed override of document styles so that users could establish their own customized style sheet (which can be used to enlarge fonts or change colors for those with vision troubles, for example).

SymbioCSS modifiers can also be scoped locally, in which case the `!important` flag is not needed. For example, let's say we want to mark certain blog articles as "featured". We can do so by adding a local modifier:

```HTML
<section class="blog">
  <article class="featured">
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
.blog article.featured {
  font-family: Wingdings;
}
```

Then, we can use Specificity to style "featured health blog articles" differently from "featured sports blog articles":

```CSS
.health.blog article.featured {
  text-shadow: 1px 1px 2px pink;
}

.sports.blog article.featured {
  text-shadow: 1px 1px 2px orange;
}
```

The key of this approach is *context*. As your style sheet grows in length, you'll find that its complexity remains low. These patterns stay consistent and repeatable throughout.

Next: [Structuring your Style Sheets &raquo;](03_structuring-your-style-sheets.md)

---
[&laquo; How to write HTML](01_html.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Structuring your Style Sheets &raquo;](03_structuring-your-style-sheets.md)
