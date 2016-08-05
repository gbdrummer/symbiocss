# SymbioCSS
## CSS Document Structure

For ideally-functioning CSS, there is a particular structure that can be used. This structure ensures proper cascade and inheritance throughout your CSS file.

### Creating a Stylesheet
Modern UIs call for componentization; Small, encapsulated units of functionality and style that can be used and reused anywhere in your document. In order for these components to work reliably, any HTML, CSS, or JavaScript contained therein needs to be scoped to that component without leaking into the surrounding DOM. HTML and JavaScript can be scoped fairly easily, as can CSS if included inline, but if being loaded from a separate stylesheet more care is necessary.

CSS documents should be arranged by two criteria: Specificity and Component Context.

Rulesets should be ordered from least specific to most specific. In other words, your global, reusable styles go at the top of your stylesheet, and your more specific, component-scoped styles go toward the bottom. This is the approach of ITCSS and deserves to be considered best practice when following a modern approach to CSS.

However, there is an additional dimension to this when you enter the world of componentization; Since components are self-contained entities, they have a large amount of CSS that only applies to the component itself. For a UI with a large number of components, a stylesheet can start to become cluttered and difficult to follow if the ITCSS approach is followed correctly.

In SymbioCSS, the ITCSS approach to specificity is retained, but further broken down. Rather than structuring your entire stylesheet from least-specific to most-specific, SymbioCSS recommends breaking it up into components and applying the ITCSS method to those. This way you can organize your CSS and specificity in chunks instead of one monolithic stylesheet.

in other words, your stylesheet will look something like this:

```CSS
/* Global utility classes */
.hidden {
	display: none !important;
    visibility: hidden !important;
	opacity: 0 !important; 
}

.show {
	display: block !important;
    visibility: visible !important;
	opacity: 1 !important;
}

/* Component-specific styles */
/* Component 1 Context */
.component-1 {}

.component-1 .sub-component {}

.component-1.modifier .sub-component {}

/* Compoonent 2 Context */
.component-2 {}

.component-2 .sub-component {}

.component-2.modifier .sub-component {}

```

In the Component-specific styles section, notice how the specificity increases as you descend through the document, but "resets" when you move from one component to the next.

This approach is analogous to ITCSS in that if ITCSS structures CSS in an inverted triangle, SymbioCSS structures it more like an inverted Christmas Tree. This allows you to place your component CSS anywhere you wish in your CSS file, or add/remove components at will without worrying about scope conflicts.

### Creating a Component
There is also an ideal way to structure your Component-scoped CSS; While not absolutely necessary, it does produce the cleanest CSS possible, free of unecessary overrides, and it does so by following a simple mobile-first approach.

For example, consider this basic component:

```HTML
<a class="button">
	Enter the Danger Zone
</a>
```

Our design specifies that this basic button should display inline with other buttons at viewport widths above our "UI switch point" (the point at which our layout switches between a small-screen version and a larger-screen version) and should fill the full width of the layout on smaller viewports.

To accomplish this, the ideal way of structuring the CSS would be as follows:

```CSS
.button {
	display: inline;
	margin: 0 .618em 0 0;
	background-color: red;
    border-radius: .382em;
}

@media screen and (min-width: 640px) {
	.button {
    	display: block;
		margin: 0 0 .618em;
    }
}

```

This is a basic mobile-first approach; we specify default rules for the component at small screen sizes, then use a media query to add overrides for larger screen sizes.

Let's add a hover state to the button:

```CSS
.button {
	display: inline;
	margin: 0 .618em 0 0;
	background-color: red;
	border-radius: .382em;
}

.button:hover {
	font-weight: bold;
	background-color: pink;
}

@media screen and (min-width: 640px) {
	.button {
    	display: block;
		margin: 0 0 .618em;
    }
}

```

The pseudo-class declaration goes after the mobile-first styles, but before the media query. This way, if want to adjust the hover style at larger screen sizes, we can do so inside the media query, and the cascade will ensure the change is applied.

Let's also say we have two versions of this button, a "danger" button and a "safety" button. We can add a modifier class to accomplish this:

```CSS
.button {
	display: inline;
	margin: 0 .618em 0 0;
    border-radius: .382em;
}

.button:hover {
	font-weight: bold;
}

.danger.button {
	background-color: red;
}

.danger.button:hover {
	backround-color: pink;
}

.safety.button {
	background-color: green;
}

.safety.button:hover {
	background-color: lightgreen;
}

@media screen and (min-width: 640px) {
	.button {
    	display: block;
		margin: 0 0 .618em;
    }
}

```

Here, we've "reset" the specificity order a couple times within this component. That is because it makes sense to consider "danger buttons" and "safety buttons" as self-contained components. They are extensions of the main "button" component, and so they receive styles from it, but they then extend that component with their own styles. In other words, "danger" and "safety" buttons do not share styles with each other, but they do both share styles with the "button" component. By resetting the specificity, we're creating a new "Context" for each button type. To illustrate:

```CSS
/* <Component Context> */

/* <Context Level 1: "Button"> */
.button {
	display: inline;
	margin: 0 .618em 0 0;
	border-radius: .382em;
}

.button:hover {
	font-weight: bold;
}
/* </Context Level 1> */

/* <Context Level 2a: "Danger Button"> */
.danger.button {
	background-color: red;
}

.danger.button:hover {
	backround-color: pink;
}
/* </Context Level 2a> */

/* <Context Level 2b: "Safety Button"> */
.safety.button {
	background-color: green;
}

.safety.button:hover {
	background-color: lightgreen;
}
/* </Context Level 2b> */

/* Reset all contexts */
@media screen and (min-width: 640px) {
	/* <Context Level 1: "Button"> */
	.button {
    	display: block;
		margin: 0 0 .618em;
	}
	/* </Context Level 1> */
	
	/* <Additional Contexts /> */
}

/* Additional Media Queries reset all contexts */

/* </Component Context> */

```

This structure also readily applies to CSS preprocessors that allow for nesting of selectors. For example, an SCSS implementation of this component would look like this:

```SCSS
.button {
	display: inline;
	margin: 0 .618em 0 0;
	border-radius: .382em;
	
	&:hover {
		font-weight: bold;
	}
	
	&.danger {
		background-color: red;
		
		&:hover {
			backround-color: pink;
		}
	}
	
	&.safety {
		background-color: green;

		&:hover {
			background-color: lightgreen;
		}
	}
	
	@media screen and (min-width: 640px) {
		display: block;
		margin: 0 0 .618em;
	}
}
```

This creates perfect scoping of this component. It is deceptively powerful; In a larger component with additional HTML tags inside, it allows us to add many different modifiers to the top-level tag and then target elements inside based on it's context. It also allows us to freely add or remove components from our stylesheet without any conflicts whatsoever.



<!--

### Types of CSS Rules
CSS rules can effectively be broken into two categories: Structural and Visual.

Structural styles include rules that affect how the element behaves in relation to other elements in the document. Some examples of Structural CSS rules include Positioning, Box-Model, and Z-Index rules. 

Visual styles include anything that affects how an element is presented without affecting its relationship to the rest of the document. Some examples include background-color, box-shadows, font-size, etc.

-->

