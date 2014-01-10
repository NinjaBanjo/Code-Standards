# Walker Art Center HTML Code Style Guide
----

## Introduction
*This style guide covers how HTML code should be styled in development, including template engines. It aims at improving collaboration, code quality, and enabling supporting infrastructure. It applies to raw, working files that use HTML. Tools are free to obfuscate, minify, and compiles as long as the general code quality is maintained.*

Template Engine style requirements are at the bottom.

## Browser Support
The Walker officially supports the three latest versions of the following browsers *(although some applications may only be built for specific browsers)*:

* Chrome
* Firefox
* Safari
* Internet Explorer (Currently 11, 10, 9)

We also try our best to test on different iOS & Android browsers.


---
## General Style Rules
### Protocol
Omit the protocol from embedded resources, this makes the URL relative--preventing mixed content issues, as well as results in minor file size savings. Do this, unless the files are not available over both https & http.

	<!-- No -->
	<script src="https://code.jquery.com/script.js"></script>
	
	<!-- Yes -->
	<script src="//code.jquery.com/script.js"></script>

### Images vs. CSS
For styles you can replicate via CSS: arrows, drop shadows, rounded corners. Please use CSS unless you cannot replicate the style at any close approximation.

---
## General Formatting
### Indentation
Indent by 2 spaces at a time, do not use tabs or mix tabs and spaces for indentation

	<ul>
	  <li>Awesome</li>
	  <li>Still Awesome</li>
	</ul>

### Capitalization
Use lowercase on the following: HTML element names, attributes, attribute values (unless text/CDATA), property values (unless strings), properties, CSS selectors.

You should use CamalCase on IDs.

	<!-- No -->
	<A HREF="/" CLASS="LINK" ID="homePAGE">Home</A>
	
	<!-- Yes -->
	<a href="/" class="link" id="HomePage">Home</a>

### Trailing Whitespace
Remove it, as it complicates diffs and is unnecessary.

---
## General Meta Rules
### Encoding
UTF-8, without a byte order mark, is required. Nothing else allowed.
Specify the encoding in the head of HTML documents via
	
	<meta charset="utf-8">
	
Do not specify the encoding within partials, as it will be assumed from the head block.

### Comments
Use comments to explain code as needed: What does it cover, what purpose does it server, why is this solution used.
Mileage of comments for HTML may heavily vary, and most likely not be needed. Any obfuscater, minified, or complier should strip out HTML comments.

### Action Items
Mark todos and action items with TODO. Highlight todos by using the keyword TODO, not other formats like @@.
Append a contact (username or email) in parentheses as the format `TODO(contact)`.
Append action items after a colon as in `TODO: action item`.

	<!-- TODO(jackson.marketon): hookup links -->
	<ul>
	  <li>Home</li>
	</ul>

	<!-- TODO: remove marquee tag -->
	<marquee>This is a marquee, see @JoshBroton about it.</marquee>

---
## HTML Style Rules
### Document Type
Use HTML5 `<!DOCTYPE html>`, this is also the only place you can break the capitalization rule, for the doctype tag.

### HTML Validity
Use valid HTML code. Use tools such as the [W3C HTML validator](http://validator.w3.org/) to test.

### Semantics
Use HTML according to its purpose, use elements ("tags") for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc. 

Using HTML accordion to its purpose is important for accessibility, reuse, and code efficiency reasons.

Use `nav` elements for navigation bars & menus, use `article` elements for articles/text blocks/etc. DO NOT use `aside` for sidebar elements, asides should be used only within `article` or `section` elements to show content that takes away from the main content.

Use `header` and `footer` elements both within `article` and `section` elements if needed, as well as to hold the page headers & footers. Do not but `article` elements inside of `header` or `footer`, you may put `section` elements inside although.

### Multimedia Fallback
For multiple such as images, videos, animated objects via canvas. You **must** offer alliterative access. For images that means use of meaningful alternative text (`alt` property) and for video and audio transcripts and captions, if available.

This is important for accessibility reasons: A blind user has few cues to tell what an image is about without `alt`, and other users may have no way of understanding what video or audio contents are about either.

(For images who alt attribute would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in `alt = ""`.)

Video files **must** have *.mp4* and *.webm* formats, as well as *.ogg* whenever possible as fallbacks.

### Separation of Concerns
Separate structure from presentation from behavior. Strictly keep markup, styling, and scripting apart. No inline scripts, or CSS allowed in HTML.

Also keep the contact area as small as possible by linking as few stylesheets and scripts as possible. You should be compiling both to single files for production.

As for templating, you should use template logic as needed in the html (if, loops, etc).

### Location of Scripts & Stylesheets
Script tags should be immediately before the closing `body` element, with the exception of Modernizr which is allowed in the head. 

Stylesheet tags should be in the header, so they can load before the body, preventing FOUC *(Flash Of Un-styled Content)* from occurring.

### Entity References
Do not use them, with the exception of characters with special meaning in HTML (like <, >, and &) as well as control or "invisible" characters (like no-break spaces).

### Optional Elements (Tags)
Some elements can be omitted via HTML5 spec, but please don't, if only for read-abilities sake. As well as better backward-compatibility.

### Void Elements (Tags)
The following elements should be written `<element>` instead of `<element />` and are considered void tags:

	<br>
	<img>
	<hr>
	<input>
	<link>
	<meta>
	<source>
	<track>
	<wbr>
	<param>
	<keygen>
	<embed>
	<area>

Please do not treat `<script>` tags as self closing, and always have a closing tag.

### Type Attributes
Omit `type` attributes for stylesheets and scripts. Unless you are not using CSS (for stylesheets) or JavaScript (for scripts).
HTML5 implies text/css and text/javascript as defaults, and this is safely backward compatible.

### HTML Formatting Rules
Use a new line for every block, list, or table element, and indent every child element. Also indent children of block, list, or table elements.

You may keep inline-block elements on one line, but you are encouraged to separate them as needed for readability.

	<!-- Bad -->
	<ul><li>Hi</li><li><a href="/"><i class="home"></i>Go Home <span>Now Please</span></a></li></ul>
	
	<!-- Good -->
	<ul>
	  <li>Hi</li>
	  <li><a href="/"><i class="home"></i>Go Home <span>Now Please</span></a></li>
	</ul>
	
	<!-- Best -->
	<ul>
	  <li>Hi</li>
	  <li>
	    <a href="/">
	      <i class="home"></i>Go Home <span>Now Please</span>
	    </a>
	  </li>
	</ul>
	
### HTML Quotation Marks
When quoting attribute values, use double quotation marks. If you need to nest quotation marks for some reason, you can escape them as needed.

	<!-- Bad -->
	<a href='/'>Sign in</a>
	
	<!-- Good -->
	<a href="/">Sign in</a>
	
	<!-- Escaped Quotation Mark -->
	<img src="#" alt="\" No one lies on the internet \" - Ben Franklin">

# Frameworks
-----
You may use the following frameworks for HTML if you wish.

* [Bootstrap](http://getbootstrap.com/) *(Use for admin/app-related pages more than anything else to prevent "bootstrappy look" or having to redo an amazing about of css)*
* [HTML5 Boilerplate](http://html5boilerplate.com/)
* [Foundation](http://foundation.zurb.com/)


# Template Engines
-----

If you are using an HTML template engine for your code (Underscore.js, etc). Use an ERB-style templating language whenever possible, unless there is a specific reason for a different style (massive performance boost, etc), template tags similar to:

	<% Logic %>
	<%= Output %>
	<%- HTML Escaped Output %>
	<%# Comment %>