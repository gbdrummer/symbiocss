[<< Table of Contents](https://github.com/gbdrummer/symbiocss)

# Introduction

SymbioCSS is an approach to writing HTML and CSS in a way that maintains separation of concerns while providing for symbiosis between the two technologies. It applies common patterns that allow for better organization and maintainability of User Interfaces.

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

HTML is specifically applied to writing web documents. 

**When writing HTML, what you are actually doing is annotating content to add meaningful context.**

### What CSS actually is
CSS stands for "Cascading Style Sheets." We all know what it is used for: styling web pages. But what *is* CSS?

CSS is a style sheet language, or "a language that expresses the presentation of structured documents."

CSS is specifically applied to documents written in a markup language. 

**When writing CSS, the whole point is to describe document presentation separately from document content.**

### What JavaScript actually is
JavaScript is a complete programming language. In the context of building a user interface for the web, it is used to add client-side behavior to HTML pages.

**JavaScript is NOT intended to replace or mimic the functions of HTML or CSS.**
