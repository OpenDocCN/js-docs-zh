# Change Log

# Change Log

## v1.1.0 — *05 Dec 2013* — [diff](https://github.com/madrobby/zepto/compare/v1.0...v1.1.0)

### Notable changes

*   IE10+ support
*   [Huge speed optimizations](http://jsperf.com/zepto-1-0-vs-1-1-performance/2) for simple CSS selectors (classname, ID) and DOM element creation
*   Provide `$.Callbacks` and `$.Deferred` in optional modules
*   Removed `fx` and `detect` modules from default build

### Ajax

*   New supported `$.ajax()` options:
    *   `xhrFields`
    *   `mimeType`
    *   `jsonpCallback`
    *   `username` & `password`
*   Promise interface supported when loading the optional “callbacks” and “deferred” modules:
    *   `xhr.done(function(data, status, xhr){ ... })`
    *   `xhr.fail(function(xhr, errorType, error){ ... })`
    *   `xhr.always(function(){ ... })`
*   Enable mutating Ajax settings in the `beforeSend` callback
*   Fix JSONP callbacks for errored responses on Android
*   Ensure consistent `Accept` request HTTP header across browsers
*   Fix `$.param()` for jQuery compatibility when handling complex nested objects
*   Support IIS JavaScript MIME type
*   Pass “abort” and “timeout” status to global `ajaxError` event handlers

### Event

*   Provide `isDefaultPrevented()`, `stopImmediatePropagation()`, and related methods for all events
*   Support the `data` argument in `.bind()`, `.on()`, and `.one()`
*   Support CSS selector argument in `.one()` for event delegation
*   Support `.on('ready')` as an alias for `.ready()`
*   Enable event handlers on plain old JS objects
*   Many fixes related to event delegation

### Data

*   Cleanup `.data()` values on DOM element removal with `.remove/empty()`
*   `.data()` now assumes that numbers that begin with zeroes are strings
*   `.removeData()` (no argument) now removes all data on the element
*   Enable reading `data-*` attributes that have underscores in the name

### Misc.

*   Support simple DOM property names in `.prop(name)` such as `for`, `class`, `readonly`…
*   Implement the `.scrollLeft([value])` method
*   Support setting `.scrollTop(value)`
*   Fix `$(document).width/height()`
*   Support fetching multiple CSS values via array in `.css(['prop1', 'prop2', ...])`
*   Support setting CSS transition delay via `delay` option for `.animate()`
*   Ensure that `.animate()` callback always firesParty like it’s one-oh!_

## v1.0 — *02 Mar 2013* — [diff](https://github.com/madrobby/zepto/compare/v1.0rc1...v1.0)

*Party like it’s one-oh!*

### Notable changes

*   Zepto is now compatible with Twitter Bootstrap
*   Portable, completely new node.js-based build system
*   Fully automated tests with PhantomJS and Travis CI
*   Removed `touch` module from default distribution

### New features

*   `$.fn.filter(function(index){ ... })`
*   `$.fn.contents()`
*   `$.fn.wrapInner()`
*   `$.fn.scrollTop()`
*   `$.contains()`
*   `$.fn.has()`
*   `$.fn.position()`
*   `$.fn.offsetParent()`
*   `$.parseJSON()`
*   `$.camelCase()`
*   `$.isWindow()`
*   `$.grep()` (interface to `Array.filter`)
*   Support `$(html, attributes)` syntax for element creation
*   Emulate `mouseenter` and `mouseleave` events
*   Bootstrap compat: support `$.fn.offset(coordinates)`
*   Bootstrap compat: implement `$.fn.detach()`
*   Add support for Ajax `cache: false` option
*   Prevent scrolling when horizontal swipe events are detected
*   `cancelTouch` for tap events
*   `prev` and `next` now support an optional selector argument
*   `$.fn.find` and `$.fn.closest` now support Zepto objects as arguments
*   Enable deep copy via `$.extend(true, target, source)`
*   Enable nested structures for `$.fn.wrap()` and `$.fn.wrapAll()`
*   Enable function arguments for `$.fn.wrap()` and `$.fn.wrapInner()`
*   Support number, boolean, JSON types in data attributes
*   Support manipulating classnames on SVG elements
*   Enable named durations for `animate`, e.g. `slow`.
*   Support `timing-function` for `animate`
*   Support event properties passed to `$.fn.trigger()` or `$.Event()`
*   Selector module: support child `&gt; *` queries
*   Add detect support for mobile Chrome browser
*   Add `$.os.phone` and `$.os.tablet` (booleans)
*   Detect Firefox mobile, Playbooks and BB10

### Fixes

*   Fix passing null selector to `on` or `off`
*   Fixed bug where self-closing html tags would act as open tags
*   Fix `val` for multiple select
*   Fix various touch and gesture bugs.
*   Corrected parameters of `load` success callback to match jQuery.
*   Fix `css` with 0 values and falsy values
*   Fix a `css` performance issues with string values
*   Fix `$.ajaxJSONP` when invoked directly
*   Fix `animate` with 0 durations.
*   Fix `toggle` and `fadeToggle` for multiple elements.
*   Fix ajax `$.fn.load` behavior with selector
*   Make `attr(name, null)` unset attribute
*   Fix `animate` in Firefox
*   Fix `animate` for elements just added to DOM
*   Fix an escaping issue with `$.param`
*   Respect `traditional: true` option in `$.ajax`
*   Fix `focus` & `blur` event delegation and enable unbind
*   Simple wrapping for any object passed to `$()`
*   Enable `children` method for XML documents
*   Don’t eval `&lt;script&gt;` content when `src` is present
*   Support `processData` option for `$.ajax()`
*   Enable passing `contentType: false` to `$.ajax()`
*   Apply `focus()` and `blur()` to all elements in collection
*   Change `$.fn.map()` to return a Zepto collection
*   Selector argument for `on(evt, selector, fn)` can be false
*   Don’t raise error on `$('#')`
*   Provide empty object in `$.support`
*   `return false` in event handler calls stopPropagation()
*   Fix `$.isPlainObject()` for `window` in Opera
*   `$.ajax` error callback correctly reports `abort` status
*   Fix `hasClass` in collections of multiple elements
*   Stop iteration in `each()` when the callback returns false
*   Add ability to set `xhr` factory per-request
*   Have `get()` method accept negative index
*   Support for multiple class names in `toggleClass()`
*   Fix error callbacks for `ajaxJSONP`
*   Support optional `data` argument for various Ajax methods
*   Fix DOM insertion operators for null values
*   Fix dataType being set for `$.getJSON`

## v1.0rc1 — *09 Apr 2012* — [diff](https://github.com/madrobby/zepto/compare/v0.8...v1.0rc1)

The *semicolon-free* edition! That’s right, we removed all trailing semicolons from the source and tests. [They were never needed anyway](http://mislav.uniqpath.com/2010/05/semicolons/ "Semicolons in JavaScript are optional").

New methods:

*   clone
*   prop
*   $.isPlainObject
*   $.inArray
*   $.trim
*   $.proxy

New module:

*   “selector.js” with experimental support for jQuery CSS pseudo-selectors such as `:visible` and `:first`

### Improvements in core:

*   added missing methods for Ember.js compatibility
*   improved creating DOM fragments from HTML with $())
*   enable append & family to accept multiple arguments
*   fix $.each context
*   fix calling get without index
*   fix calling val on empty collection
*   using `css(property, '')` removes the property
*   fix filter, is, and closest when operating on nodes that are detached from the document
*   remove `end` & `andSelf` from core to the new “stack.js” plugin
*   exposed important internal Zepto functions through the `$.zepto` object for extending or overriding Zepto functionality.
*   data method returns undefined when there is no data
*   support camelized names in data method

Apart from improving the basic `data` method in core, the “data.js” module got improvements as well:

*   better jQuery compatibility
*   ability to store functions
*   new `removeData` method

### Ajax:

*   have correct ajaxComplete argument order for JSONP abort and timeout
*   JSONP requests that hit a 404 will now correctly invoke the error callback
*   add support for `dataType: 'jsonp'` in $.ajax
*   add support for `data` in $.ajaxJSONP
*   HTTP 304 status is treated as success instead of an error
*   made load more compatible with jQuery
*   allow Content-Type to be set via request headers
*   respect Content-Type of the response if `dataType` isn’t set
*   work around Chrome CORS bug when data is empty

### Changes in other modules:

*   fix animate for edge cases such as when there is an animation within an animated element, and improve handling of transition CSS properties
*   new “singleTap” event
*   improved “longTap” detection

## 0.8 — *03 Nov 2011* — [diff](https://github.com/madrobby/zepto/compare/v0.7...v0.8)

*   CSS transitions for every browser with `animate()` method;
*   unified event handling with `fn.on()` & `off()`;
*   Ajax global events & timeout support;
*   performance boost for selectors.

See [full release notes](https://gist.github.com/1337487 "Zepto 0.8 release notes").

## 0.7 — *01 Aug 2011* — [diff](https://github.com/madrobby/zepto/compare/v0.6...v0.7)

*   add `$.each`, `$.map`, `$.slice`;
*   add `.serializeArray()`, `.serialize()`;
*   add `.triggerHandler()`;
*   add `.wrap`, `.wrapAll`, `.unwrap`, `.width/height` setters, `.append` (and friends) improvements;
*   add “longTap” event;
*   `.anim()` accepts CSS transform properties;
*   `return false` in event handlers cancels browser event behavior.

## 0.6 — *14 May 2011* — [diff](https://github.com/madrobby/zepto/compare/v0.5...v0.6)

*   add `.add`, `.appendTo`, `.prependTo`, `.replaceWith`, `.empty`, `.submit`;
*   allow function args for `.add/.remove/.toggleClass`;
*   improvements to events and xhr.

## 0.5 — *01 Mar 2011* — [diff](https://github.com/madrobby/zepto/compare/v0.4...v0.5)

*   add `.not`, `.children`, `.siblings`, `$.param`;
*   improve `.attr` & `.html`;
*   support callback for `.anim`.

## 0.4 — *21 Jan 2011* — [diff](https://github.com/madrobby/zepto/compare/v0.3...v0.4)

*   JSONP;
*   better `.find`, `.each`, `.closest`;
*   add `.eq`, `.size`, `.parent`, `.parents`, `.removeAttr`, `.val`;
*   support function args in `.html`, `.attr`;
*   adjacency methods now take Zepto objects.

## 0.3 — *17 Dec 2010* — [diff](https://github.com/madrobby/zepto/compare/v0.2...v0.3)

*   add `.toggleClass`, `.attr` setter, `.last`, `.undelegate`, `.die`;
*   proxied event objects for event delegation;
*   support `$` fragments.

## 0.2 — *01 Dec 2010* — [diff](https://github.com/madrobby/zepto/compare/v0.1...v0.2)

*   now compatible with [backbone.js](http://documentcloud.github.com/backbone/);
*   support event unbind;
*   ajax posts with data.

## 0.1 — *26 Oct 2010*

[First. Release.](https://github.com/madrobby/zepto/blob/v0.1/src/zepto.js) Ever.