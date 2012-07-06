## lazy-retina

Lazy-retina is based on fasterize lazyload, it's the same code with retina support and external options.

It's a standalone script that weights ~1KB minified gzipped.

## How to use ?

1. Add lazy-retina.min.js to your page before any `<script>` tag, either src or inline if
you do not have any other scripts in the `<head>`.
2. Change all `<img>` tags to lazyload :

```html
  <img
    data-src="real/image/src.jpg"
    src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw=="
    onload="lzld(this)" onerror="lzld(this)"
    width="200" height="400" >
```

## And for non-lazyloaded images ?

It's possible to use lazy-retina for non-lazyloaded images, it's the same syntax and the same process :

1. Add lazy-retina.min.js to your page before any `<script>` tag, either src or inline if
you do not have any other scripts in the `<head>`.
2. Change all `<img>` tags to add support :

```html
  <img
    src="real/image/src.jpg"
    onload="lzld(this)" onerror="lzld(this)"
    width="200" height="400" >
```

## Who use it ?

lazy-retina is used on :

* [mobile.lemonde.fr](http://mobile.lemonde.fr/), news, 1st mobile website in France. [source](http://www.mediametrie.fr/internet/communiques/telecharger.php?f=26408ffa703a72e8ac0117e74ad46f33) (pdf)

## Configuration

We can configure lazy-retina for custom use :

```html
  <script src="lazy-retina.js"></script>
  <script>
    lzld.config.retina = true; // force retina
    lzld.config.lazy-attr = "data-mysrc-attr"; // change attribute
  </script>
```

* `retina` : Set the retina support, default `auto` (the retina is determined by `window.devicePixelRatio`), it accepts a boolean to force support.
* `hdCallback` : The callback to transform the `src` in a retina `src`, `var hdSrc = hdCallback(src)`;
* `lazyAttr` : The lazy attribute, default `data-src`.
* `minDevicePixelRatio` : The min device pixel ratio to enable retina in "auto" mode.
* `offset` : Vertical offset in px. Used for preloading images while scrolling

### The default hdCallback

The default hd callback simply add `@2x` to the img like on iOS platforms :

````javascript
function defaultHdCallback(src)
{
	var srcSegments = src.split("."),
	    srcWithoutExtension = srcSegments.slice(0, (srcSegments.length - 1)).join("."),
	    extension = srcSegments[srcSegments.length - 1];
	
	return srcWithoutExtension + "@2x." + extension;
}
````

## Methods

### lzld.update()

Force an update of all loaded images :

````javascript
// We force retina and we update all loaded images
lzld.config.retina = true;
lzld.update();
````

### lzld.isRetinaDevice()

Check if the device is retina according to `lzld.config.minDevicePixelRatio`.

## Browser support

*IE6+ or modern browser.*

IE6/7 originally does not support data uri:s images but using the onerror event on to-be-lazyloaded images, we're able to register the current image in the lazyloader.
The only drawback is that you can have red crosses showing that original data uri:s image cannot be loaded. But well, it's old IE so no big deal.

You can have IE6/7 support without the hack, use the `b.gif` image instead of the data uri:s and remove `onerror`.

## How does it works

Lazy-retina is based on fasterize lazyload, so it's efficient and speedy. You can see how the lazyload part works on https://github.com/fasterize/lazyload/.

The retina part is no more complicated, it test if retina is active and supported and execute a callback to modify the source in order to load the retina image file.

## Credits

Fully based on very powerful https://github.com/fasterize/lazyload/

## Licence

(The MIT Licence)

Copyright (c) 2012 Greg Bergé, http://neoziro.com

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.