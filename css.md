# Walker Art Center CSS Code Style Guide
----

## Introduction
*This style guide covers how CSS code should be styled in development, including pre-processors. It aims at improving collaboration, code quality, and enabling supporting infrastructure. It applies to raw, working files that use CSS and pre-processors (SASS/SCSS/LESS). Tools are free to obfuscate, minify, and compiles as long as the general code quality is maintained.*

### Preprocessors
**Do not use LESS.** We are entirely a SCSS shop (SCSS, is a type of SASS, that is written like CSS). If a plugin/framework uses less, please either compile it, and import the CSS, or find a SASS port of the project.

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

	/* No */
	.example {
  		background: url(http://www.google.com/images/example);
  	}
	
	/* Yes */
	.example {
  		background: url(//www.google.com/images/example);
  	}

### Images vs. CSS
For styles you can replicate via CSS: arrows, drop shadows, rounded corners. Please use CSS unless you cannot replicate the style at any close approximation.

---
## General Formatting
### Indentation
Indent by 4 spaces at a time, do not use tabs or mix tabs and spaces for indentation

	.example {
	    color: blue;
	}

### Capitalization
##### CSS
Use lowercase on the following: HTML element names, attributes, attribute values (unless text/CDATA), property values (unless strings), properties, CSS selectors.

	/* No */
	color: #E5E5E5;
	
	/* Yes */
	color: #e5e5e5;
	
##### Preprocessor
Global variables should be `spinal-case` (unless a frameworks requires a different case, then comment what framework is using it), Local variables should be `lower_snake_case`, and mixins should be `camelBackCase`

	$base-font: 16px; // Susy Framework Default Var
	
	@function pxToEm($pixel, $context: $base-font) {
		$converted_pixel = $pixel/$context;
		@return #{$converted_pixel}em
	}

### Trailing Whitespace
Remove it, as it complicates diffs and is unnecessary.

---
## General Meta Rules
### Encoding
UTF-8, without a byte order mark, is required. Nothing else allowed. UTF-8 is assumed in CSS.

### Comments
Use comments to explain code as needed: What does it cover, what purpose does it server, why is this solution used.
For pre-processors, please comment on the function of mixins, as well as what variables should do, using [DocBlockr](https://github.com/Warin/Sublime/tree/master/DocBlockr) format. Ex:

	$base-font: 16px; // Default
	
	/**
	 * [em Convert pixel to EM]
	 * @param {[px value]} $pixel [convert pixels to ems]
	 * @param {[px value]} $context [pixel value of font, defaults to global $base-font]
	 * @return [em value]
	 */
	@function em($pixel, $context: $base-font) {
		@return ($pixel / $context) * 1em;
	}

### Action Items
Mark todos and action items with TODO. Highlight todos by using the keyword TODO, not other formats like @@.
Append a contact (username or email) in parentheses as the format `TODO(contact)`.
Append action items after a colon as in `TODO: action item`.

	// TODO(jackson.marketon): change color
	color: red;

	// TODO: fix height bug
	height: 100%;

---
## CSS Style Rules
### CSS Validity
Use valid CSS/SCSS where possible, unless dealing with validator bugs or requiring proprietary syntax, use valid CSS code.
Use tools such as [W3C CSS Validator](http://jigsaw.w3.org/css-validator/) to test.
This gives us a baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

### ID and Class Naming
Use meaningful or generic ID and class names. Do not use presentational or cryptic names. IDs should only occur once on a page, as per valid CSS. Classes should be preferred over IDs, using a preprocessor and OOCSS (Objective Oriented CSS), should allow you to reduce the number of both IDs and classes required. 

	/* Bad: meaningless */
	#de-200 {}
	
	/* Bad: presentational */
	.button-green {}
	.clear {}
	
	/* Good: Specific */
	#gallery {}
	.video {}
	
	/* Good: generic */
	.theme-primary-color {}
	.aux {}
	.alt {}
	
	/* Good: functional */
	.clear-float {}
	
### ID and Class Name Styles
Use ID and class names that are as short as possible but as long as necessary. Contribute to acceptable levels of understandability and code efficiency.

	/* Bad */
	#navigation {}
	.atr {}
	
	/* Good */
	#nav {}
	.author {}
	
### Type Selectors
Avoid qualifying ID and class names with type selectors, unless necessary (for example helper/puesdo classes), do not use element names in conjunction with IDs or classes. This also helps produce more OOCSS as well as for [performance reasons](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/).

	/* Bad */
	ul#example {}
	div.error {}
	
	/* Good */
	#example {}
	.error {}
	
### Shorthand Properties
Use shorthand properties where possible (font, margin, etc).

	/* Bad */
	border-top-style: none;
	font-family: Ariel;
	font-size: 100%;
	line-height: 1.6;
	padding-bottom: 2em;
	padding-top: 0;
	padding-right: 1em;
	padding-left: 1em;
	
	/* Good */
	border-top: 0;
	font: 100%/1.6 Ariel;
	padding: 0 1em 2em;
	
### 0s and units
Do not use units after 0 unless they are required.

### Leading 0s
Omit leading "0"s in values or lengths between -1 and 1.

### Hexadecimal Notation
Use Hexadecimal notation where possible, switch to RGB if needed for transparency. Use 3 character hexadecimal notation when permitted.

	/* Bad */
	color: #eebbcc;
	
	/* Good */
	color: #ebc;

### Prefixes
Use namespaces for prefixing for large projects or code for embedding, use the same unique prefix on all code related to that project followed by a dash.

	.adw-help {} // Adwords
	#wacmc-slider {} // Walker Art Center Media Collection

### ID and Class Name Delimiters
Separate words in ID via lowerCamelCase, separate words in classes via a hyphen as in spinal-case. Do not use any other style of delimiter.

	#videoSlider {}
	.slide-item {}	

### Hacks
Avoid user agent detection as well as CSS "hacks" -- try a different approach first. It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

## CSS Formatting Rules

### Declaration Order
Alphabetize declarations, ignore vendor-specific prefixes for sporting purposes. However sort multiple vender-specific prefixes for a property.
	
	background: grey;
	border: 0;
	-moz-border-radius: 4px;
	-webkit-border-radius: 4px;
	text-align: center;
	text-indent: 4em;
	z-index: 200;

### Block content Indentation
Indent all block content, to reflect hierarchy and improve understanding.

### Declaration Stops
End every declaration with a semicolon for consistency and extensibility reasons.

	/* Bad */
	.test {
	    display: block;
	    height: 100px
	}
	
	/* Good */
	.test {
	    display: block;
	    height: 1px;
	}

### Property Name Stops
Use a space after a property name's colon, but not before for consistency reasons.

	/* Bad */
	font-weight:bold;
	font-color :red;
	
	/* Good */
	font-weight: bold;
	font-color: red;
	
### Declaration Block Separation
Use a space between the last selector and declaration block. The opening brace should be on the same line as the last selector in a given rule.

	/* Bad: missing space */
	video{
	    margin: 1px;
	}
	
	/* Bad: unneeded line break */
	video
	{
	    margin: 1px;
	}
	
	/* Good */
	video {
	    margin: 1px;
	}

### Selector and Declaration Separation
Always start a new line for each selector and declaration.

	h1,
	h2,
	h3 {
	    font-weight: normal;
	}

### Rule Separation
Always but a blank line between rules. For preprocessors, always but a blank link between rules and mixing, variables should be separated into related groups.

	video {}
	
	audio {}
	
	@mixin randomize() {}
	
	$variable-1: ;
	$variable-2: ;
	
	$unrelated-variable: ;

### CSS Quotation Marks
Use single (' ') instead of double (" ") quotation marks for attribute selectors or property values. Do not use quotation marks in URI values (`url()`).

`Exception: the **@charset** rule does not permit single quotation marks`

## CSS Meta Rules
### Section Comments
Group sections by a start and end section comments. Separate sections with new lines.
	
	/* Header */
	header {}
	/* End Header */
	
## SCSS Meta Rules
### Multiple Document Tree
You should have a `main.scss` file, that imports everything else. All your imported documents should have filenames starting with underscores (_), you should separate these files by function and content. The last file imported **MUST** be a `_hacks.scss` file, see more about this below. For example:

	main.scss
	_config.scss (holds global config variables and imports for compass/susy)
	_typography.scss
	_layout.scss (imports _header, _body, _footer)
	_header.scss
	_body.scss (imports _slideshow)
	_slideshow.scss
	_footer.scss
	_hacks.scss

### _hacks.scss file
This file is for quick bug fixes to SCSS code. It should be empty upon major version releases and should only be used if someone is unable to find where to fix the bug they are encountering elsewhere, also, put all browser hacks here.

---
## Frameworks
You are free to use the following frameworks:

* [Inuit.css](https://github.com/csswizardry/inuit.css/)
* [Compass](http://compass-style.org/) (Preferred)
* [Susy](http://susy.oddbird.net/) (Preferred)
* [Bootstrap](http://getbootstrap.com/css/)
* [Foundation](http://foundation.zurb.com/) 