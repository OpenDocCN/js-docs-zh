# Examples

## Examples

The list of examples that follows, while long, is not exhaustive. If you've worked on an app that uses Backbone, please add it to the [wiki page of Backbone apps](https://github.com/jashkenas/backbone/wiki/Projects-and-Companies-using-Backbone).

[Jérôme Gravel-Niquet](http://jgn.me/) has contributed a Todo List application that is bundled in the repository as Backbone example. If you're wondering where to get started with Backbone in general, take a moment to read through the annotated source. The app uses a [LocalStorage adapter](http://github.com/jeromegn/Backbone.localStorage) to transparently save all of your todos within your browser, instead of sending them to a server. Jérôme also has a version hosted at [localtodos.com](http://localtodos.com/).

### DocumentCloud

The [DocumentCloud workspace](http://www.documentcloud.org/public/#search/) is built on Backbone.js, with *Documents*, *Projects*, *Notes*, and *Accounts* all as Backbone models and collections. If you're interested in history — both Underscore.js and Backbone.js were originally extracted from the DocumentCloud codebase, and packaged into standalone JS libraries.

### USA Today

[USA Today](http://usatoday.com) takes advantage of the modularity of Backbone's data/model lifecycle — which makes it simple to create, inherit, isolate, and link application objects — to keep the codebase both manageable and efficient. The new website also makes heavy use of the Backbone Router to control the page for both pushState-capable and legacy browsers. Finally, the team took advantage of Backbone's Event module to create a PubSub API that allows third parties and analytics packages to hook into the heart of the app.

### Rdio

[New Rdio](http://rdio.com/new) was developed from the ground up with a component based framework based on Backbone.js. Every component on the screen is dynamically loaded and rendered, with data provided by the [Rdio API](http://developer.rdio.com/). When changes are pushed, every component can update itself without reloading the page or interrupting the user's music. All of this relies on Backbone's views and models, and all URL routing is handled by Backbone's Router. When data changes are signaled in realtime, Backbone's Events notify the interested components in the data changes. Backbone forms the core of the new, dynamic, realtime Rdio web and *desktop* applications.

### Hulu

[Hulu](http://hulu.com) used Backbone.js to build its next generation online video experience. With Backbone as a foundation, the web interface was rewritten from scratch so that all page content can be loaded dynamically with smooth transitions as you navigate. Backbone makes it easy to move through the app quickly without the reloading of scripts and embedded videos, while also offering models and collections for additional data manipulation support.

### Quartz

[Quartz](http://qz.com) sees itself as a digitally native news outlet for the new global economy. Because Quartz believes in the future of open, cross-platform web applications, they selected Backbone and Underscore to fetch, sort, store, and display content from a custom WordPress API. Although [qz.com](http://qz.com) uses responsive design for phone, tablet, and desktop browsers, it also takes advantage of Backbone events and views to render device-specific templates in some cases.

### Earth

[Earth.nullschool.net](http://earth.nullschool.net) displays real-time weather conditions on an interactive animated globe, and Backbone provides the foundation upon which all of the site's components are built. Despite the presence of several other javascript libraries, Backbone's non-opinionated design made it effortless to mix-in the Events functionality used for distributing state changes throughout the page. When the decision was made to switch to Backbone, large blocks of custom logic simply disappeared.

### Vox

Vox Media, the publisher of [SB Nation](http://www.sbnation.com/), [The Verge](http://www.theverge.com/), [Polygon](http://www.polygon.com/), [Eater](http://www.eater.com/), [Racked](http://www.racked.com/), [Curbed](http://www.curbed.com/), and [Vox.com](http://www.vox.com/), uses Backbone throughout [Chorus](http://techcrunch.com/2012/05/07/a-closer-look-at-chorus-the-next-generation-publishing-platform-that-runs-vox-media/), its home-grown publishing platform. Backbone powers the [liveblogging platform](http://product.voxmedia.com/post/25113965826/introducing-syllabus-vox-medias-s3-powered-liveblog) and [commenting system](http://product.voxmedia.com/2013/11/11/5426878/using-backbone-js-for-sanity-and-stability) used across all Vox Media properties; Coverage, an internal editorial coordination tool; [SB Nation Live](http://www.sbnation.com/college-basketball/2014/4/7/5592112/kentucky-vs-uconn-2014-ncaa-tournament-championship-live-chat), a live event coverage and chat tool; and [Vox Cards](http://www.vox.com/cards/ukraine-everything-you-need-to-know/what-is-the-ukraine-crisis), Vox.com's highlighter-and-index-card inspired app for providing context about the news.

### Gawker Media

[Kinja](http://kinja.com) is Gawker Media's publishing platform designed to create great stories by breaking down the lines between the traditional roles of content creators and consumers. Everyone — editors, readers, marketers — have access to the same tools to engage in passionate discussion and pursue the truth of the story. Sharing, recommending, and following within the Kinja ecosystem allows for improved information discovery across all the sites.

Kinja is the platform behind [Gawker](http://gawker.com/), [Gizmodo](http://gizmodo.com/), [Lifehacker](http://lifehacker.com/), [io9](http://io9.com/) and other Gawker Media blogs. Backbone.js underlies the front-end application code that powers everything from user authentication to post authoring, commenting, and even serving ads. The JavaScript stack includes [Underscore.js](http://www.css88.com/doc/underscore/) and [jQuery](http://jquery.com/), with some plugins, all loaded with [RequireJS](http://requirejs.org/). Closure templates are shared between the [Play! Framework](http://www.playframework.com/) based Scala application and Backbone views, and the responsive layout is done with the [Foundation](http://foundation.zurb.com/) framework using [SASS](http://sass-lang.com/).

### Flow

[MetaLab](http://www.metalabdesign.com/) used Backbone.js to create [Flow](http://www.getflow.com/), a task management app for teams. The workspace relies on Backbone.js to construct task views, activities, accounts, folders, projects, and tags. You can see the internals under `window.Flow`.

### Gilt Groupe

[Gilt Groupe](http://gilt.com) uses Backbone.js to build multiple applications across their family of sites. [Gilt's mobile website](http://m.gilt.com) uses Backbone and [Zepto.js](http://zeptojs.com) to create a blazing-fast shopping experience for users on-the-go, while [Gilt Live](http://live.gilt.com) combines Backbone with WebSockets to display the items that customers are buying in real-time. Gilt's search functionality also uses Backbone to filter and sort products efficiently by moving those actions to the client-side.

### Enigma

[Enigma](http://enigma.io) is a portal amassing the largest collection of public data produced by governments, universities, companies, and organizations. Enigma uses Backbone Models and Collections to represent complex data structures; and Backbone's Router gives Enigma users unique URLs for application states, allowing them to navigate quickly through the site while maintaining the ability to bookmark pages and navigate forward and backward through their session.

### NewsBlur

[NewsBlur](http://www.newsblur.com) is an RSS feed reader and social news network with a fast and responsive UI that feels like a native desktop app. Backbone.js was selected for [a major rewrite and transition from spaghetti code](http://www.ofbrooklyn.com/2012/11/13/backbonification-migrating-javascript-to-backbone/) because of its powerful yet simple feature set, easy integration, and large community. If you want to poke around under the hood, NewsBlur is also entirely [open-source](http://github.com/samuelclay/NewsBlur).

### WordPress.com

[WordPress.com](http://wordpress.com/) is the software-as-a-service version of [WordPress](http://wordpress.org). It uses Backbone.js Models, Collections, and Views in its [Notifications system](http://en.blog.wordpress.com/2012/05/25/notifications-refreshed/). Backbone.js was selected because it was easy to fit into the structure of the application, not the other way around. [Automattic](http://automattic.com) (the company behind WordPress.com) is integrating Backbone.js into the Stats tab and other features throughout the homepage.

### Foursquare

Foursquare is a fun little startup that helps you meet up with friends, discover new places, and save money. Backbone Models are heavily used in the core JavaScript API layer and Views power many popular features like the [homepage map](https://foursquare.com) and [lists](https://foursquare.com/seriouseats/list/the-best-doughnuts-in-ny).

### Bitbucket

[Bitbucket](http://www.bitbucket.org) is a free source code hosting service for Git and Mercurial. Through its models and collections, Backbone.js has proved valuable in supporting Bitbucket's [REST API](https://api.bitbucket.org), as well as newer components such as in-line code comments and approvals for pull requests. Mustache templates provide server and client-side rendering, while a custom [Google Closure](https://developers.google.com/closure/library/) inspired life-cycle for widgets allows Bitbucket to decorate existing DOM trees and insert new ones.

### Disqus

[Disqus](http://www.disqus.com) chose Backbone.js to power the latest version of their commenting widget. Backbone’s small footprint and easy extensibility made it the right choice for Disqus’ distributed web application, which is hosted entirely inside an iframe and served on thousands of large web properties, including IGN, Wired, CNN, MLB, and more.

### Delicious

[Delicious](https://delicious.com/) is a social bookmarking platform making it easy to save, sort, and store bookmarks from across the web. Delicious uses [Chaplin.js](http://chaplinjs.org), Backbone.js and AppCache to build a full-featured MVC web app. The use of Backbone helped the website and [mobile apps](http://delicious.com/tools) share a single API service, and the reuse of the model tier made it significantly easier to share code during the recent Delicious redesign.

![Delicious](http://www.delicious.com)

### Khan Academy

[Khan Academy](http://www.khanacademy.org) is on a mission to provide a free world-class education to anyone anywhere. With thousands of videos, hundreds of JavaScript-driven exercises, and big plans for the future, Khan Academy uses Backbone to keep frontend code modular and organized. User profiles and goal setting are implemented with Backbone, [jQuery](http://jquery.com/) and [Handlebars](http://handlebarsjs.com/), and most new feature work is being pushed to the client side, greatly increasing the quality of [the API](https://github.com/Khan/khan-api/).

![Khan Academy](http://www.khanacademy.org)

### IRCCloud

[IRCCloud](http://irccloud.com/) is an always-connected IRC client that you use in your browser — often leaving it open all day in a tab. The sleek web interface communicates with an Erlang backend via websockets and the [IRCCloud API](https://github.com/irccloud/irccloud-tools/wiki/API-Overview). It makes heavy use of Backbone.js events, models, views and routing to keep your IRC conversations flowing in real time.

![IRCCloud](http://irccloud.com/)

### Pitchfork

[Pitchfork](http://pitchfork.com/) uses Backbone.js to power its site-wide audio player, [Pitchfork.tv](http://pitchfork.com/tv/), location routing, a write-thru page fragment cache, and more. Backbone.js (and [Underscore.js](http://www.css88.com/doc/underscore/)) helps the team create clean and modular components, move very quickly, and focus on the site, not the spaghetti.

![Pitchfork](http://pitchfork.com/)

### Spin

[Spin](http://spin.com/) pulls in the [latest news stories](http://www.spin.com/news) from their internal API onto their site using Backbone models and collections, and a custom `sync` method. Because the music should never stop playing, even as you click through to different "pages", Spin uses a Backbone router for navigation within the site.

![Spin](http://spin.com/)

### ZocDoc

[ZocDoc](http://www.zocdoc.com) helps patients find local, in-network doctors and dentists, see their real-time availability, and instantly book appointments. On the public side, the webapp uses Backbone.js to handle client-side state and rendering in [search pages](http://www.zocdoc.com/primary-care-doctors/los-angeles-13122pm) and [doctor profiles](http://www.zocdoc.com/doctor/nathan-hashimoto-md-58078). In addition, the new version of the doctor-facing part of the website is a large single-page application that benefits from Backbone's structure and modularity. ZocDoc's Backbone classes are tested with [Jasmine](http://pivotal.github.io/jasmine/), and delivered to the end user with [Cassette](http://getcassette.net/).

![ZocDoc](http://www.zocdoc.com)

### Walmart Mobile

[Walmart](http://www.walmart.com/) used Backbone.js to create the new version of [their mobile web application](http://mobile.walmart.com/) and created two new frameworks in the process. [Thorax](http://walmartlabs.github.com/thorax/) provides mixins, inheritable events, as well as model and collection view bindings that integrate directly with [Handlebars](http://handlebarsjs.com/) templates. [Lumbar](http://walmartlabs.github.com/lumbar/) allows the application to be split into modules which can be loaded on demand, and creates platform specific builds for the portions of the web application that are embedded in Walmart's native Android and iOS applications.

![Walmart Mobile](http://mobile.walmart.com/r/phoenix)

### Groupon Now!

[Groupon Now!](http://www.groupon.com/now) helps you find local deals that you can buy and use right now. When first developing the product, the team decided it would be AJAX heavy with smooth transitions between sections instead of full refreshes, but still needed to be fully linkable and shareable. Despite never having used Backbone before, the learning curve was incredibly quick — a prototype was hacked out in an afternoon, and the team was able to ship the product in two weeks. Because the source is minimal and understandable, it was easy to add several Backbone extensions for Groupon Now!: changing the router to handle URLs with querystring parameters, and adding a simple in-memory store for caching repeated requests for the same data.

![Groupon Now!](http://www.groupon.com/now)

### Basecamp

[37Signals](http://37signals.com/) chose Backbone.js to create the [calendar feature](http://basecamp.com/calendar) of its popular project management software [Basecamp](http://basecamp.com/). The Basecamp Calendar uses Backbone.js models and views in conjunction with the [Eco](https://github.com/sstephenson/eco) templating system to present a polished, highly interactive group scheduling interface.

![Basecamp Calendar](http://basecamp.com/calendar)

### Slavery Footprint

[Slavery Footprint](http://slaveryfootprint.org/survey) allows consumers to visualize how their consumption habits are connected to modern-day slavery and provides them with an opportunity to have a deeper conversation with the companies that manufacture the goods they purchased. Based in Oakland, California, the Slavery Footprint team works to engage individuals, groups, and businesses to build awareness for and create deployable action against forced labor, human trafficking, and modern-day slavery through online tools, as well as off-line community education and mobilization programs.

![Slavery Footprint](http://slaveryfootprint.org/survey)

### Stripe

[Stripe](https://stripe.com) provides an API for accepting credit cards on the web. Stripe's [management interface](https://manage.stripe.com) was recently rewritten from scratch in CoffeeScript using Backbone.js as the primary framework, [Eco](https://github.com/sstephenson/eco) for templates, [Sass](http://sass-lang.com/) for stylesheets, and [Stitch](https://github.com/sstephenson/stitch) to package everything together as [CommonJS](http://commonjs.org/) modules. The new app uses [Stripe's API](https://stripe.com/docs/api) directly for the majority of its actions; Backbone.js models made it simple to map client-side models to their corresponding RESTful resources.

![Stripe](https://stripe.com)

### Airbnb

[Airbnb](http://airbnb.com) uses Backbone in many of its products. It started with [Airbnb Mobile Web](http://m.airbnb.com) (built in six weeks by a team of three) and has since grown to [Wish Lists](https://www.airbnb.com/wishlists/popular), [Match](http://www.airbnb.com/match), [Search](http://www.airbnb.com/s/), Communities, Payments, and Internal Tools.

![Airbnb](http://m.airbnb.com/)

### SoundCloud Mobile

[SoundCloud](http://soundcloud.com) is the leading sound sharing platform on the internet, and Backbone.js provides the foundation for [SoundCloud Mobile](http://m.soundcloud.com). The project uses the public SoundCloud [API](http://soundcloud.com/developers) as a data source (channeled through a nginx proxy), [jQuery templates](http://www.css88.com/jqapi-1.9/category/plugins/templates/) for the rendering, [Qunit](http://docs.jquery.com/Qunit) and [PhantomJS](http://www.phantomjs.org/) for the testing suite. The JS code, templates and CSS are built for the production deployment with various Node.js tools like [ready.js](https://github.com/dsimard/ready.js), [Jake](https://github.com/mde/jake), [jsdom](https://github.com/tmpvar/jsdom). The **Backbone.History** was modified to support the HTML5 `history.pushState`. **Backbone.sync** was extended with an additional SessionStorage based cache layer.

![SoundCloud](http://m.soundcloud.com)

### Art.sy

[Art.sy](http://artsy.net) is a place to discover art you'll love. Art.sy is built on Rails, using [Grape](https://github.com/intridea/grape) to serve a robust [JSON API](http://artsy.net/api). The main site is a single page app written in CoffeeScript and uses Backbone to provide structure around this API. An admin panel and partner CMS have also been extracted into their own API-consuming Backbone projects.

### Pandora

When [Pandora](http://www.pandora.com/newpandora) redesigned their site in HTML5, they chose Backbone.js to help manage the user interface and interactions. For example, there's a model that represents the "currently playing track", and multiple views that automatically update when the current track changes. The station list is a collection, so that when stations are added or changed, the UI stays up to date.

### Inkling

[Inkling](http://inkling.com/) is a cross-platform way to publish interactive learning content. [Inkling for Web](https://www.inkling.com/read/) uses Backbone.js to make hundreds of complex books — from student textbooks to travel guides and programming manuals — engaging and accessible on the web. Inkling supports WebGL-enabled 3D graphics, interactive assessments, social sharing, and a system for running practice code right in the book, all within a single page Backbone-driven app. Early on, the team decided to keep the site lightweight by using only Backbone.js and raw JavaScript. The result? Complete source code weighing in at a mere 350kb with feature-parity across the iPad, iPhone and web clients. Give it a try with [this excerpt from JavaScript: The Definitive Guide](https://www.inkling.com/read/javascript-definitive-guide-david-flanagan-6th/chapter-4/function-definition-expressions).

### Code School

[Code School](http://www.codeschool.com) courses teach people about various programming topics like [CoffeeScript](http://coffeescript.org), CSS, Ruby on Rails, and more. The new Code School course [challenge page](http://coffeescript.codeschool.com/levels/1/challenges/1) is built from the ground up on Backbone.js, using everything it has to offer: the router, collections, models, and complex event handling. Before, the page was a mess of [jQuery](http://jquery.com/) DOM manipulation and manual Ajax calls. Backbone.js helped introduce a new way to think about developing an organized front-end application in JavaScript.

### CloudApp

[CloudApp](http://getcloudapp.com) is simple file and link sharing for the Mac. Backbone.js powers the web tools which consume the [documented API](http://developer.getcloudapp.com) to manage Drops. Data is either pulled manually or pushed by [Pusher](http://pusher.com) and fed to [Mustache](http://github.com/janl/mustache.js) templates for rendering. Check out the [annotated source code](http://cloudapp.github.com/engine) to see the magic.

![CloudApp](http://getcloudapp.com)

### SeatGeek

[SeatGeek](http://seatgeek.com)'s stadium ticket maps were originally developed with [Prototype.js](http://prototypejs.org/). Moving to Backbone.js and [jQuery](http://jquery.com/) helped organize a lot of the UI code, and the increased structure has made adding features a lot easier. SeatGeek is also in the process of building a mobile interface that will be Backbone.js from top to bottom.

![SeatGeek](http://seatgeek.com)

### Easel

[Easel](http://easel.io) is an in-browser, high fidelity web design tool that integrates with your design and development process. The Easel team uses CoffeeScript, Underscore.js and Backbone.js for their [rich visual editor](http://easel.io/demo) as well as other management functions throughout the site. The structure of Backbone allowed the team to break the complex problem of building a visual editor into manageable components and still move quickly.

![Easel](http://easel.io)

### Jolicloud

[Jolicloud](http://www.jolicloud.com/) is an open and independent platform and [operating system](http://www.jolicloud.com/jolios) that provides music playback, video streaming, photo browsing and document editing — transforming low cost computers into beautiful cloud devices. The [new Jolicloud HTML5 app](https://my.jolicloud.com/) was built from the ground up using Backbone and talks to the [Jolicloud Platform](http://developers.jolicloud.com), which is based on Node.js. Jolicloud works offline using the HTML5 AppCache, extends Backbone.sync to store data in IndexedDB or localStorage, and communicates with the [Joli OS](http://www.jolicloud.com/jolios) via WebSockets.

![Jolicloud](http://jolicloud.com/)

### Salon.io

[Salon.io](http://salon.io) provides a space where photographers, artists and designers freely arrange their visual art on virtual walls. [Salon.io](http://salon.io) runs on [Rails](http://rubyonrails.org/), but does not use much of the traditional stack, as the entire frontend is designed as a single page web app, using Backbone.js, [Brunch](http://brunch.io/) and [CoffeeScript](http://coffeescript.org).

![Salon.io](http://salon.io)

### TileMill

Our fellow [Knight Foundation News Challenge](http://www.newschallenge.org/) winners, [MapBox](http://mapbox.com/), created an open-source map design studio with Backbone.js: [TileMill](https://www.mapbox.com/tilemill/). TileMill lets you manage map layers based on shapefiles and rasters, and edit their appearance directly in the browser with the [Carto styling language](https://github.com/mapbox/carto). Note that the gorgeous [MapBox](http://mapbox.com/) homepage is also a Backbone.js app.

### Blossom

[Blossom](http://blossom.io) is a lightweight project management tool for lean teams. Backbone.js is heavily used in combination with [CoffeeScript](http://coffeescript.org) to provide a smooth interaction experience. The app is packaged with [Brunch](http://brunch.io). The RESTful backend is built with [Flask](http://flask.pocoo.org/) on Google App Engine.

![Blossom](http://blossom.io)

### Trello

[Trello](http://trello.com) is a collaboration tool that organizes your projects into boards. A Trello board holds many lists of cards, which can contain checklists, files and conversations, and may be voted on and organized with labels. Updates on the board happen in real time. The site was built ground up using Backbone.js for all the models, views, and routes.

![Trello](http://trello.com)

### Tzigla

[Cristi Balan](http://twitter.com/evilchelu) and [Irina Dumitrascu](http://dira.ro) created [Tzigla](http://tzigla.com), a collaborative drawing application where artists make tiles that connect to each other to create [surreal drawings](http://tzigla.com/boards/1). Backbone models help organize the code, routers provide [bookmarkable deep links](http://tzigla.com/boards/1#!/tiles/2-2), and the views are rendered with [haml.js](https://github.com/creationix/haml-js) and [Zepto](http://zeptojs.com/). Tzigla is written in Ruby ([Rails](http://rubyonrails.org/)) on the backend, and [CoffeeScript](http://coffeescript.org) on the frontend, with [Jammit](http://documentcloud.github.com/jammit/) prepackaging the static assets.

![Tzigla](http://www.tzigla.com/)