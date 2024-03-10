# F.A.Q.

## F.A.Q.

**Why use Backbone, not [other framework X]?** If your eye hasn't already been caught by the adaptability and elan on display in the above list of examples, we can get more specific: Backbone.js aims to provide the common foundation that data-rich web applications with ambitious interfaces require — while very deliberately avoiding painting you into a corner by making any decisions that you're better equipped to make yourself.

*   The focus is on supplying you with helpful methods to manipulate and query your data, not on HTML widgets or reinventing the JavaScript object model.
*   Backbone does not force you to use a single template engine. Views can bind to HTML constructed in [your](http://www.css88.com/doc/underscore/#template) [favorite](http://guides.rubyonrails.org/layouts_and_rendering.html) [way](http://mustache.github.com).
*   It's smaller. There are fewer kilobytes for your browser or phone to download, and less *conceptual* surface area. You can read and understand the source in an afternoon.
*   It doesn't depend on stuffing application logic into your HTML. There's no embedded JavaScript, template logic, or binding hookup code in `data-` or `ng-` attributes, and no need to invent your own HTML tags.
*   Synchronous events are used as the fundamental building block, not a difficult-to-reason-about run loop, or by constantly polling and traversing your data structures to hunt for changes. And if you want a specific event to be asynchronous and aggregated, [no problem](http://www.css88.com/doc/underscore/#debounce).
*   Backbone scales well, from [embedded widgets](http://disqus.com) to [massive apps](http://www.usatoday.com).
*   Backbone is a library, not a framework, and plays well with others. You can embed Backbone widgets in Dojo apps without trouble, or use Backbone models as the data backing for D3 visualizations (to pick two entirely random examples).
*   "Two-way data-binding" is avoided. While it certainly makes for a nifty demo, and works for the most basic CRUD, it doesn't tend to be terribly useful in your real-world app. Sometimes you want to update on every keypress, sometimes on blur, sometimes when the panel is closed, and sometimes when the "save" button is clicked. In almost all cases, simply serializing the form to JSON is faster and easier. All that aside, if your heart is set, [go](http://rivetsjs.com) [for it](http://nytimes.github.com/backbone.stickit/).
*   There's no built-in performance penalty for choosing to structure your code with Backbone. And if you do want to optimize further, thin models and templates with flexible granularity make it easy to squeeze every last drop of potential performance out of, say, IE8.

**There's More Than One Way To Do It** It's common for folks just getting started to treat the examples listed on this page as some sort of gospel truth. In fact, Backbone.js is intended to be fairly agnostic about many common patterns in client-side code. For example...

**References between Models and Views** can be handled several ways. Some people like to have direct pointers, where views correspond 1:1 with models (`model.view` and `view.model`). Others prefer to have intermediate "controller" objects that orchestrate the creation and organization of views into a hierarchy. Others still prefer the evented approach, and always fire events instead of calling methods directly. All of these styles work well.

**Batch operations** on Models are common, but often best handled differently depending on your server-side setup. Some folks don't mind making individual Ajax requests. Others create explicit resources for RESTful batch operations: `/notes/batch/destroy?ids=1,2,3,4`. Others tunnel REST over JSON, with the creation of "changeset" requests:

```js
 {
    "create":  [array of models to create]
    "update":  [array of models to update]
    "destroy": [array of model ids to destroy]
  } 
```

**Feel free to define your own events.** Backbone.Events is designed so that you can mix it in to any JavaScript object or prototype. Since you can use any string as an event, it's often handy to bind and trigger your own custom events: `model.on("selected:true")` or `model.on("editing")`

**Render the UI** as you see fit. Backbone is agnostic as to whether you use [Underscore templates](http://www.css88.com/doc/underscore/#template), [Mustache.js](https://github.com/janl/mustache.js), direct DOM manipulation, server-side rendered snippets of HTML, or [jQuery UI](http://jqueryui.com/) in your `render` function. Sometimes you'll create a view for each model ... sometimes you'll have a view that renders thousands of models at once, in a tight loop. Both can be appropriate in the same app, depending on the quantity of data involved, and the complexity of the UI.

**Nested Models & Collections** It's common to nest collections inside of models with Backbone. For example, consider a `Mailbox` model that contains many `Message` models. One nice pattern for handling this is have a `this.messages` collection for each mailbox, enabling the lazy-loading of messages, when the mailbox is first opened ... perhaps with `MessageList` views listening for `"add"` and `"remove"` events.

```js
var Mailbox = Backbone.Model.extend({

  initialize: function() {
    this.messages = new Messages;
    this.messages.url = '/mailbox/' + this.id + '/messages';
    this.messages.on("reset", this.updateCounts);
  },

  ...

});

var inbox = new Mailbox;

// And then, when the Inbox is opened:

inbox.messages.fetch({reset: true}); 
```

If you're looking for something more opinionated, there are a number of Backbone plugins that add sophisticated associations among models, [available on the wiki](https://github.com/jashkenas/backbone/wiki/Extensions%2C-Plugins%2C-Resources).

Backbone doesn't include direct support for nested models and collections or "has many" associations because there are a number of good patterns for modeling structured data on the client side, and *Backbone should provide the foundation for implementing any of them.* You may want to…

*   Mirror an SQL database's structure, or the structure of a NoSQL database.
*   Use models with arrays of "foreign key" ids, and join to top level collections (a-la tables).
*   For associations that are numerous, use a range of ids instead of an explicit list.
*   Avoid ids, and use direct references, creating a partial object graph representing your data set.
*   Lazily load joined models from the server, or lazily deserialize nested models from JSON documents.

**Loading Bootstrapped Models** When your app first loads, it's common to have a set of initial models that you know you're going to need, in order to render the page. Instead of firing an extra AJAX request to fetch them, a nicer pattern is to have their data already bootstrapped into the page. You can then use reset to populate your collections with the initial data. At DocumentCloud, in the [ERB](http://en.wikipedia.org/wiki/ERuby) template for the workspace, we do something along these lines:

```js
<script>
  var accounts = new Backbone.Collection;
  accounts.reset(<%= @accounts.to_json %>);
  var projects = new Backbone.Collection;
  projects.reset(<%= @projects.to_json(:collaborators => true) %>);
</script> 
```

You have to [escape](http://mathiasbynens.be/notes/etago) `&lt;/` within the JSON string, to prevent javascript injection attacks.

**Extending Backbone** Many JavaScript libraries are meant to be insular and self-enclosed, where you interact with them by calling their public API, but never peek inside at the guts. Backbone.js is *not* that kind of library.

Because it serves as a foundation for your application, you're meant to extend and enhance it in the ways you see fit — the entire source code is annotated to make this easier for you. You'll find that there's very little there apart from core functions, and most of those can be overridden or augmented should you find the need. If you catch yourself adding methods to `Backbone.Model.prototype`, or creating your own base subclass, don't worry — that's how things are supposed to work.

**How does Backbone relate to "traditional" MVC?** Different implementations of the [Model-View-Controller](http://en.wikipedia.org/wiki/Model–View–Controller) pattern tend to disagree about the definition of a controller. If it helps any, in Backbone, the View class can also be thought of as a kind of controller, dispatching events that originate from the UI, with the HTML template serving as the true view. We call it a View because it represents a logical chunk of UI, responsible for the contents of a single DOM element.

Comparing the overall structure of Backbone to a server-side MVC framework like **Rails**, the pieces line up like so:

*   **Backbone.Model** – Like a Rails model minus the class methods. Wraps a row of data in business logic.
*   **Backbone.Collection** – A group of models on the client-side, with sorting/filtering/aggregation logic.
*   **Backbone.Router** – Rails `routes.rb` + Rails controller actions. Maps URLs to functions.
*   **Backbone.View** – A logical, re-usable piece of UI. Often, but not always, associated with a model.
*   **Client-side Templates** – Rails `.html.erb` views, rendering a chunk of HTML.

**Binding "this"** Perhaps the single most common JavaScript "gotcha" is the fact that when you pass a function as a callback, its value for `this` is lost. When dealing with events and callbacks in Backbone, you'll often find it useful to rely on listenTo or the optional `context` argument that many of Underscore and Backbone's methods use to specify the `this` that will be used when the callback is later invoked. (See [_.each](http://www.css88.com/doc/underscore/#each), [_.map](http://www.css88.com/doc/underscore/#map), and object.on, to name a few). View events are automatically bound to the view's context for you. You may also find it helpful to use [_.bind](http://www.css88.com/doc/underscore/#bind) and [_.bindAll](http://www.css88.com/doc/underscore/#bindAll) from Underscore.js.

```js
var MessageList = Backbone.View.extend({

  initialize: function() {
    var messages = this.collection;
    messages.on("reset", this.render, this);
    messages.on("add", this.addMessage, this);
    messages.on("remove", this.removeMessage, this);

    messsages.each(this.addMessage, this);
  }

});

// Later, in the app...

Inbox.messages.add(newMessage); 
```

**Working with Rails** Backbone.js was originally extracted from [a Rails application](http://www.documentcloud.org); getting your client-side (Backbone) Models to sync correctly with your server-side (Rails) Models is painless, but there are still a few things to be aware of.

By default, Rails versions prior to 3.1 add an extra layer of wrapping around the JSON representation of models. You can disable this wrapping by setting:

```js
ActiveRecord::Base.include_root_in_json = false 
```

... in your configuration. Otherwise, override parse to pull model attributes out of the wrapper. Similarly, Backbone PUTs and POSTs direct JSON representations of models, where by default Rails expects namespaced attributes. You can have your controllers filter attributes directly from `params`, or you can override toJSON in Backbone to add the extra wrapping Rails expects.