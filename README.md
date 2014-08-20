ti-xregexp
=============

[XRegExp](http://xregexp.com/) 2.0.0 for Appcelerator Titanium

This is a [titaniumified][ti] version of [XRegExp][xre]. This is built using [`grunt-titaniumifier`][gti].

[xre]: http://xregexp.com/
[gti]: https://github.com/smclab/grunt-titaniumifier


### Installation

If you are developing a Titanium SDK application, a packaged *CommonJS* module can be found in the [Releases page][rls].

If you are instead
- porting with *titaniumifier* a Node.js module to Titanium, and it uses *superagent*;
- or building CommonJS module using *titaniumifier* and you want to have a reliable, stable, tested HTTPClient;

then you can install this module with

    npm install --save xregexp ti-xregexp

In your `package.json` add

```js
{
  "name": "...",
  "version": "...",
  // ...
  "titanium": {
    "xregexp": "ti-xregexp"
  }
}
```

This will tell *titaniumifier* that when your code requires `xregexp`, `ti-xregexp` is served instead.

You can use [this *package.json* from one of our modules][lrc-pkg] as a reference.

[rls]: https://github.com/mdpauley/ti-xregexp/releases
[lrc-pkg]: https://github.com/smclab/liferay-connector/tree/master/package.json


Usage overview
--------------

For the full documentation head over the [original repository][xre].

```js
var xregexp = require('xregexp').XRegExp;

// Using named capture and flag x (free-spacing and line comments)
date = XRegExp('(?<year>  [0-9]{4} ) -?  # year  \n' +
               '(?<month> [0-9]{2} ) -?  # month \n' +
               '(?<day>   [0-9]{2} )     # day     ', 'x');

XRegExp.exec('2012-06-10', date).year;
// -> '2012'

// Matchception: Finding matches within matches, while passing forward and
// returning specific backreferences
html = '<a href="http://xregexp.com/api/">XRegExp</a>' +
       '<a href="http://www.google.com/">Google</a>';
XRegExp.matchChain(html, [
  {regex: /<a href="([^"]+)">/i, backref: 1},
  {regex: XRegExp('(?i)^https?://(?<domain>[^/?#]+)'), backref: 'domain'}
]);
// -> ['xregexp.com', 'www.google.com']
```
