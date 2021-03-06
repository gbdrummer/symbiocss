# SymbioCSS

[&laquo; Structuring Your Style Sheets](03_structuring-your-style-sheets.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Interfacing with JavaScript &raquo;](05_interfacing-with-javascript.md)

# Building Reusable Components

Now that you are familiar with the basic approach, let's explore how powerful it can be; Let's build a reusable component with a number of different interactions and states.

To construct a component with SymbioCSS, follow these steps:

1. Select an appropriate HTML tag.
2. Choose a descriptive name for the component and establish its default properties.
3. Choose descriptors for the component's states and establish their properties.
4. Choose descriptors for the component's variations and establish their properties. Then, repeat step 3 for any additional states accompanying these variations.
5. Add any additional HTML attributes as necessary.

The basic structure of the component looks like this:

```HTML
<{tag} class="[{variations}] {component} [{state}]" id="{javascript_hook}" {attributes}>
  ...
</{tag}>
```

Here's a simple example:

Let's say we are tasked with creating a UI that allows the user to edit a block of text. At the bottom, we need a "Save" button which will update in response to whether or not the save operation was successful.

First, we need to select an appropriate tag. Because this button does not redirect users to a new document or section of the current document, an `<a>` tag is not appropriate, so let's go with a `<button>` instead:

```HTML
<button>Save</button>
```

Now, let's come up with a name for this component. "Save Button" seems obvious. We know this component is a button thanks to the `<button>` tag, so let's use a class to add the remaining context:

```HTML
<button class="save">Save</button>
```

Let's establish our button's default properties with some CSS:

```CSS
button.save {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: .382em 1em;
  background: blue;
  color: white;
}
```

Great, now we've got a reusable "Save Button" component.

Next, let's think about what states we need. Let's say our design spec calls for two states aside from the default: a "Save Failed" state and a "Save Successful" state. For the fail state we want to show a warning icon and change the color of the button to red, and for the success state we want to show a checkmark icon and change the background to green. First, let's add the missing pieces to our component:

```HTML
<button class="save [successful] [failed]">
  <div class="icon"></div>
  Save
</button>
```
...and let's add the CSS:

```CSS
button.save .icon {
  display: none;
  width: 1.382em;
  height: 1.382em;
}

button.save.successful {
  background: green;
}

button.save.successful .icon {
  display: block;
  background-image: url("icons/checkmark.svg");
}

button.save.failed {
  background: red;
}

button.save.failed .icon {
  display: block;
  background-image: url("icons/warning.svg");
}
```

Now, all we have to do to change the state of this button is add classes "successful" or "failed". The Cascade and Specificity take care of the rest.

Now let's say we want to create a variation of this component. Let's add a "disabled" local modifier:

```HTML
<button class="[disabled] save [successful] [failed]">
  <div class="icon"></div>
  Save
</button>
```

```CSS
button.save.disabled {
  opacity: .382;
  pointer-events: none;
}
```

The properties of this modifier will cascade to all elements of this button regardless of which state is active at a given time. This is because we **only applied styles that are specific to the context** of each state and variation.

The final CSS for this component looks like this:

```CSS
button.save {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  
  padding: .382em 1em;
  
  background: blue;
  color: white;
}

button.save .icon {
  display: none;
  width: 1.382em;
  height: 1.382em;
}

button.save.successful {
  background: green;
}

button.save.successful .icon {
  display: block;
  background-image: url("icons/checkmark.svg");
}

button.save.failed {
  background: red;
}

button.save.failed .icon {
  display: block;
  background-image: url("icons/warning.svg");
}

button.save.disabled {
  opacity: .382;
  pointer-events: none;
}
```

The `.disabled` styles are placed last so that, due to the Cascade, they will override the `.sucessful` and `.failed` styles if they should include properties also applied by `.disabled`. When two rules have the same Specificity level, the later rule will always win out over the earlier one. 

This component can now be used anywhere! This structure is applicable to any form of componentization; React, Angular, Web Components, whatever you may be using, the built-in scoping of this structure will work. When you structure your entire project this way, you may be surprised at how it just simply works, with no unexpected conflicts. And you get the added benefit of HTML and CSS that are clean, semantic, and easy to understand by a large team of developers.

## Standardizing

There is also an ideal way to structure your Component-scoped CSS; While not absolutely necessary, it does produce the cleanest CSS possible, free of unecessary overrides, and it does so by following a simple mobile-first approach.

For example, consider this basic component:

