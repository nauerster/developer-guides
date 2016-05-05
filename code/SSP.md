# Scalable SASS Patterns


## Blocks
Core components used to define the layout of your app.

```css

/**
 * common block styles
 *
 * .header
 * .content
 * .sidebar
 * .footer
 *
 **/

// block modifiers

.header
	{...}
	&--global
		{...}
	&--content
		{...}
	&--module
		{...}


.content
	{...}
	&--main
		{...}
	&--module
		{...}


.sidebar
	{...}
	&--left
		{...}
	&--right
		{...}


.footer
	{...}
	&--global
		{...}
	&--content
		{...}
	&--module
		{...}


```

## Elements
Minor componets, e.g. search, buttons, navs

```css

.header
	{...}
	&--global
		{...}


.header--global
	.user-login

```