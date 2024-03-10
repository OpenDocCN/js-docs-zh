# Change Log

## Change Log

**1.1.2** — *Feb. 20, 2014* — [Diff](https://github.com/jashkenas/backbone/compare/1.1.1...1.1.2) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/1.1.2/index.html)

*   Backbone no longer tries to require jQuery in Node/CommonJS environments, for better compatibility with folks using Browserify. If you'd like to have Backbone use jQuery from Node, assign it like so: `Backbone.$ = require('jquery');`
*   Bugfix for route parameters with newlines in them.

**1.1.1** — *Feb. 13, 2014* — [Diff](https://github.com/jashkenas/backbone/compare/1.1.0...1.1.1) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/1.1.1/index.html)

*   Backbone now registers itself for AMD (Require.js), Bower and Component, as well as being a CommonJS module and a regular (Java)Script. Whew.
*   Added an `execute` hook to the Router, which allows you to hook in and custom-parse route arguments, like query strings, for example.
*   Performance fine-tuning for Backbone Events.
*   Better matching for Unicode in routes, in old browsers.
*   Backbone Routers now handle query params in route fragments, passing them into the handler as the last argument. Routes specified as strings should no longer include the query string (`'foo?:query'` should be `'foo'`).

**1.1.0** — *Oct. 10, 2013* — [Diff](https://github.com/jashkenas/backbone/compare/1.0.0...1.1.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/1.1.0/index.html)

*   Made the return values of Collection's `set`, `add`, `remove`, and `reset` more useful. Instead of returning `this`, they now return the changed (added, removed or updated) model or list of models.
*   Backbone Views no longer automatically attach options passed to the constructor as `this.options` and Backbone Models no longer attach `url` and `urlRoot` options, but you can do it yourself if you prefer.
*   All `"invalid"` events now pass consistent arguments. First the model in question, then the error object, then options.
*   You are no longer permitted to change the **id** of your model during `parse`. Use `idAttribute` instead.
*   On the other hand, `parse` is now an excellent place to extract and vivify incoming nested JSON into associated submodels.
*   Many tweaks, optimizations and bugfixes relating to Backbone 1.0, including URL overrides, mutation of options, bulk ordering, trailing slashes, edge-case listener leaks, nested model parsing...

**1.0.0** — *March 20, 2013* — [Diff](https://github.com/jashkenas/backbone/compare/0.9.10...1.0.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/1.0.0/index.html)

*   Renamed Collection's "update" to set, for parallelism with the similar `model.set()`, and contrast with reset. It's now the default updating mechanism after a fetch. If you'd like to continue using "reset", pass `{reset: true}`.
*   Your route handlers will now receive their URL parameters pre-decoded.
*   Added listenToOnce as the analogue of once.
*   Added the findWhere method to Collections, similar to where.
*   Added the `keys`, `values`, `pairs`, `invert`, `pick`, and `omit` Underscore.js methods to Backbone Models.
*   The routes in a Router's route map may now be function literals, instead of references to methods, if you like.
*   `url` and `urlRoot` properties may now be passed as options when instantiating a new Model.

**0.9.10** — *Jan. 15, 2013* — [Diff](https://github.com/jashkenas/backbone/compare/0.9.9...0.9.10) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.9.10/index.html)

*   A `"route"` event is triggered on the router in addition to being fired on `Backbone.history`.
*   Model validation is now only enforced by default in `Model#save` and no longer enforced by default upon construction or in `Model#set`, unless the `{validate:true}` option is passed.
*   `View#make` has been removed. You'll need to use `$` directly to construct DOM elements now.
*   Passing `{silent:true}` on change will no longer delay individual `"change:attr"` events, instead they are silenced entirely.
*   The `Model#change` method has been removed, as delayed attribute changes are no longer available.
*   Bug fix on `change` where attribute comparison uses `!==` instead of `_.isEqual`.
*   Bug fix where an empty response from the server on save would not call the success function.
*   `parse` now receives `options` as its second argument.
*   Model validation now fires `invalid` event instead of `error`.

**0.9.9** — *Dec. 13, 2012* — [Diff](https://github.com/jashkenas/backbone/compare/0.9.2...0.9.9) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.9.9/index.html)

*   Added listenTo and stopListening to Events. They can be used as inversion-of-control flavors of `on` and `off`, for convenient unbinding of all events an object is currently listening to. `view.remove()` automatically calls `view.stopListening()`.
*   When using `add` on a collection, passing `{merge: true}` will now cause duplicate models to have their attributes merged in to the existing models, instead of being ignored.
*   Added update (which is also available as an option to `fetch`) for "smart" updating of sets of models.
*   HTTP `PATCH` support in save by passing `{patch: true}`.
*   The `Backbone` object now extends `Events` so that you can use it as a global event bus, if you like.
*   Added a `"request"` event to Backbone.sync, which triggers whenever a request begins to be made to the server. The natural complement to the `"sync"` event.
*   Router URLs now support optional parts via parentheses, without having to use a regex.
*   Backbone events now supports `once`, similar to Node's `once`, or jQuery's `one`.
*   Backbone events now support jQuery-style event maps `obj.on({click: action})`.
*   While listening to a `reset` event, the list of previous models is now available in `options.previousModels`, for convenience.
*   Validation now occurs even during "silent" changes. This change means that the `isValid` method has been removed. Failed validations also trigger an error, even if an error callback is specified in the options.
*   Consolidated `"sync"` and `"error"` events within Backbone.sync. They are now triggered regardless of the existence of `success` or `error` callbacks.
*   For mixed-mode APIs, `Backbone.sync` now accepts `emulateHTTP` and `emulateJSON` as inline options.
*   Collections now also proxy Underscore method name aliases (collect, inject, foldl, foldr, head, tail, take, and so on...)
*   Removed `getByCid` from Collections. `collection.get` now supports lookup by both `id` and `cid`.
*   After fetching a model or a collection, *all* defined `parse` functions will now be run. So fetching a collection and getting back new models could cause both the collection to parse the list, and then each model to be parsed in turn, if you have both functions defined.
*   Bugfix for normalizing leading and trailing slashes in the Router definitions. Their presence (or absence) should not affect behavior.
*   When declaring a View, `options`, `el`, `tagName`, `id` and `className` may now be defined as functions, if you want their values to be determined at runtime.
*   Added a `Backbone.ajax` hook for more convenient overriding of the default use of `$.ajax`. If AJAX is too passé, set it to your preferred method for server communication.
*   `Collection#sort` now triggers a `sort` event, instead of a `reset` event.
*   Calling `destroy` on a Model will now return `false` if the model `isNew`.
*   To set what library Backbone uses for DOM manipulation and Ajax calls, use `Backbone.$ = ...` instead of `setDomLibrary`.
*   Removed the `Backbone.wrapError` helper method. Overriding `sync` should work better for those particular use cases.
*   To improve the performance of `add`, `options.index` will no longer be set in the `add` event callback. `collection.indexOf(model)` can be used to retrieve the index of a model as necessary.
*   For semantic and cross browser reasons, routes will now ignore search parameters. Routes like `search?query=…&page=3` should become `search/…/3`.
*   `Model#set` no longer accepts another model as an argument. This leads to subtle problems and is easily replaced with `model.set(other.attributes)`.

**0.9.2** — *March 21, 2012* — [Diff](https://github.com/jashkenas/backbone/compare/0.9.1...0.9.2) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.9.2/index.html)

*   Instead of throwing an error when adding duplicate models to a collection, Backbone will now silently skip them instead.
*   Added push, pop, unshift, and shift to collections.
*   A model's changed hash is now exposed for easy reading of the changed attribute delta, since the model's last `"change"` event.
*   Added where to collections for simple filtering.
*   You can now use a single off call to remove all callbacks bound to a specific object.
*   Bug fixes for nested individual change events, some of which may be "silent".
*   Bug fixes for URL encoding in `location.hash` fragments.
*   Bug fix for client-side validation in advance of a `save` call with `{wait: true}`.
*   Updated / refreshed the example Todo List app.

**0.9.1** — *Feb. 2, 2012* — [Diff](https://github.com/jashkenas/backbone/compare/0.9.0...0.9.1) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.9.1/index.html)

*   Reverted to 0.5.3-esque behavior for validating models. Silent changes no longer trigger validation (making it easier to work with forms). Added an `isValid` function that you can use to check if a model is currently in a valid state.
*   If you have multiple versions of jQuery on the page, you can now tell Backbone which one to use with `Backbone.setDomLibrary`.
*   Fixes regressions in **0.9.0** for routing with "root", saving with both "wait" and "validate", and the order of nested "change" events.

**0.9.0** — *Jan. 30, 2012* — [Diff](https://github.com/jashkenas/backbone/compare/0.5.3...0.9.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.9.0/index.html)

*   Creating and destroying models with `create` and `destroy` are now optimistic by default. Pass `{wait: true}` as an option if you'd like them to wait for a successful server response to proceed.
*   Two new properties on views: `$el` — a cached jQuery (or Zepto) reference to the view's element, and `setElement`, which should be used instead of manually setting a view's `el`. It will both set `view.el` and `view.$el` correctly, as well as re-delegating events on the new DOM element.
*   You can now bind and trigger multiple spaced-delimited events at once. For example: `model.on("change:name change:age", ...)`
*   When you don't know the key in advance, you may now call `model.set(key, value)` as well as `save`.
*   Multiple models with the same `id` are no longer allowed in a single collection.
*   Added a `"sync"` event, which triggers whenever a model's state has been successfully synced with the server (create, save, destroy).
*   `bind` and `unbind` have been renamed to `on` and `off` for clarity, following jQuery's lead. The old names are also still supported.
*   A Backbone collection's `comparator` function may now behave either like a [sortBy](http://www.css88.com/doc/underscore/#sortBy) (pass a function that takes a single argument), or like a [sort](https://developer.mozilla.org/JavaScript/Reference/Global_Objects/Array/sort) (pass a comparator function that expects two arguments). The comparator function is also now bound by default to the collection — so you can refer to `this` within it.
*   A view's `events` hash may now also contain direct function values as well as the string names of existing view methods.
*   Validation has gotten an overhaul — a model's `validate` function will now be run even for silent changes, and you can no longer create a model in an initially invalid state.
*   Added `shuffle` and `initial` to collections, proxied from Underscore.
*   `Model#urlRoot` may now be defined as a function as well as a value.
*   `View#attributes` may now be defined as a function as well as a value.
*   Calling `fetch` on a collection will now cause all fetched JSON to be run through the collection's model's `parse` function, if one is defined.
*   You may now tell a router to `navigate(fragment, {replace: true})`, which will either use `history.replaceState` or `location.hash.replace`, in order to change the URL without adding a history entry.
*   Within a collection's `add` and `remove` events, the index of the model being added or removed is now available as `options.index`.
*   Added an `undelegateEvents` to views, allowing you to manually remove all configured event delegations.
*   Although you shouldn't be writing your routes with them in any case — leading slashes (`/`) are now stripped from routes.
*   Calling `clone` on a model now only passes the attributes for duplication, not a reference to the model itself.
*   Calling `clear` on a model now removes the `id` attribute.

**0.5.3** — *August 9, 2011* — [Diff](https://github.com/jashkenas/backbone/compare/0.5.2...0.5.3) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.5.3/index.html) A View's `events` property may now be defined as a function, as well as an object literal, making it easier to programmatically define and inherit events. `groupBy` is now proxied from Underscore as a method on Collections. If the server has already rendered everything on page load, pass `Backbone.history.start({silent: true})` to prevent the initial route from triggering. Bugfix for pushState with encoded URLs.

**0.5.2** — *July 26, 2011* — [Diff](https://github.com/jashkenas/backbone/compare/0.5.1...0.5.2) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.5.2/index.html) The `bind` function, can now take an optional third argument, to specify the `this` of the callback function. Multiple models with the same `id` are now allowed in a collection. Fixed a bug where calling `.fetch(jQueryOptions)` could cause an incorrect URL to be serialized. Fixed a brief extra route fire before redirect, when degrading from `pushState`.

**0.5.1** — *July 5, 2011* — [Diff](https://github.com/jashkenas/backbone/compare/0.5.0...0.5.1) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.5.1/index.html) Cleanups from the 0.5.0 release, to wit: improved transparent upgrades from hash-based URLs to pushState, and vice-versa. Fixed inconsistency with non-modified attributes being passed to `Model#initialize`. Reverted a **0.5.0** change that would strip leading hashbangs from routes. Added `contains` as an alias for `includes`.

**0.5.0** — *July 1, 2011* — [Diff](https://github.com/jashkenas/backbone/compare/0.3.3...0.5.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.5.0/index.html) A large number of tiny tweaks and micro bugfixes, best viewed by looking at [the commit diff](https://github.com/jashkenas/backbone/compare/0.3.3...0.5.0). HTML5 `pushState` support, enabled by opting-in with: `Backbone.history.start({pushState: true})`. `Controller` was renamed to `Router`, for clarity. `Collection#refresh` was renamed to `Collection#reset` to emphasize its ability to both reset the collection with new models, as well as empty out the collection when used with no parameters. `saveLocation` was replaced with `navigate`. RESTful persistence methods (save, fetch, etc.) now return the jQuery deferred object for further success/error chaining and general convenience. Improved XSS escaping for `Model#escape`. Added a `urlRoot` option to allow specifying RESTful urls without the use of a collection. An error is thrown if `Backbone.history.start` is called multiple times. `Collection#create` now validates before initializing the new model. `view.el` can now be a jQuery string lookup. Backbone Views can now also take an `attributes` parameter. `Model#defaults` can now be a function as well as a literal attributes object.

**0.3.3** — *Dec 1, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.3.2...0.3.3) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.3.3/index.html) Backbone.js now supports [Zepto](http://zeptojs.com), alongside jQuery, as a framework for DOM manipulation and Ajax support. Implemented Model#escape, to efficiently handle attributes intended for HTML interpolation. When trying to persist a model, failed requests will now trigger an `"error"` event. The ubiquitous `options` argument is now passed as the final argument to all `"change"` events.

**0.3.2** — *Nov 23, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.3.1...0.3.2) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.3.2/index.html) Bugfix for IE7 + iframe-based "hashchange" events. `sync` may now be overridden on a per-model, or per-collection basis. Fixed recursion error when calling `save` with no changed attributes, within a `"change"` event.

**0.3.1** — *Nov 15, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.3.0...0.3.1) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.3.1/index.html) All `"add"` and `"remove"` events are now sent through the model, so that views can listen for them without having to know about the collection. Added a `remove` method to Backbone.View. `toJSON` is no longer called at all for `'read'` and `'delete'` requests. Backbone routes are now able to load empty URL fragments.

**0.3.0** — *Nov 9, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.2.0...0.3.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.3.0/index.html) Backbone now has Controllers and History, for doing client-side routing based on URL fragments. Added `emulateHTTP` to provide support for legacy servers that don't do `PUT` and `DELETE`. Added `emulateJSON` for servers that can't accept `application/json` encoded requests. Added Model#clear, which removes all attributes from a model. All Backbone classes may now be seamlessly inherited by CoffeeScript classes.

**0.2.0** — *Oct 25, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.1.2...0.2.0) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.2.0/index.html) Instead of requiring server responses to be namespaced under a `model` key, now you can define your own parse method to convert responses into attributes for Models and Collections. The old `handleEvents` function is now named delegateEvents, and is automatically called as part of the View's constructor. Added a toJSON function to Collections. Added Underscore's chain to Collections.

**0.1.2** — *Oct 19, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.1.1...0.1.2) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.1.2/index.html) Added a Model#fetch method for refreshing the attributes of single model from the server. An `error` callback may now be passed to `set` and `save` as an option, which will be invoked if validation fails, overriding the `"error"` event. You can now tell backbone to use the `_method` hack instead of HTTP methods by setting `Backbone.emulateHTTP = true`. Existing Model and Collection data is no longer sent up unnecessarily with `GET` and `DELETE` requests. Added a `rake lint` task. Backbone is now published as an [NPM](http://npmjs.org) module.

**0.1.1** — *Oct 14, 2010* — [Diff](https://github.com/jashkenas/backbone/compare/0.1.0...0.1.1) — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.1.1/index.html) Added a convention for `initialize` functions to be called upon instance construction, if defined. Documentation tweaks.

**0.1.0** — *Oct 13, 2010* — [Docs](https://cdn.rawgit.com/jashkenas/backbone/0.1.0/index.html) Initial Backbone release.