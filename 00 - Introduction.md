# SymbioCSS

[&laquo; Table of Contents](https://github.com/gbdrummer/symbiocss) | [HTML &raquo;](01 - HTML.md)

---

# Introduction

SymbioCSS is an approach to writing HTML and CSS in a way that maintains separation of concerns (SOC) while providing for symbiosis between the two technologies. It applies common patterns that allow for better organization and maintainability of Web User Interfaces.

The key advantages of this approach:

- Makes HTML and CSS easily maintainable by any size development team, large or small:
	- Produces the cleanest, most semantic HTML possible
	- Negates specificity conflicts
	- Provides BEM-style namespacing without the ugly markup
	- All CSS selectors **read like English**
	- Works in any browser
- Designed for Componentization
- Modular and Scalable architecture

## Separation of concerns
When building user interfaces, it is vitally important that we understand the intention and limitations of the tools we are using.  The tools of choice for writing user interfaces for the web are HTML, CSS and JavaScript. **These technologies will hereafter be referred to as "The Big 3."**

### What HTML actually is
HTML stands for "Hyper Text Markup Language." We all know what it is used for: structuring web pages. But what *is* HTML?

HTML is a markup language, or "a system for annotating a document in a way that is *syntactically distinguishable* from its content." This means it allows you to "mark up" your content, adding meaning and context, without polluting the content itself. HTML is specifically applied to writing web documents. 

**tl;dr When writing HTML, what you are actually doing is annotating content to add meaningful context.**

### What CSS actually is
CSS stands for "Cascading Style Sheets." We all know what it is used for: styling web pages. But what *is* CSS?

CSS is a style sheet language, or "a language that expresses the presentation of structured documents." It includes a feature called the *Cascade*, an algorithm defining how to combine property values originating from different sources. CSS is specifically applied to documents written in a markup language.

**tl;dr When writing CSS, the whole point is to describe document presentation separately from document content.**

### What JavaScript actually is
JavaScript is a [Turing Complete](https://en.wikipedia.org/wiki/Turing_completeness) programming language. In the context of building a User Interface for the web, it is used to add client-side behavior to HTML pages.

**JavaScript is NOT intended to replace or mimic the functions of HTML or CSS.**

## Creating symbiosis
**Symbiosis**: any interdependent or mutually beneficial relationship between two persons, groups, or web technologies (That last bit was added by me).

Maintaining SOC is not just a dogma; it is necessary to allow each of The Big 3 to work as intended. That said, none of The Big 3 operate in a vacuum; they must work together, and they must do so in a *symbiotic* way.

There are numerous popular approaches to writing CSS, all of which have merit. However, none represent a cohesive approach to using The Big 3 together in a way that minimizes friction. Some strip bulk from CSS and add it to HTML, some do the opposite. Most introduce hard syntactic rules that require time and training to master. All target a particular demon, be it "bloat," "disorganization," or "repetition", often to the exclusion of others.

That's where SymbioCSS comes in; it applies common patterns to HTML and CSS that solve many of the maintenance issues UI developers typically run into, and it does so by using the inherent functionality of HTML and CSS.

---
[&laquo; Table of Contents](https://github.com/gbdrummer/symbiocss) | [HTML &raquo;](01 - HTML.md)

<!--
HTML elements with descriptors like "wrapper," "green" or "col-sm-3 col-md-6 col-lg-9 cf h30 main-container__header--v2" are not particularly conducive to communication amongst a team of developers. Any team member must be trained on what each of these descriptors mean, and even then it may not be entirely obvious which UI elements these descriptors refer to.

If you have seen our News Articles example and you are thinking "this looks an awful lot like BEM but less efficient," you are absolutely correct. This approach is not as efficient to parse as BEM due to the chained CSS selectors. 

However, it is entirely worth the added readability and maintainability of your code, especially if you are working with a large team. There is no specific syntax to learn, and besides, the amount of additional processing overhead required to parse the extra selectors is offset by the need for fewer selectors and declarations within. In fact, **this is how CSS was designed to work in the first place.**
-->
