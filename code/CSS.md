[![forthebadge](http://forthebadge.com/images/badges/uses-css.svg)](http://forthebadge.com)

# CSS



## Advanced Attribute Selectors

```
a[title] 								# Only selects anchor tags that have a title attribute
a[href="http://net.tuts.com"]			# Only selects anchor tags which link to http://net.tuts.com
a[href*="tuts"]							# The proceeding value must appear somewhere in the attribute's value
a[href^="http"]							# The proceeding value must appear at the beginning
a[href$=".jpg"]							# The proceeding value must appear at the end

```

**What if we want to select anchors with various image types: png, jpg, gif, etc?**

We could write the following...

```
a[href$=".png"],
a[href$=".jpg"],
a[href$=".gif"] {...}
```
Wait, we can do better than that! Let's write our own data attribute.

```
<a href="path/to/image.png" data-filetype="image">Image Link</a>
```
Now, with that hook in place, we can target every (or, only) those that have the above data attributes.

```
a[data-filetype="image"] {...}
```

In the same way, we could create a data attribute, which can receive a space-separated list of anything we want.

```
<a href="path/to/image.jpg" data-info="external image">View Image</a>
```
With the above in place, we could write...

```
a[data-info~="external"] {
	color: red;
}

a[data-info~="image"] {
	border: 1px solid black;
}
```