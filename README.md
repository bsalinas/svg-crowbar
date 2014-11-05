#SVG Crowbar

This is a fork of the SVG Crowbar bookmarklet developed by the New York Times. See [that project page](http://nytimes.github.com/svg-crowbar/)

# Programmatic Usage of SVG Crowbar
One of the things that SVG Crowbar does very nicely is automatically embed styles applied to SVGs via CSS in that CSS. This library takes that functionality and lets you use it programmatically via javascript. In particular, this library:
* Removes the interactive functionality in the bookmarklet ("Select Which SVG to Download")
* Provides access to the array of SVGs found on the DOM
* Allows you to get the raw SVG (with embedded styles)
* Allows you to download any individual SVG (with embedded styles)
* Allows you to get the Blob of any individual SVG (for saving files programmatically)

# Usage
Include `svg-crowbar.js` in your website. This will expose the `crowbar` object which has the following methods
## findAndParseSVGs
This method should be called first. It returns an array of SVGs which the library finds on your DOM.
```
var sources = crowbar.findAndParseSVGs()
```
Here is an example element of the sources array
```javascript
{
	childElementCount: 624,
	class: "first",
	height: 302,
	id: null,
	left: 8,
	source:["...actual SVG code with embedded styles"],
	top:86.7187,
	width:602
}
```
The `id` and `class` attributes can be used to help identify which SVG to download. The `source` array contains the actual `svg` markup.

## prepareBlob
The prepareBlob method requires a source (from the response of `findAndParseSVGs` method) to be specified as an argument. It will return a `Blob` that represents that svg.
```javascript
var sources = crowbar.findAndParseSVGs()
if(sources.length > 0){
	//Just get the Blob for the first
	var blob = crowbar.prepareBlob(sources[0])
}
```

## download
The download method requires a source (from the response of `findAndParseSVGs` method) to be specified as an argument. It will trigger a download of that svg file in the browser.
```javascript
var sources = crowbar.findAndParseSVGs()
if(sources.length > 0){
	//Just download the first
	crowbar.download(sources[0])
}
```

# Example
See the example directory for examples.


