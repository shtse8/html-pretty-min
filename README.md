HTML Pretty-Min
===============

HTML Pretty-Min is a PHP library for minifying and prettyprinting (indenting) HTML documents
that works directly on the DOM tree of an HTML document.

Currently it has the following features:

- **Prettyprint**:
  - Indent Block-level elements, do not indent inline elements

- **Minify**: 
  - Remove whitespace and newlines
  - Compress embedded Javascript using [mrclay/jsmin-php](https://packagist.org/packages/mrclay/jsmin-php)
  - Compress embedded CSS using [tubalmartin/cssmin](https://packagist.org/packages/tubalmartin/cssmin)
  - Remove some attributes when their value is empty (by default "style" and "class" attributes)
  - Remove comments, except those matching some given regular expressions (by default, IE conditional comments are kept)

Installation
------------

`composer require wasinger/html-pretty-min`

Usage
-----

```php
<?php
use Wa72\HtmlPrettymin\PrettyMin;

$pm = new PrettyMin();

$output = $pm
    ->load($html)   // $html may be a \DOMDocument, a string containing an HTML code, 
                    // or an \SplFileInfo pointing to an HTML document
    ->minify()
    ->saveHtml();
```

Attention: Because the formatting is done directly on the DOM tree, a DOMDocument given to the `load()` method
will be modified:

```php
$dom_document = new \DOMDocument('1.0', 'UTF-8');
$dom_document->loadHTML('<html>...some html code...</html>');

$pm->load($dom_document)->minify();

echo $dom_document->saveHTML(); // Will output the minified, not the original, document
```