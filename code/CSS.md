# CSS

The main objective of this document is to expose some of today's Best Practices as well as introduce techniques that will keep your code Consistent, Organized, and of course - Scalable.


## Codeing style


#### Spacing

- Use soft-tabs with a two space indent.
- Put spaces after : in property declarations.
- Put spaces before { in rule declarations.
- Put line breaks between rulesets.
- Seperate each class identifier with a dash/hyphen
- When grouping selectors, keep individual selectors to a single line - seperating them with a comma and a single space.
- Place closing braces of declaration blocks on a new line.
- Each declaration should appear on its own line for more accurate error reporting.

#### Formatting

- Use hex color codes #000 unless using rgba().
- Use // for comment blocks (instead of /\* comment */).
- Avoid specifying units for zero values, e.g., margin: 0; instead of margin: 0px;.
- Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values.
- As a rule of thumb, avoid unnecessary nesting in SASS/SCSS. At most, aim for three levels. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting).


**Quick Example:** More Below

```

.menu {
  width: 200px;
  height: auto;
}
.menu-item {
  width: 25px;
  height: 30px;
}


```


### Naming Conventions

Follow the [BEM](http://bem.info/method/definitions/) methodology.

#### BEM:
Allows developers to create a simple naming convention helping make your CSS more modular and portable.

- Block: `the 'thing' - like a .menu`
- Element: `a child of the block - like .menu-item`
- Modifier: `a variation of the 'thing' - like .menu-vertical`

In some ways, ** BEM ** is similar to ** OOP ** `(Object-Oriented Programming)`. It's a way of describing reality in code, a range of `patterns`, and a way of thinking about program entities regardless of programming languages being used.

**What constitutes BEM?**

- **Block:** A `block` is an independent entity, a "building block" of an application. A block can be either simple or compound (containing other blocks).

- **Element:** An `element` is a part of a block that performs a certain function. Elements are context-dependent: they only make sense in the context of the block they belong to.

- **Modifier:** A `modifier` is a property of a block or an element that alters its look or behavior.


**Example:**

CSS class for an element is a `block name` and an `element name` separated by a hyphen.

```

// block
.menu

// element
.menu-item

// modifier
.menu-list or menu-tabbed


// In Sass you could write:
// ===========================================

.menu
	width: 100%
	
	.menu-item
		color: #8A8A8A
		
	&-list
		.menu-item
			color: #F89406
			
	&-tabbed
		.menu-item
			color: #D15B47
		
		
		
// Which would print:
// ===========================================

.menu {
  width: 100%;
}

.menu .menu-item {
  color: #8A8A8A;
}

.menu-list .menu-item {
  color: #F89406;
}

.menu-tabbed .menu-item {
  color: #D15B47;
}



```

See [Styleguides](https://github.com/nauerster/styleguides) for more on Sass.



### Basic Formatting Examples


**Formatting your selectors:**

```

.notSoGood {}
	
.this-is-better {}

```

**Example of good basic formatting practices:**


```

.styleguide-format {
	color: #000;
	background-color: #000;
	border: 1px solid #0F0;
}

```

**Example of individual selectors getting their own lines:**


```

.multiple,
.classes,
.get-new-lines {
	display: block;
}

or

.multiple:before, .multiple:after
.classes:before, classes:after
.get-new-lines:before, get-new-lines:after {
	display: block;
}

```

**Avoid unnecessary shorthand declarations:**

```

.not-so-good {
	margin: 0 0 20px;
}
.good {
	margin-bottom: 20px;
}

```

### Specificity (classes vs. ids)


Elements that occur exactly once inside a page should use IDs, otherwise, use classes. When in doubt, use a class name.

* Good candidates for ids: header, footer, modal popups.
* Bad candidates for ids: navigation, item listings, item view pages (ex: issue view).

When styling a component, start with an element + class namespace (prefer class names over ids), prefer direct descendant selectors by default, and use as little specificity as possible.

**Example:**

```

<ul class="category-list">
	<li class="item">Category 1</li>
	<li class="item">Category 2</li>
	<li class="item">Category 3</li>
</ul>

.category-list {}

// Direct descendant selector > for list items

.category-list > li {
	list-style-type: disc;
}

// Minimal specificity for all links

.category-list > li a {
	color: #F00;
}

```

## Credits:

- [BEM Crew](http://bem.info/authors/)
- [Jonathan Snook](http://smacss.com/book) - Author of SMACSS
- [Harry Roberts](http://cssguidelin.es/)