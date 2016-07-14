# SASS

The main objective of this document is to expose some of today's Best Practices as well as introduce techniques that will keep your code Consistent, Organized, and Scalable. 


## Table of Content

1. [Documentation](#documentation)
1. [File Organization](#file-organization)
1. [Methodologies & Principles](#methodologies-principles)
1. [Code Guidelines](#code-guidelines)
1. [Practical Examples](#practical-examples)


## Documentation

Using [SassDoc](http://http://sassdoc.com/), you can parse your source folder to grab documentation-specific comments. From there, it builds a data tree, that gets enhanced and filtered before being passed to the view.

1. In Terminal/Command-line, simply run `grunt sassdoc` at the root of your project directory.


## File Organization

> In general, the CSS file organization should follow something like this:

```sh
  + styles/
  |
  | + sass/
  |   |
  |   | + base/                           # reset, typography, site-wide
  |   |   |-- _index.sass                 # imports for all base styles
  |   |   |-- _base.sass                  # base styles
  |   |   |-- _normalize.scss             # normalize v3.0.1
  |   |   |-- _reset.sass                 # reset v0.0.1
  |   |   |-- _modifiers.sass             # single responsibility classes
  |   |   |-- _typography.sass            # core typography rules
  |   |
  |   | + layout/                         # major components, e.g., header, footer etc.
  |   |   |-- _index.sass                 # imports for all layout styles
  |   |   |-- _content.sass               # core content block's, e.g., .section, .container, .row, .content
  |   |   |-- _grid.sass                  # responsive grid system
  |   |   |-- _header.sass                # global header
  |   |   |-- _footer.sass                # global footer
  |   |   |-- _variables.sass             #
  |   |
  |   | + components/                     # minor components, e.g., buttons, widgets etc.
  |   |   |-- _index.sass                 # imports for all modules
  |   |   |-- _modal.sass                 # modal styles
  |   |   |-- _button.sass                # default build decorator
  |   |
  |   | + states/                         # js-based classes, alternative states e.g., success or error state
  |   |   |-- _index.sass                 # imports for all state styles
  |   |   |-- _states.sass                # state rules
  |   |   |-- _print.sass                 # print styles
  |   |   |-- _touch.sass                 # touch styles
  |   |
  |   | + themes/                         # (optional) separate theme files
  |   |   |-- theme.sass                  # rename to appropriate theme name
  |   |
  |   | + views/                          # (optional) separate view files
  |   |   |-- _index.sass                 # imports for all views styles
  |   |   |-- _view1.sass                 # specific view styles
  |   |   |-- _view2.sass                 # specific view styles
  |   |   |-- ...                         # more...
  |   |
  |   | + utilities/                      # non-CSS outputs (i.e. mixins, variables) & non-modules
  |   |   |-- _index.sass                 # imports for all mixins + global project variables
  |   |   |-- _fonts.sass                 # @font-face mixins
  |   |   |-- + functions/                # ems to rems conversion, etc.
  |   |       | _index.sass               # imports for all function modules
  |   |       | _colors.scss              # color mapper
  |   |       | _units.scss               # ems to rems conversion
  |   |       | _layout.scss              # width calculations and depth mapping
  |   |
  |   |   |-- _config.sass                # config variables
  |   |   |-- _colors.sass                # color variables
  |   |   |-- _typography.sass            # typography variables
  |   |   |-- _helpers.sass               # extension classes
  |   |   |-- _mixins.sass                # media queries, CSS3, etc.
  |   |   |-- _lib.sass                   # imports for third party styles
  |   |   |-- + lib/                      # third party styles
  |   |       | _pesticide.scss           # CSS pesticide
  |   |       | _animate.scss             # Cross-Browser animation library
  |   |
  |   |   + styles.sass                   # primary Sass file
  |   |   + _shame.sass                   # because hacks happen

```

## Methodologies & Principles

#### BEM: `Block`-`Element`-`Modifier`
> Allows developers to create a simple naming convention helping make your CSS more modular and portable.

- Block: represents the higher level of an abstraction or component (i.e., `the 'thing' - like a .menu`) 
- Element: represents a descendent of `.block` that helps form `.block` as a whole (i.e., `a child of the block - like .menu__item`)
- Modifier: represents a variation of the 'thing' (i.e., `a different state or version - like .menu--vertical`

In some ways, **BEM** is similar to **OOP** `(Object-Oriented Programming).` It's a way of describing reality in code, a range of `patterns,` and a way of thinking about program entities regardless of programming languages being used.

**What constitutes BEM?**

- **Block:** A `block` is an independent entity, a "building block" of an application. A block can be either simple or compound (containing other blocks).

- **Element:** An `element` is a part of a block that performs a certain function. Elements are context-dependent: they only make sense in the context of the block they belong to.

- **Modifier:** A `modifier` is a property of a block or an element that alters its look or behavior.

An **analogy** of how DEM classes work, might be:

```css

.person {}
.person--man {}
  .person__hand {}
  .person__hand--left {}
  .person__hand--right {}

```

The above example shows the basic object we’re describing is a person, and that a different type of person might be a man.
That person also has hands, which are sub-parts of the person `object`. Those sub-parts are different, one is left, the other is right.  

Using this approach, we can namespace our selectors based on their base objects and we can also communicate what job the selector does; is it a sub-component (__) or a variation (--)?





#### OOCSS: `Object`-`Oriented`-`CSS`

A scalable, maintainable, semantic, and predictable approach to writing CSS.



#### SMACSS: `Scalable`-`Modular`-`Architecture`*for*`CSS`

The basics of SMACSS:

 - Base: applies to HTML, no class / id selectors
 - Layout: page sections (e.g., header, sidebar, footer, etc.)
 - Module: encapsulated modules, re-usable
 - State: override defaults or JS driven manipulations (e.g., .is-opened or .is-expanded)
 - Theme: optional, if theming is needed



#### DRY CSS: `Don't`-`Repeat`-`Your`-`CSS`

How DRY CSS works:

It comes down to 3 core principles.

- Group reusable css properties together
- Name these groups logically
- Add your selectors to the various css groups

Want more? Visit: [DRY Out Your SASS](http://alistapart.com/article/dry-ing-out-your-sass-mixins)



#### LIFT: `Locating`-`Identify`-`Flat`-`Try to stay DRY`

- Locating our code is easy
- Identify code at a glance
- Flat structure as long as we can
- Try to stay DRY (Don’t Repeat Yourself)



## Coding Guildlines


#### Naming Conventions

Following the [BEM](http://bem.info/method/definitions/) naming convention.

```css
/*
 * block
 */
 
.menu

/*
 * element
 */
 
.menu__item

/*
 * modifier
 */
 
.menu--list or .menu--tabbed

/*
 * In Sass you could write:
 */

.menu
	width: 100%

	.menu__item
		color: #8A8A8A

	&--list
		.menu__item
			color: #F89406

	&--tabbed
		.menu__item
			color: #D15B47

/* 
 * Which would print:
 */

.menu {
  width: 100%;
}

.menu .menu__item {
  color: #8A8A8A;
}

.menu--list .menu__item {
  color: #F89406;
}

.menu--tabbed .menu__item {
  color: #D15B47;
}

```


#### Modifiers:

Standalone modifiers don't form part of an abstraction or a component, therefore don't follow a particular pattern.

```css

.pad-tb-sm {
	padding: 1rem 0; /* applies 16px padding to the Top and Bottom */
}

```

#### States:

When modifying elements based on states, us the `is-state` pre-qualifier. 

```css
.is-open
  display: block !important

.is-closed,
  display: none !important

```

#### Variables:

```css
/* 
 * Descriptive Name
 */

$variable

/* 
 * Namespace Variable
 */

$namespace__variable

/*
 * Namespace Modified Variable
 */

$namespace__variable--modifier
```


```css
/*
 * Example:
 */

$blue					: #1C84C6

$color__primary			: $blue

$color__primary--hover	: darken($color__primary, 10%)


```

#### Mixins:

```css
=button

/* OR */

=button-skin

```

#### Helpers:
Also know as `Placeholders`

```css
%foobar

/* OR */

%foo-bar

```


## Practical Examples


#### Variables:

> Used to store global & local values, which are leveraged through Mixins and other parts of your code.

```css
/*
 * Descriptive colors
 */

$black                 : #000
$gray                  : #C2C2C2
$blue                  : #1C84C6

/*
 * Theme colors
 * /

$color__primary                       : #424446
$color__primary--tinted               : tint($color__primary, 5%)
$color__primary--shaded               : shade($color__primary, 5%)

$color__accent                        : #FFAC5B
$color__accent--tinted                : tint($color__accent, 5%)
$color__accent--shaded                : shade($color__accent, 5%)

$color__secondary                     : #898E91
$color__secondary--tinted             : tint($color__secondary, 5%)
$color__secondary--shaded             : shade($color__secondary, 5%)

/*
 * States
 */

$color__link          : $blue
$color__link--hover		: darken($color__link, 5%)
$color__link--active	: darken($color__link, 10%)

/*
 * Constants
 */

$img-path				: 'folder/img/'

/*
 * Media Break Points
 */

$media__mobile--sm		: '(max-width: 240px)'
$media__mobile--lg		: '(max-width: 320px)'
$media__tablet--sm		: '(max-width: 480px)'
$media__tablet--lg		: '(max-width: 768px)'
$media__screen--sm		: '(max-width: 992px)'
$media__screen--lg		: '(max-width: 1024px)'
$media__screen--xl		: '(max-width: 1200px)'


```


#### Mixins:

> Appropriate when passing arguments

```css

/*
 * Lets create a mixin for a common pattern seen when building out buttons
 */

=button-skin($clr, $bg)
  +transition(all 300ms linear)
  color: $clr
  border-color: darken($bg, 5%)
  background-color: $bg
  &:hover
    color: darken($clr, 5%)
    border-color: darken($bg, 10%)
    background-color: darken($bg, 5%)
		
/*
 * In SASS you could then write
 */

.btn

	display: inline-block
	
	&--default
    	+button-skin($white, $color__default)
    
/* 
 * Which would print:
 */

.btn--default {
  -webkit-transition: all 300ms linear;
  transition: all 300ms linear;
  color: #FFF;
  border-color: #7b7b7b;
  background-color: #888888;
}

```

#### Helpers: 

> Will extend common CSS properties to other selectors without adding the additional CSS Selector Property.


```css
%icon {
  transition: background-color ease .2s;
  margin: 0 .5em;
}

.error-icon {
  @extend %icon;
  /* error specific styles... */
}

.info-icon {
  @extend %icon;
  /* info specific styles... */
}

```

> Potential use-cases for placeholders (i.e., helper classes)

```css

// Let's say I have a button component...
%button
  display: inline-block
  padding: 1rem
  border: 1px solid gray
  color: black
  background: #EFEFEF


// And I have a button group component that stacks all buttons inside
// and makes their backgrounds pink (for whatever reason)...
%buttonGroup
  display: block
  border: 2px solid gray

  
  // Here is where the inner buttons are changed.
  %button
    display: block
    background: pink

//------------------------------------
// In a separate file, far far away...
//------------------------------------

// I can change the selectors just in this place, and
// the relationship between buttons and buttonGroups are preserved
button, 
input[type=button], 
input[type=submit], 
.button 
  @extend %button

.buttonGroup 
  %buttonGroup

#epilogue
  content: 'Yes, placeholders have great potential to be misused, especially when it can easily be'
  content: 'substituted for a @mixin, but using placeholders for RELATIONSHIPS between'
  content: 'components is much, much simpler than using mixins.'


```

**More Info:**

 - [Hugo Giraudel](https://www.sitepoint.com/avoid-sass-extend/) 



#### Modifiers: (Single Responsibility Classes):

> Not to be confused with `Placeholders`. SRC's (Single Responsibility Classes) should only be used within the Mark-Up.


```css

.pad-tb-none
	padding-top: 0px !important
	padding-bottom: 0px !important

.pull-left
	float: left
	
.pull-right
	float: right
	
.clearfix
	&:before,
	&:after
		content: ''
		display: table
		clear: both

```

**Example:**

```html
 <div class='content'>I have padding.</div>
 <div class='content pad-tb-none'>I don't have padding.</div>

```



## Nesting


Generally, you want to avoid nesting more than 3 level's deep. While in your SASS file it might make perfect sense, when compiled, those nested child element become buried in a string of selector's making your css bloated and unmanageable – especially when talking about specificity.

**When is it okay to use nesting?**

```css
.element
  /* Some CSS declarations */

  &:hover,
  &:focus
    /* More CSS declarations for hover/focus state */


  &:before
    /* Some CSS declarations for before pseudo-element */
```



## Scalable SASS Patterns

- [Developer Guides - SASS Patterns](https://github.com/nauerster/developer-guides/blob/master/code/SSP.md)

## Credits


- [BEM Crew](https://bem.info/)
- [Scalable and Modular Architecture for CSS](http://smacss.com/book) (<abbr title="Scalable and Modular Architecture for CSS">SMACSS</abbr>) 

