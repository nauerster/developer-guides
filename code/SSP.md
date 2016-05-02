# Scalable SASS Patterns


## Blocks
Core components used to define the layout of your app.

```

// common block styles

.header
.content
.sidebar
.footer


// block modifiers

.header
	{...}
	&-global
		{...}
	&-content
		{...}
	&-module
		{...}


.content
	{...}
	&-main
		{...}
	&-module
		{...}


.sidebar
	{...}
	&-left
		{...}
	&-right
		{...}


.footer
	{...}
	&-global
		{...}
	&-content
		{...}
	&-module
		{...}


```

## Elements
Minor componets, e.g. search, buttons, navs

```

.header
	{...}
	&-global
		{...}


.header-global
	.user-login

```