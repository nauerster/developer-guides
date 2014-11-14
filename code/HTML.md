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

```
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

```
 <ul id="categories">
	<li class="item">Category 1</li>
	<li class="item">Category 2</li>
	<li class="item">Category 3</li>
 </ul>
```

###Naming Conventions
When assigning a class or id to a selector, name it based off the nature of what it is, rather than by what it looks like.

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

```
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>A Descriptive Title</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- Place favicon.ico and apple-touch-icon.png in the root directory -->
    <link rel="stylesheet" type="text/css" href="css/vendor.min.css" />
    <link rel="stylesheet" type="text/css" href="css/style.min.css" />
</head>
<body>
    <!--[if lt IE 7]>
    <p class="browsehappy">You are using an <strong>outdated</strong> browser. Please <a href="http://browsehappy.com/">upgrade your browser</a> to improve your experience.</p>
    <![endif]-->
    
    <header>
        <a id="logo" href="/">Site Title</a>
        <div id="slogan">Application Slogan</div>
        
        <nav>
            <!-- use nav tag if applicable -->
        </nav>
    </header>
    
    <section class="container">
        
        <article class="row">
        <div class="col-xs-12">
            <h3></h3>
            <p></p>
        </div>
        </article>
        
    </section>
    
    <!-- Google Analytics: change UA-XXXXX-X to be your site's ID -->
    <script>
    (function(b,o,i,l,e,r){b.GoogleAnalyticsObject=l;b[l]||(b[l]=
    function(){(b[l].q=b[l].q||[]).push(arguments)});b[l].l=+new Date;
    e=o.createElement(i);r=o.getElementsByTagName(i)[0];
    e.src='//www.google-analytics.com/analytics.js';
    r.parentNode.insertBefore(e,r)}(window,document,'script','ga'));
    ga('create','UA-XXXXX-X');ga('send','pageview');
    </script>
    <script src="js/vendor.min.js"></script>
    <script src="js/app-angular.min.js"></script>
    <script src="js/app.min.js"></script>
</body>
</html>

```



