---
layout: post
title: BEM Basics
---

Being recently new to the wondrous world that is web development I think I was a little bit overwhelmed when I just started out. Beside the basic stuff I knew, there were so many tools, plugins and processors available to simplify my work that I didn't know where to begin.

Now after 4 years of work, I've found a middle ground and have settled on a few best practices that I think are worth sharing.
One of them is BEM. Which stands for Block, Element, Modifier, but more on that later. This methodology still helps me daily when I'm building new components for websites, because it forces me to approach this process in a modular and maintainable way.

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