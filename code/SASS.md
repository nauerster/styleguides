## Overview

#####The main objective of this document is to ensure our code is...
- Organized
- Consistent
- Scalable
- And follows Best Practices


<br />
## Naming Conventions
****

<br />
**Classes & Modifiers:**



```
.namespace (namespace = parent elem)
.namespace-block (block = child elem)
.namespace-block-sibling / .namespace-block-modifier

OR

.block
.block-name
.block-name-modifier

```

**Variables:** Camel Case

```
$variableName

```

**Mixins:**

```
=mixin-name

OR

=_mixin-name

```

**Placeholders:**

```
%placeholder-name
```

<br />
## Models
****

**Variables:**
Used to store global & local values, which are leveraged through Mixins and other parts of your code.

```
$colorTheme: rgba(88,195,240,1)
$colorPrimary: rgba(34,34,34,1)
$colorSecondary: lighten($colorPrimary, 10%)

$link: rgba(16,187,241,1)
$linkHover: lighten($link, 10%)
$linkActive: darken($link, 10%)

$img-path: 'folder/img/'

$break-xs:	'(max-width: 320px)'
$break-sm: 	'(max-width: 480px)'
$break-md: 	'(max-width: 768px)'
$break-lg: 	'(max-width: 992px)'
$break-xl:	'(max-width: 1200px)'

```


**Mixins:**
Appropriate when passing arguments

```
*** SASS ***

=_position($position: 'rel')
	@if $position == 'abs'
		position: absolute
	@else if $position == 'rel'
		position: relative
	@else if $position == 'fix'
		position: fixed
		
*** CSS ***

.block
	+_position(abs)


*** OUTPUT ***

.block {
	position: absolute;
}

```

**Placeholders:** Will extend common CSS properties to other selectors without adding the additional CSS Selector Property. 

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


<br />
##Nesting
****

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


<br />
##Architecture
****


#####SMACSS (Scalable and Modular Architecture for CSS)

Written by: _Jonathan Snook_

At the very core of [SMACSS](http://smacss.com/book/categorizing) is categorization. By categorizing CSS rules, we begin to see patterns and can define better practices around each of these patterns.

 





*****
###ToDo:
DRY SASS/CSS


