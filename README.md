# SymbioCSS

> This repo is getting a bit long in the tooth, but I think there are still some valid ideas to be found in it. So, I'm leaving it here for anyone who may find it useful as a learning tool.

SymbioCSS is a methodology for writing scalable, composable and maintainable HTML and CSS which I (Graham Butler) have been developing since 2014.

## Why another methodology?
In my opinion, a good HTML/CSS methodology is one that produces code that is:

1. clean and semantic,
2. modular and composable,
3. patterned in a consistent, repeatable way, and is
4. easy to read and understand by any size team.

There are a number of very well-conceived methodologies out there, like [OOCSS](https://github.com/stubbornella/oocss/wiki), [SMACSS](https://smacss.com/), and [ITCSS](http://itcss.io/). Unfortunately, despite their individual strengths, none of them satisfy all of the above for me.

From 2014 to 2018 I was challenged with building consistent, modern responsive UIs for a large suite of applications, powered by a very large, very old code base. This legacy code base included a single, 12,000-line css file constructed over the course of 10 years by a legion of different developers, all of whom employed their own unique approaches.

Cleaning all this up was a daunting task to say the least, but I'm happy to say the end result is a tried-and-true approach to HTML/CSS development that nails all four of my requirements and then some.

---

Quickly, here's how I'm defining HTML and CSS:

HTML is a markup language, or "a system for annotating a document in a way that is syntactically distinguishable from the text." ([Wikipedia](https://en.wikipedia.org/wiki/Markup_language)) This means HTML allows you to "mark up" your content, adding meaning and context, without polluting the content itself.

CSS is a style sheet language, or "a language that expresses the presentation of structured documents." It includes a feature called the Cascade, an algorithm defining how to combine property values originating from different sources. ([Wikipedia](https://en.wikipedia.org/wiki/Style_sheet_language))

**tl;dr the point of HTML is to annotate existing content to add meaningful context, and the point of CSS is to describe a document's presentation separately from its content.**

Without further ado, on to the approach!

## Table of Contents

1. [How to write HTML](./01_html.md)
2. [How to write CSS](./02_css.md)

### Building UIs
3. [Structuring your Stylesheets](./03_structuring-your-style-sheets.md)
4. [Building Reusable Components](./04_building-reusable-components.md)
5. [Interfacing with JavaScript](./05_interfacing-with-javascript.md)

### Example Code (Coming Soon!)
6. Boilerplate
7. A Basic Website
8. Chassis Framework
