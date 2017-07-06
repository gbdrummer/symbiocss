# SymbioCSS

[&laquo; Table of Contents](https://github.com/gbdrummer/symbiocss) | [How to write HTML &raquo;](01_html.md)

# Introduction

SymbioCSS is a methodology for writing HTML and CSS which I (Graham Butler) have been developing since 2014.

## Why another methodology?
In my opinion, a good HTML/CSS methodology is one that produces code that is:

1. clean and semantic,
2. modular and composable,
3. patterned in a consistent, repeatable way, and is
4. easy to read and understand by any size team.

There are a number of very well-conceived methodologies out there, like [OOCSS](https://github.com/stubbornella/oocss/wiki), [SMACSS](https://smacss.com/), and [ITCSS](http://itcss.io/). Unfortunately, despite their individual strengths, none of them satisfy all of the above for me.

Since 2014 I've been presented with the challenge of building consistent, modern responsive UIs for a large suite of applications, powered by a very large, very old code base. This legacy code base included a single, 12,000-line css file constructed over the course of 10 years by a legion of different developers, all of whom used their own methods.

Cleaning all this up was a daunting task to say the least, but I'm happy to say the end result is a tried-and-true approach to HTML/CSS development that nails all four of my requirements and then some.

---

Quickly, here's how I'm defining HTML and CSS:

HTML is a markup language, or "a system for annotating a document in a way that is syntactically distinguishable from the text." ([Wikipedia](https://en.wikipedia.org/wiki/Markup_language)) This means HTML allows you to "mark up" your content, adding meaning and context, without polluting the content itself.

CSS is a style sheet language, or "a language that expresses the presentation of structured documents." It includes a feature called the Cascade, an algorithm defining how to combine property values originating from different sources. ([Wikipedia](https://en.wikipedia.org/wiki/Style_sheet_language))

**tl;dr the point of HTML is to annotate existing content to add meaningful context, and the point of CSS is to describe a document's presentation separately from its content.**

Without further ado, [on to the approach!](01_html.md)

---
[&laquo; Table of Contents](https://github.com/gbdrummer/symbiocss) | [How to write HTML &raquo;](01_html.md)
