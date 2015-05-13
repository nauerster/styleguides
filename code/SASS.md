# SASS

The main objective of this document is to expose some of today's Best Practices as well as introduce techniques that will keep your code Consistent, Organized, and of course - Scalable.


## Naming Conventions

A CSS class for an element is a `block name` and an `element name` separated by a hyphen.

```

// block
.menu

// element
.menu__item

// modifier
.menu--list or menu--tabbed

```

See [Styleguides > CSS](https://github.com/nauerster/styleguides) for more on .


**Classes & Modifiers:**

```
.notSoGood {}
	
.this-is-better {}

```

**States:**

When modifying elements based on states, us the "is-state" pre-qualifier. 

```

.is-open,
.is-visible,
.is-expanded
  display: block !important

.is-closed,
.is-hidden,
.is-collaspsed
  display: none !important


```


**Variables:**

```

// Descriptive Name

$variable

// Namespace Variable

$namespace__variable

// Namespace Modified Variable

$namespace__variable--modifier

// Example:

$blue					: #1C84C6

$color__primary			: $blue

$color__primary--hover	: darken($color__primary, 10%)

```

**Mixins:**

```
=button

OR

=button__skin

```

**Helpers:** Also know as 'Placeholders'

```
%foobar

OR

%foo-bar

```

**Variables:**

Used to store global & local values, which are leveraged through Mixins and other parts of your code.

```
// Create some descriptive colors:

$black                 : #000
$gray                  : #C2C2C2
$blue                  : #1C84C6

// Set some core colors:

$color__theme			: lighten($blue, 10%)
$color__default			: $gray
$color__primary			: darken($color__default, 10%)

// Set some core color states:

$color__link			: $blue
$color__link--hover		: darken($color-link, 5%)
$color__link--active	: darken($color-link, 10%)

// Define some constants:

$img-path				: 'folder/img/'

$media__mobile--sm		: '(max-width: 240px)'
$media__mobile--lg		: '(max-width: 320px)'
$media__tablet--sm		: '(max-width: 480px)'
$media__tablet--lg		: '(max-width: 768px)'
$media__screen--sm		: '(max-width: 992px)'
$media__screen--lg		: '(max-width: 1024px)'
$media__screen--xl		: '(max-width: 1200px)'

```


**Mixins:**

Appropriate when passing arguments

```

*** SASS ***

// Lets create a mixin for a common pattern seen when building out buttons 

=button__skin($clr, $bg)
  +transition(all 300ms linear)
  color: $clr
  border-color: darken($bg, 5%)
  background-color: $bg
  &:hover
    color: darken($clr, 5%)
    border-color: darken($bg, 10%)
    background-color: darken($bg, 5%)
		
*** CSS ***

.btn

	// add button styles here
  
  	// define modifier 
	&--default
    	+button__skin($white, $color__default)
    
*** CSS OUTPUT ***

.btn--default {
  -webkit-transition: all 300ms linear;
  transition: all 300ms linear;
  color: #FFF;
  border-color: #7b7b7b;
  background-color: #888888;
}

```

**Builders:** 

Will extend common CSS properties to other selectors without adding the additional CSS Selector Property. 

```

%icon
  transition: background-color ease .2s;
  margin: 0 .5em;

.icon--error
  @extend %icon
  /* error specific styles... */

.icon--info
  @extend %icon
  /* info specific styles... */


```

**Helpers (Single Responsibilty Classes):**

Not to be confused with *Placeholders. SRC's should only be used within the Mark-Up.


```

.ptb-none
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

***Example:***

```
 <div class='pull-left'></div>

```



## Nesting


Generally, you want to avoid nesting more than 3 level's deep. While in your SASS file it might make perfect sense, when compiled, those nested child element become buried in a string of selector's making your css bloated and unmanageable – especially when talking about specificity.

When is it okay to use nesting?

```

.element

  /* Some CSS declarations */
 
  &:hover,
  &:focus
  
    /* More CSS declarations for hover/focus state */

  &:before
  
    /* Some CSS declarations for before pseudo-element */

```


## Architecture

Based off [SMACSS](http://smacss.com/book/categorizing) "By categorizing CSS rules, we begin to see patterns and can define better practices around each of these patterns."

```

  + app/
  |
  | + sass/
  |   |
  |   | + base/                           # reset, typography, site-wide
  |   |   |-- _index.sass                 # imports for all base styles
  |   |   |-- _base.sass                  # base styles
  |   |   |-- _normalize.scss             # normalize v3.0.1
  |   |   |-- _reset.sass                 # reset v0.0.1
  |   |   |-- _helpers.sass               # single responsibilty classes 
  |   |   |-- _typography.sass            # core typography rules   
  |   |
  |   | + layout/                         # major components, e.g., header, footer etc.  
  |   |   |-- _index.sass                 # imports for all layout styles
  |   |   |-- _content.sass               # core content block's, e.g., .section, .container, .row, .content
  |   |   |-- _grid.sass                  # responsive grid system
  |   |   |-- _header.sass                # global header
  |   |   |-- _footer.sass                # global footer
  |   |
  |   | + modules/                        # minor components, e.g., buttons, widgets etc.
  |   |   |-- _index.sass                 # imports for all modules
  |   |   |-- _modal.sass                 # modal styles
  |   |   |-- + buttons/                  # button directory consist of decorators  
  |   |   |-- | _button.sass              # default build decorator
  |   |   |-- | _button-states.sass       # button states decorator, i.e., primary, success, warning etc.
  |   |   |-- | _button-sizes.sass        # button sizes decorators, e.g., small, large
  |   |   |-- | _button-types.sass        # button variable decorators, e.g., outlined, squared etc.
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
  |   |   |-- _functions.sass             # ems to rems conversion, etc.
  |   |   |-- _global.sass                # global variables
  |   |   |-- _builders.sass              # builder classes, i.e., extension classes
  |   |   |-- _mixins.sass                # media queries, CSS3, etc.
  |   |   |-- _lib.sass                   # imports for third party styles
  |   |   |-- + lib/                      # third party styles
  |   |       | _pesticide.scss           # CSS pesticide
  |   |       | _animate.scss             # Cross-Browser animation library
  |   |
  |   |   + ie.sass                       # IE specific Sass file
  |   |   + styles.sass                   # primary Sass file
  |   |   + _shame.sass                   # because hacks happen


```
 

## DRY SASS/CSS


## Credits

- [Scalable and Modular Architecture for CSS](http://smacss.com/book) (<abbr title="Scalable and Modular Architecture for CSS">SMACSS</abbr>)
- [BEM Crew](https://bem.info/)
- [Mina Markham](https://github.com/minamarkham) and her [Sassy Starter](https://github.com/minamarkham/sassy-starter)



