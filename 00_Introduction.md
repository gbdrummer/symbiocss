# SymbioCSS

[&laquo; Table of Contents](/symbiocss) | [HTML &raquo;](./01_html.md)

# Introduction

SymbioCSS is a methodology for writing HTML and CSS which I have developed over the last 3 years.

## Why another methodology?
In my opinion, a good HTML/CSS methodology should meet the following requirements:

HTML and CSS code should:

1. be clean and semantic.
2. be modular and composable.
3. employ consistent and repeatable patterns.
4. be easy to read and understand by any size team.

There are a number of very well-conceived methodologies out there, like OOCSS, SMACSS, and ITCSS. Unfortunately, despite their individual strengths, none of them meet all these requirements for me.

Over the last few years I've been faced with the challenge of building consistent, modern responsive UIs for a large suite of applications, all built on top of a very large, very old legacy code base. This code base included a single, 10,000-line css file constructed over the course of 10 years by a legion of different developers, all of whom had a different approach to HTML structure and naming conventions.

Cleaning all this up was a daunting task to say the least, but I'm happy to say the end result is a tried-and-true approach to HTML/CSS development that nails all four of my requirements and then some.

---

Quickly, here's how I'm defining HTML and CSS:

HTML is a markup language, or "a system for annotating a document in a way that is syntactically distinguishable from the text." ([Wikipedia](https://en.wikipedia.org/wiki/Markup_language)) This means HTML allows you to "mark up" your content, adding meaning and context, without polluting the content itself.

CSS is a style sheet language, or "a language that expresses the presentation of structured documents." It includes a feature called the Cascade, an algorithm defining how to combine property values originating from different sources. ([Wikipedia](https://en.wikipedia.org/wiki/Style_sheet_language))

**tl;dr the point of HTML is to annotate existing content to add meaningful context, and the point of CSS is to describe a document's presentation separately from its content.**

Without further ado, [on to the approach!](01 - HTML.md)

---
[&laquo; Table of Contents](./) | [HTML &raquo;](./01_html.md)
