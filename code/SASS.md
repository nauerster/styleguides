# SASS

The main objective of this document is to expose some of today's Best Practices as well as introduce techniques that will keep your code Consistent, Organized, and of course - Scalable.


## Naming Conventions

A CSS class for an element is a `block name` and an `element name` separated by a hyphen.

```

// block
.menu

// element
.menu-item

// modifier
.menu-list or menu-tabbed

```

See [Styleguides > CSS](https://github.com/nauerster/styleguides) for more on .


**Classes & Modifiers:**

```
.notSoGood {}
	
.this-is-better {}

```


**Variables:**

```
$variable

OR

$variable-name

```

**Mixins:**

```
=mixin

OR

=mixin-name

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
$color-theme			: rgba(88,195,240,1)
$color-primary			: rgba(34,34,34,1)
$color-secondary		: lighten($color-primary, 10)

$color-link				: rgba(16,187,241,1)
$color-link-hover		: lighten($color-link, 10)
$color-link-active		: darken($color-link, 10)

$img-path				: 'folder/img/'

$mobile-sm				: '(max-width: 240px)'
$mobile-lg				: '(max-width: 320px)'
$tablet-sm				: '(max-width: 480px)'
$tablet-lg				: '(max-width: 768px)'
$screen-sm				: '(max-width: 992px)'
$screen-lg				: '(max-width: 1024px)'
$screen-xl				: '(max-width: 1200px)'

```


**Mixins:**

Appropriate when passing arguments

```

*** SASS ***

=position($position: 'rel')
	@if $position == 'abs'
		position: absolute
	@else if $position == 'rel'
		position: relative
	@else if $position == 'fix'
		position: fixed
		
*** CSS ***

.block
	+position(abs)


*** OUTPUT ***

.block {
	position: absolute;
}

```

**Helpers:** Will extend common CSS properties to other selectors without adding the additional CSS Selector Property. 

```

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


**Modifiers:**

Not to be confused with *Placeholders. Modifiers should only be used within the Mark-Up.


```

.padding-tb-none
	padding-top: 0px !important
	padding-bottom: 0px !important

.pull
	float: left
	
.push
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
 <div class='pull'></div>

```



## Nesting


Generally, you want to avoid nesting more than 3 level's deep. While in your SASS file it might make perfect sense, when compiled, those nested child element become baried in a string of selector's making your css bloated and unmanagable – especially when talking about specificity.

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
  |   |
  |   | + layout/                         # major components, e.g., header, footer etc.
  |   |   |-- _index.sass                 # imports for all layout styles
  |   |   |-- _grid.sass                  # responsive grid system
  |   |   |-- _header.sass                # global header
  |   |   |-- _footer.sass                # global footer
  |   |
  |   | + modules/                        # minor components, e.g., buttons, widgets etc.
  |   |   |-- _index.sass                 # imports for all modules
  |   |   |-- _modal.sass                 # modal styles
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
  |   |   |-- _login.sass                 # specific view styles
  |   |   |-- _dashboard.sass             # specific view styles
  |   |   |-- ...                         # more...
  |   |
  |   | + utilities/                      # non-CSS outputs (i.e. mixins, variables) & non-modules
  |   |   |-- _index.sass                 # imports for all mixins + global project variables
  |   |   |-- _fonts.sass                 # @font-face mixins
  |   |   |-- _functions.sass             # ems to rems conversion, etc.
  |   |   |-- _global.sass                # global variables
  |   |   |-- _helpers.sass               # placeholder helper classes
  |   |   |-- _mixins.sass                # media queries, CSS3, etc.
  |   |   |-- _lib.sass                   # imports for third party styles
  |   |   |-- + lib/                      # third party styles
  |   |       | _pesticide.scss           # CSS pesticide
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



