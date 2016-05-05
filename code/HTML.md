[![forthebadge](http://forthebadge.com/images/badges/uses-html.svg)](http://forthebadge.com)

##Overview
This document contains guildelines for...

The main objectives of this document are to ensure:

1. code consistency:
2. best practices:


##Pillars of Front-end Development
1. Separation of presentation, content, and behavior.
2. Markup should be well-formed, semantically correct and generally valid.
3. Javascript should progressively enhance the experience.


##HTML5
HTML5 is a markup language used for structuring and presenting content for the World Wide Web and a core technology of the Internet. It is the fifth revision of the HTML standard and, as of December 2012, is a candidate recommendation of the World Wide Web Consortium (W3C). Its core aims have been to improve the language with support for the latest multimedia while keeping it easily readable by humans and consistently understood by computers and devices (web browsers, parsers, etc.). HTML5 is intended to subsume not only HTML 4, but also XHTML 1 and DOM Level 2 HTML.

###Doctype

A proper Doctype which triggers standards mode in your browser should always be used. Quirks mode should always be avoided.

A nice aspect of HTML5 is that it streamlines the amount of code that is required. Meaningless attributes have been dropped, and the DOCTYPE declaration has been simplified significantly. Additionally, there is no need to use CDATA to escape inline JavaScript, formerly a requirement to meet XML strictness in XHTML.

`
<!DOCTYPE html>
`

###Character Encoding
All markup should be delivered as UTF-8, as its the most friendly for internationalization. It should be designated in both the HTTP header and the head of the document.

Setting the character set using <meta> tags:

`<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />`

In HTML5, just do:

`<meta charset="utf-8">`

##General Guidelines
The following are general guidelines for structuring your HTML markup. Authors are reminded to always use markup which represents the semantics of the content in the document being created.

- Use actual P elements for paragraph delimiters as opposed to multiple BR tags.
- Make use of DL (definition lists) and BLOCKQUOTE, when appropriate.
- Items in list form should always be housed in a UL, OL, or DL, never a set of DIVs or Ps
- Use `<label></label>` fields to label each form field, the `for` attribute should associate itself with the input field, so users can click the labels. `cursor:pointer;` on the label is wise, as well.
- Do not use the size attribute on your input fields. The size attribute is relative to the font-size of the text inside the input. Instead use css width.
- Place an html comment on some closing div tags to indicate what element you're closing. It will help when there is lots of nesting and indentation.
- Tables shouldn't be used for page layout.
- Make use of THEAD, TBODY, and TH tags (and Scope attribute) when appropriate.


**Example:**

```html
 <table>
 	<thead>
		<tr>
			<th scope="col">Table header 1</th>
			<th scope="col">Table header 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Table data 1</td>
			<td>Table data 2</td>
		</tr>
	</tbody>
 </table>
```

- Always use title-case for headers and titles. Do not use all caps or all lowercase titles in markup, instead apply the CSS property `text-transform:uppercase/lowercase`.


###General Coding Principles
- Add CSS through external files, minimizing the # of files, if possible. It should always be in the HEAD of the document.
- Use the LINK tag to include your external files

`<link rel="stylesheet" type="text/css" href="styles.css" />`

- Do not use inline styles

`<p style="font-size: 12px; color: #FFFFFF">This is poor form, I say</p>`


- Elements that occur only once inside a document should use IDs, otherwise, use classes.

- Write selectors that are optimized for speed. Where possible, avoid expensive CSS selectors. For example, avoid the * wildcard selector and don't qualify ID selectors (e.g. `div#myid`) or class selectors (e.g. `table.results`.)


###Classes vs. IDs
You should only give elements an ID attribute if they are unique. They should be applied to that element only and nothing else. Classes can be applied to multiple elements that share the same style properties. Things that should look and work in the same way can have the same class name.

**Example:**

```html
 <ul id="categories">
	<li class="item">Category 1</li>
	<li class="item">Category 2</li>
	<li class="item">Category 3</li>
 </ul>
```

###Naming Conventions
When assigning a class or id to a selector, name it based off the nature of what it is, rather than by what it looks like.

See [CSS Styleguide](https://github.com/nauerster/styleguides/blob/master/code/CSS.md) for a more in depth look into proper naming conventions.

**Meaningful**...

`<p class="note-text"></p>`

`<p class="callout"></p>`


**Meaningless**...

`<p class="big-blue-text"></p>`


###Indentation
Indentation will be done with "soft tabs" using spaces, the tab equivalent should be set to 4 spaces.

###Readability vs Compression
During the development phase &ndash; whitespace and comments are encouraged, where appropraite. We will use Grunt Task Runner to remove any comments or whitespace, as well as minify and compress our files to be production ready.



##HTML5-Boilerplate

```html

<!doctype html>
<!--[if lt IE 7]><html class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]-->
<!--[if IE 7]><html class="no-js lt-ie9 lt-ie8"> <![endif]-->
<!--[if IE 8]><html class="no-js lt-ie9"> <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js gt-ie9"> <!--<![endif]-->
  <head>

    <!--

      Description: ...
      Stack: Javascript, Sass, CSS3, HTML5
      Version: 0.0.1
      Author: Your Name

    //-->

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <!-- #DNS prefetching -->
    <!-- http://csswizardry.com/2013/01/front-end-performance-for-web-designers-and-front-end-developers -->
    <link rel="dns-prefetch" href="//ajax.googleapis.com">
    <link rel="dns-prefetch" href="//use.typekit.net">
    <link rel="dns-prefetch" href="//google-analytics.com">

    <!-- #Asset Prefetching -->
    <!-- Fetch and Download Assets before requested by the user  -->
    <!-- http://csswizardry.com/2013/01/front-end-performance-for-web-designers-and-front-end-developers/#section:resource-prefetching -->
    <link rel="prefetch" href="">

    <!-- #Page Prefetching -->
    <!-- http://calendar.perfplanet.com/2012/speed-up-your-site-using-prefetching -->
    <link rel="prefetch" href="index.html">

    <title>Project Title</title>
    <meta name="description" content="">
    <meta name="robots" content="all">

    <!-- Mobile Metas -->
    <meta name="viewport" content="width=device-width, user-scalable=1, initial-scale=1, maximum-scale=1">
    <meta name="apple-mobile-web-app-capable" content="yes">

    <!-- MS Tap Highlight for Windows Phones -->
    <!-- The tag is specific to Internet Explorer 10 on Windows Phone, and does not apply to Internet Explorer 10 on Windows. -->
    <!-- http://stackoverflow.com/questions/7508100/webkit-tap-highlight-color-in-windows-phone -->
    <meta name="msapplication-tap-highlight" content="no">

    <!-- Place favicon.ico and apple-touch-icon.png in the root directory -->

    <!-- build:css css/vendor.css -->
    <link rel="stylesheet" href="bower_components/bootstrap/dist/css/bootstrap.css" />
    <link rel="stylesheet" href="bower_components/animate.css/animate.min.css" />
    <!-- endbuild -->

    <!-- build:css({.tmp,app}) css/style.css -->
    <link rel="stylesheet" href="css/styles.css">
    <!-- endbuild -->

  </head>
  <body>

    <!--[if lt IE 7]>
    <p class="browsehappy">You are using an <strong>outdated</strong> browser. Please <a href="http://browsehappy.com/">upgrade your browser</a> to improve your experience.</p>
    <![endif]-->
    <!-- Add your site or application content here -->


    <section class="container">
        
        <article class="row">

          <div class="wrapper">

            <h3>Heading</h3>
            <p>Content</p>

          </div>
          
        </article>
        
    </section>

    <!--[if lt IE 9]>
    <script src="bower_components/es5-shim/es5-shim.js"></script>
    <script src="bower_components/json3/lib/json3.min.js"></script>
    <![endif]-->

    <!-- build:js js/vendor.js -->
    <script src="bower_components/angular/angular.js"></script>
    <script src="bower_components/angular-ui-router/release/angular-ui-router.js"></script>
    <script src="bower_components/angular-ui-bootstrap-bower/ui-bootstrap-tpls.js"></script>
    <!-- endbuild -->

    <!-- build:js({.tmp,app}) js/app.js -->
    <script src="js/app.js"></script>
    <!-- Directives -->
    <!-- End Directives -->
    <!-- Models -->
    <!-- End Models -->
    <!-- endbuild -->

  </body>
</html>

```



