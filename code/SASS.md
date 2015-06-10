# SASS

The main objective of this document is to expose some of today's Best Practices as well as introduce techniques that will keep your code Consistent, Organized, and Scalable. 

****

## Table of Content

1. [Getting Started](#getting-started)
2. [Fire It Up](#fire-it-up)
3. [File Organization](#file-organization)
4. [Methodologies & Principles](#methodologies-principles)
5. [Code Guidelines](#code-guidelines)
6. [Practical Examples](#practical-examples)

## Getting Started

#### Step 1: Install Dependencies
1. [node](http://nodejs.org/): follow the link and click the button
2. [ruby](https://www.ruby-lang.org/en/installation/): this comes pre-installed on macs
3. `gem install sass` & `gem install compass`
4. `npm install grunt` & `npm install grunt-cli`: installs grunt and grunt-cli globally.
5. `npm install -g bower` : installs bower globally (*optional*)

**Note:**

 - Depending on your permissions setup, you might need to prefix each command with `sudo` (use with caution)
 - All user level installs: `cd ~` will put you at your user level


#### Step 2: Clone Project

You'll need to clone this repository so that its on your local computer.

```
$ cd /path/to/your/repo
$ git clone https://mnetpbldev@bitbucket.org/mnetpbldev/styleguide.git (HTTPS Method)

```

#### Step 3: Know Your Git Commads
* `git add -A`: stages all files to commit (locally)
* `git commit -am "Commit message"`: commits all files with a description
* `git push origin {branch name}`: push committed files to repository
* `git branch {new branch}`: creates a new working branch
* `git checkout branch`: switches you to your new branch
* `git merge {branch name}` : will merge changes from the specified branch into your current branch 

## Fire It Up
Follow these instructions to fire up your `Sass Plate` after ensuring you have all dependencies listed above installed in your environment.

1. In terminal/Command line, navigate to the root directory (where Gruntfile.js is located)
	* Install Node Modules: `npm install`

2. In the same directory run the following command
	* `grunt serve`: css file will be output into the dev folder. The watch task will continue to run until you quit it `(ctrl + c)`.
	* `grunt build`: will run all the same dev tasks, but will compress our css file for final release.



## File Organization
In general, the CSS file organization should follow something like this:

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
  |   |   |-- + functions/                # ems to rems conversion, etc.
  |   |       | _index.sass               # imports for all function modules
  |   |       | _colors.scss              # color mapper
  |   |       | _units.scss               # ems to rems conversion
  |   |       | _layout.scss              # width calculations and depth mapping
  |   |
  |   |   |-- _global.sass                # global variables
  |   |   |-- _helpers.sass               # extension classes
  |   |   |-- _mixins.sass                # media queries, CSS3, etc.
  |   |   |-- _lib.sass                   # imports for third party styles
  |   |   |-- + lib/                      # third party styles
  |   |       | _pesticide.scss           # CSS pesticide
  |   |       | _animate.scss             # Cross-Browser animation library
  |   |
  |   |   + ie.sass                       # IE specific Sass file
  |   |   + styles.sass                   # primary Sass file
  |   |   + _shame.sass                   # because hacks happen
  |
  + node_modules/                         # repository for node modules 
  + bower.json                            # use to install third party dependencies
  + package.json                          # use to install grunt dependencies
  + Gruntfile.js                          # used to configure your grunt tasks
  + README.md                             # used to shared helpful information about the project
  + .gitignore                            # used to ignore certain files and/or directories when push to remote repo
  + .bowerrc                              # used to change the install location of your bower_components)
  + config.rb                             # Compass configuration file (optional)
  + Gruntfile.js                          # Grunt configuration & tasks
  + package.json                          # Grunt metadata & dependencies

```

## Methodologies & Principles

#### BEM: `Block`-`Element`-`Modifier`
Allows developers to create a simple naming convention helping make your CSS more modular and portable.

- Block: `the 'thing' - like a .menu`
- Element: `a child of the block - like .menu-item`
- Modifier: `a variation of the 'thing' - like .menu-vertical`

In some ways, ** BEM ** is similar to **OOP** `(Object-Oriented Programming).` It's a way of describing reality in code, a range of `patterns,` and a way of thinking about program entities regardless of programming languages being used.

**What constitutes BEM?**

- **Block:** A `block` is an independent entity, a "building block" of an application. A block can be either simple or compound (containing other blocks).

- **Element:** An `element` is a part of a block that performs a certain function. Elements are context-dependent: they only make sense in the context of the block they belong to.

- **Modifier:** A `modifier` is a property of a block or an element that alters its look or behavior.

****

#### OOCSS: `Object`-`Oriented`-`CSS`

A scalable, maintainable, semantic, and predictable approach to writing CSS.

****

#### SMACSS: `Scalable`-`Modular`-`Architecture`*for*`CSS`

The basics of SMACSS:

 - Base: applies to HTML, no class / id selectors
 - Layout: page sections (e.g., header, sidebar, footer, etc.)
 - Module: encapsulated modules, re-usable
 - State: override defaults or JS driven manipulations (e.g., .is-opened or .is-expanded)
 - Theme: optional, if theming is needed

****

#### DRY CSS: `Don't`-`Repeat`-`Your`-`CSS`

How DRY CSS works:

It comes down to 3 core principles.

- Group reusable css properties together
- Name these groups logically
- Add your selectors to the various css groups

Want more? Visit: [DRY Out Your SASS](http://alistapart.com/article/dry-ing-out-your-sass-mixins)

****

#### LIFT: `Locating`-`Identify`-`Flat`-`Try to stay DRY`

- Locating our code is easy
- Identify code at a glance
- Flat structure as long as we can
- Try to stay DRY (Don’t Repeat Yourself)

****

## Coding Guildlines


#### Naming Conventions

Following the [BEM](http://bem.info/method/definitions/) naming convention.

```
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

```
.pad-tb-sm {
	padding: 1rem 0; /* applies 16px padding to the Top and Bottom */
}

```

#### States:

When modifying elements based on states, us the `is-state` pre-qualifier. 

```
.is-open
  display: block !important

.is-closed,
  display: none !important

```

#### Variables:

```
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


```
/*
 * Example:
 */

$blue					: #1C84C6

$color__primary			: $blue

$color__primary--hover	: darken($color__primary, 10%)


```

#### Mixins:

```
=button

OR

=button-skin

```

#### Helpers:
Also know as `Placeholders`

```
%foobar

OR

%foo-bar

```


## Practical Examples


#### Variables:

Used to store global & local values, which are leveraged through Mixins and other parts of your code.

```
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

$color__link			: $blue
$color__link--hover		: darken($color__link, 5%)
$color__link--active	: darken($color__link, 10%)

/*
 * Constants
 */

$img-path				: 'folder/img/'

/*
 * Media Break Points
 */

$mobile                               : '(min-width: 321px)'
$mobile-landscape                     : '(min-width: 480px)'
$tablet                               : '(min-width: 768px)'
$desktop                              : '(min-width: 992px)'
$widescreen                           : '(min-width: 1200px)'


```


#### Mixins:

Appropriate when passing arguments

```

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
Will extend common CSS properties to other selectors without adding the additional CSS Selector Property.

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



#### Modifiers: (Single Responsibility Classes):

Not to be confused with `Placeholders`. SRC's (Single Responsibility Classes) should only be used within the Mark-Up.


```

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

```
 <div class='content'>I have padding.</div>
 <div class='content pad-tb-none'>I don't have padding.</div>

```


#### Implementing BEM in a main navigation block

```
<nav class="nav" role="navigation" aria-label="primary">
  <ul class="nav__list">
    <li class="nav__list__item">
      <a href="" class="nav__link"></a>
    </li>
    <li class="nav__list__item">
      <a href="" class="nav__link--active"></a>
    </li>
    <li class="nav__list__item">
      <a href="" class="nav__link"></a>
    </li>
  </ul>
</nav>

```

##### We could then write our Sass like this

```
.nav

  &__list

    &__item

  &__link

    &--active
    
```

##### Which would compile to...

```
.nav {
}
.nav__list {
}
.nav__list__item {
}
.nav__link {
}
.nav__link--active {
}

```


##Nesting


Generally, you want to avoid nesting more than 3 level's deep. While in your SASS file it might make perfect sense, when compiled, those nested child element become buried in a string of selector's making your css bloated and unmanageable – especially when talking about specificity.

**When is it okay to use nesting?**

```
.element
  /* Some CSS declarations */

  &:hover,
  &:focus
    /* More CSS declarations for hover/focus state */


  &:before
    /* Some CSS declarations for before pseudo-element */
```



## Credits


- [BEM Crew](https://bem.info/)
- [Scalable and Modular Architecture for CSS](http://smacss.com/book) (<abbr title="Scalable and Modular Architecture for CSS">SMACSS</abbr>) 


