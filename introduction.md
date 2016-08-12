[<< Table of Contents](https://github.com/gbdrummer/symbiocss)

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
When building user interfaces, it is vitally important that we understand the intention and limitations of the tools we are using.  The tools of choice for writing user interfaces for the web are HTML, CSS and JavaScript. SymbioCSS focuses on HTML and CSS and the way they interface with JavaScript. **These three technologies will hereafter be collectively referred to as "The Big Three."**

### What HTML actually is
HTML stands for "Hyper Text Markup Language." We all know what it is used for: structuring web pages. But what *is* HTML?

HTML is a markup language, or "a system for annotating a document in a way that is *syntactically distinguishable* from its content." This means it allows you to "mark up" your content, adding meaning and context, without polluting the content itself.

HTML is specifically applied to writing web documents. 

**When writing HTML, what you are actually doing is annotating content to add meaningful context.**

### What CSS actually is
CSS stands for "Cascading Style Sheets." We all know what it is used for: styling web pages. But what *is* CSS?

CSS is a style sheet language, or "a language that expresses the presentation of structured documents."

CSS is specifically applied to documents written in a markup language. 

**When writing CSS, the whole point is to describe document presentation separately from document content.**

### What JavaScript actually is
JavaScript is a [Turing Complete](https://en.wikipedia.org/wiki/Turing_completeness) programming language. In the context of building a user interface for the web, it is used to add client-side behavior to HTML pages.

**JavaScript is NOT intended to replace or mimic the functions of HTML or CSS.**

## Creating symbiosis
**Symbiosis**: any interdependent or mutually beneficial relationship between two persons, groups, or web technologies (That last bit was added by us)

Maintaining separation of concerns is not just a dogma; it is necessary to allow each of The Big Three to work as intended. That said, none of The Big Three operate in a vacuum; they must work together, and they must do so in a *symbiotic* way.

There are numerous popular approaches to writing CSS, all of which have merit. However, none represent a cohesive approach to using The Big Three together in a way that minimizes friction. Some strip bulk from CSS and add it to HTML, some do the opposite. All introduce hard syntactic rules that require time and training to master. All target a particular demon, be it "bloat," "disorganization," or "repetition", to the exclusion of others.

That's where SymbioCSS comes in; it applies common patterns to HTML and CSS that solve many of the maintenance issues UI developers typically run into, and it does so by using the inherent functionality of HTML and CSS.
