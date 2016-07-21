---
layout: post
title: BEM Basics
---

Being recently new to the wondrous world that is web development I think I was a little bit overwhelmed when I just started out. Beside the basic stuff I knew, there were so many tools, plugins and processors available to simplify my work that I didn't know where to begin.

Now after 4 years of work, I've found a middle ground and have settled on a few best practices that I think are worth sharing.
One of them is **BEM**. Which stands for Block, Element, Modifier, but more on that later. This methodology still helps me daily when I'm building new components for websites, because it *forces* me to approach this process in a modular and maintainable way.

## Which does what?

The code structure for BEM is quite simple. When written out it looks a bit like this `.block__element--modifier`. You've got the following flavors to choose from:

### Blocks: 

A block is an isolated component that can be reused throughout your site. Blocks are usually not modified by other blocks that surround them.

### Elements:

These are the component parts of the block that you're building. They add contextual meaning to the parts that make up your block which leads you to quicker recognize them when writing code.

### Modifiers:

Lastly, modifiers. These are a bit odd, in that they can modify both blocks as a whole, but also elements within a block. The syntax remains the same however.

## What it looks like

Since this is a relatively abstract discription I've written a small example to help you wrap your head around this abstraction. This example is written in SASS.

Consider this markup:

``` html
<div class='block block--modifier'>
	<span class='element element--modifier'></span>
	<span class='element'></span>
</div>
```

We could write this SCSS for it:

``` scss
/**
 * Block description
 */
.block {
	display: block;
	position: relative;
	
	&__element {
		display: inline-block;
		margin-right: 5px;
		
		&--modifier {
			margin-right: 10px;
		}
	}
	
	&--modifier {
		background-color: #f2f2f2;
	}
}
```

Which will translate to:

```
.block {
	display: block;
	position: relative;
}

.block__element {
	display: inline-block;
	margin-right: 5px;
}

.block__element--modifier {
	margin-right: 10px;
}

.block--modifier {
	background-color: #f2f2f2;
}
```

As you can see, the generated CSS is not nested and so all the classes that make up the styling of our block and its component parts are on the same specificity level. This is very useful, because it means that we can actually use the cascading nature of CSS in a predictable way.

## File structure

To get the most out of BEM I think it is useful to have a file structure that follows the same structured way of thinking. I usually use this as a rough setup of my SASS folder.

```
style.scss
_reset.scss
_variables.scss
_mixins.scss
_fonts.scss
_components.scss
|_ component (folder)
	|_ _block.scss
	|_ _another.scss
_utilities.scss
_shame.scss
```

The main file is normally style.scss, a file that everything gets imported into. The first import will always be a type of reset file, which smooths out bumps in browser default behaviour.

After that come my variables and mixins, which can be used throughout the rest of the code, so they need to be in front. 

Since I tend to work with font icons and custom fonts often, I like to have all styles related to that in a font.scss file.

Now for the most important file: `_components.scss`. This file imports all my components which get saved in the components folder. The filename for these components is usually the same as the blockname. This makes it easy to find a component back, even without the use of maps.

After components I tend to import `_utilities.scss`. This file contains a collection of classes that style one or two attributes at most at a time. As an additional identifier, any attribute set in a utility class could have `!important` assigned to it. Since these utilities are imported after the components, and because the use of BEM has made our specificity tree very flat, this probably won't be necessary.

The last part is `_shame.scss`. This file contains all the things that couldn't be styled in a desirable way, either because of code that needed to remain the same, or because of an ugly hack elsewhere in the code. The goal for this file is to be as empty as possible and if at all possible, completely empty.