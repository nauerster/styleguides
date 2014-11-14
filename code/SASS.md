##Overview

The main objectives of this document are to ensure:

1. code consistency:
2. best practices:

##Naming Conventions


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

##Models


**Variables:**
Used to store global & local values, which are leveraged through Mixins.

```
//Theme Colors

$theme: #C3D603
$primary: #000
$secondary: #E0E1DD

//Paths

$img-path: 'folder/img/'

//Media Break Points

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



##Nesting

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





`
Example of Highlighted Text
`



- List Item
- List Item


**Example:**


##DRY SASS/CSS







##Architecture



