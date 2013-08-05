#html-table-of-contents

Generates a table of contents for your HTML document based on the headings 
present.

## Where do I get it?

You can download it from github at 
[https://github.com/matthewkastor/html-table-of-contents](https://github.com/matthewkastor/html-table-of-contents) 
or, if you have node installed you can get it from npm

`npm install html-table-of-contents`

## Usage

Using this module in your browser is as simple as including it in your page 
and calling `htmlTableOfContents()` after the page has loaded.

The table of contents will be generated in the first element with the id of 
`toc`. It will consist of a series of sibling `div`'s whose class directly maps 
to the heading level of the heading it describes. By default there is no 
styling done to the table of contents, to allow you to style it however you 
wish. This module comes with a css stylesheet which you can include in your 
page if you would like to. The provided stylesheet simply indents entries in 
the table of contents based on the heading level in the document. Take a look 
at the stylesheet `html-table-of-contents.css`, in this module's root folder, 
to get an idea of how to access the table of contents entries if you wish to 
create your own stylesheet.

If you're using this module outside of a browser you will have to supply a 
reference to a dom document object, unless you've called it `document` and 
have declared your document object globally. I did 
not require any specific module for parsing the DOM, because there are a few 
out there and it would be rude of me to force you to use a specific one for 
such a simple function.

### Generating a table of contents in Browser

```
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
    <head>
        <title>
            html-table-of-contents Example
        </title>
        <script src="./node_modules/html-table-of-contents/src/html-table-of-contents.js"
              type="text/javascript">
</script>
        <link rel="stylesheet"
            type="text/css"
            href="./node_modules/html-table-of-contents/html-table-of-contents.css" />
    </head>
    <body onload="htmlTableOfContents();">
        <p>
            <b>Contents</b>
        </p>

        <div id="toc">
        </div>

        <h1>
            top heading 1
        </h1>

        <h2>
            second heading
        </h2>

        <h1>
            top heading 2
        </h1>
    </body>
</html>
```

### Generating a table of contents in Node

```
// parse your html into a DOM Document using jsdom
// or something https://npmjs.org/package/jsdom

var fs = require('fs'); 
var jsdom = require("jsdom").jsdom;
var htmlTableOfContents = require('html-table-of-contents');

var html = fs.readFileSync('example.html', 'utf8');
// javascript written for the browser expects global
// window and document objects
var document = global.document = jsdom(html, null, {
    features: {
        FetchExternalResources : false,
        ProcessExternalResources : false
    }
});
var window = global.window = global.document.parentWindow;

htmlTableOfContents();
// alternatively, if you've called the 
// document object something other than 
// document, you may supply it as the 
// first argument and everything will 
// work out fine.
// htmlTableOfContents(nonstandardDocumentReference);

console.log(document.documentElement.innerHTML);

// Shazam. The document now contains a table of 
// contents you didn't have to write.
```
