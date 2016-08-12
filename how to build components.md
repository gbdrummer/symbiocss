# How to build components

When building composable components for UI, two perspectives must be considered; Internal and External Context. In other words, the developer must plan for how the internal parts of a component are presented, and for how the component itself interacts with the larger document. To cover for both perspectives, a very simple basic structure can be used:

```HTML
<{tag} class="[{variations}] {component} [{state}]" id="{javascript_hook}" {attributes}>
	...
</{tag}>
```

To construct a component, follow these steps:

1. Select an appropriate HTML tag
2. Choose a descriptive name for the component that is semantic to the user context and establish its default properties
3. Choose descriptors for the component's states and establish their properties
4. Choose descriptors for the component's variations and establish their properties. Then, repeat step 3 for any additional states accompanying these variations
5. Add any additional HTML attributes as necessary

Here's a simple example:

Let's say we have a basic UI for editing a block of text. At the bottom, we have a "Save" button. When the user clicks the button, its state changes to show whether or not the save operation was successful. Let's build this button:

First, we select an appropriate tag. Because this button does not redirect users to a new document or section of the current document, an `<a>` tag is not appropriate, so let's go with a `<button>` instead:

```HTML
<button>
	Save
</button>
```

Now, let's come up with a name for this component. "Save Button" seems obvious. We know this component is a button thanks to the `<button>` tag, so let's use a class to add the remaining context:

```HTML
<button class="save">
	Save
</button>
```

Let's establish our button's default properties with some CSS:

```CSS
button.save {
	display: inline-flex;
	justify-content: center;
    align-items: center;
    
	padding: 0 1em;
	line-height: 1.618em;
    
	background: blue;
    color: white;
}
```

Great, now we've got a reusable "Save Button" component.

Next, let's think about what states we need. Let's say our design spec calls for two states aside from the default: a "Save Failed" state and a "Save Successful" state. For the fail state we want to show a warning icon and change the color of the button to red, and for the success state we want to show a checkmark icon and change the background to green. First, let's add the missing pieces to our component:

```HTML
<button class="save [successful] [failed]">
	<img class="fail icon" src="icons/warning.svg" />
    <img class="success icon" src="icons/checkmark.svg" />
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

button.save.successful .success.icon {
	display: inline-block;
}

button.save.failed {
	background: red;
}

button.save.failed .fail.icon {
	display: inline-block;
}
```

Now, all we have to do to change the state of this button is add classes "successful" or "failed". The CSS cascade takes care of the rest.

Now let's say we want to create a variation of this component. There may be times when Saving is disabled in our app, so let's create a local modifier for that:

```HTML
<button class="[fancy] save [successful] [failed]">
	<img class="fail icon" src="icons/warning.svg" />
    <img class="success icon" src="icons/checkmark.svg" />
	Save
</button>
```

```CSS
button.fancy.save {
	font-family: cursive;
}
```

The properties of this modifier will cascade to all elements of this button regardless of which state is active at a given time.

The final HTML/CSS for this component looks like this:

```HTML
<button class="[fancy] save [successful] [failed]">
	<img class="fail icon" src="icons/warning.svg" />
    <img class="success icon" src="icons/checkmark.svg" />
	Save
</button>
```
```CSS
button.save {
	display: inline-flex;
	justify-content: center;
    align-items: center;
  
	padding: 0 1em;
	line-height: 1.618em;
  
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

button.save.successful .success.icon {
	display: inline-block;
}

button.save.failed {
	background: red;
}

button.save.failed .fail.icon {
	display: inline-block;
}

button.fancy.save {
	font-family: cursive;
}
```

---

This component can now be used anywhere! This structure is applicable to any form of componentization; React, Angular, Web Components, whatever you may be using, the built-in scoping of this structure will work. When you structure your entire project this way, you may be surprised at how it just simply works, with no unexpected conflicts. And you get the added benefit of HTML and CSS that are clean, semantic, and easy to understand by a large team of developers.