```HTML
<a class="button">Enter the Danger Zone</a>
```

Let's say our hypothetical design specifies that this basic button should display inline with other buttons at viewport widths above 640px, and should fill the full width of the layout on smaller viewports.

To accomplish this, the ideal way of structuring the CSS would be as follows:

```CSS
.button {
  display: flex;
  margin: 0 0 1em;
  background-color: black;
  border-radius: .382em;
  color: white;
}

@media screen and (min-width: 640px) {
  .button {
    display: inline-flex;
    margin: 0 1em 0 0;
  }
}

```

This is a basic mobile-first approach; we specify default rules for the component at small screen sizes, then use a media query to add overrides for larger screen sizes.

Let's add a hover state to the button:

```CSS
.button {
  display: flex;
  margin: 0 0 1em;
  background-color: black;
  border-radius: .382em;
  color: white;
}

.button:hover {
  font-weight: bold;
  background-color: grey;
}

@media screen and (min-width: 640px) {
  .button {
    display: inline-flex;
    margin: 0 1em 0 0;
  }
}

```

The `:hover` ruleset goes after the mobile-first styles, but before the media query. This way, if we want to adjust the hover style at larger screen sizes, we can do so inside the media query, and the cascade will ensure the change is applied.

Let's also say we have two versions of this button, a "danger" button and a "safety" button. We can add a modifier class to accomplish this:

```CSS
.button {
  display: flex;
  margin: 0 0 1em;
  background-color: black;
  border-radius: .382em;
  color: white;
}

.button:hover {
  background-color: grey;
  font-weight: bold;
}

.danger.button {
  background-color: red;
}

.danger.button:hover {
  background-color: pink;
}

.safety.button {
  background-color: green;
}

.safety.button:hover {
  background-color: lightgreen;
}

@media screen and (min-width: 640px) {
  .button {
    display: inline-flex;
    margin: 0 1em 0 0;
  }
}

```

Here, we've "reset" the specificity level a couple times within this component. We're treating "danger buttons" and "safety buttons" as self-contained extensions of the main "button" component. By resetting the specificity, we're creating a new "Context" for each button type. To illustrate:

```CSS
<Component Context>

  <Context Level 1: "Button">
    .button {
      display: flex;
      margin: 0 0 1em;
      background-color: black;
      border-radius: .382em;
      color: white;
    }
	
    .button:hover {
      background-color: grey;
      font-weight: bold;
    }
		
    <Context Level 2a: "Danger Button">
      .danger.button {
        background-color: red;
      }
			
      .danger.button:hover {
        background-color: pink;
      }
    </Context Level 2a>
		
    <Context Level 2b: "Safety Button">
      .safety.button {
        background-color: green;
      }
			
      .safety.button:hover {
        background-color: lightgreen;
      }
    </Context Level 2b>
  </Context Level 1>
	
  @media screen and (min-width: 640px) {
    <Context Level 1: "Button">
      .button {
        display: inline-flex;
        margin: 0 1em 0 0;
      }
			
      <Additional Contexts />
    </Context Level 1>
  }

</Component Context>

```

This structure also readily applies to CSS preprocessors that allow for nesting of selectors. For example, an SCSS implementation of this component would look like this:

```SCSS
.button {
  display: flex;
  margin: 0 0 1em;
  background-color: black;
  border-radius: .382em;
  color: white;
	
  &:hover {
    background-color: grey;
    font-weight: bold;
  }
	
  &.danger {
    background-color: red;
		
    &:hover {
      background-color: pink;
    }
  }
	
  &.safety {
    background-color: green;

    &:hover {
      background-color: lightgreen;
    }
  }
	
  @media screen and (min-width: 640px) {
    display: inline-flex;
    margin: 0 1em 0 0;
  }
}
```

This structure creates perfect internal scoping for this component. It is deceptively powerful; In a larger component with additional HTML tags inside, it allows us to add many different modifiers to the top-level tag and then target elements inside in the context of the modifier class. It also allows us to freely add or remove components from our stylesheet without any conflicts whatsoever.

As the CSS specification develops, this approach will continue to work well moving forward. [CSS Nesting Module Level 3](http://tabatkins.github.io/specs/css-nesting/) will allow you to take advantage of nesting without the need for a CSS preprocessor.

---
[&laquo; Structuring Your Style Sheets](03_structuring-your-style-sheets.md) | [Table of Contents](https://github.com/gbdrummer/symbiocss) | [Interfacing with JavaScript &raquo;](05_interfacing-with-javascript.md)
