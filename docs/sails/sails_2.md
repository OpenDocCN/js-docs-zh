# Reference

# sails-docs-reference

Reference Section of Sails.js documentation

## ideas for some restructuring:

```
 |
 |- Usage
   |
   |- Request (req)
   |
   |- Response (res)
   |
   |- Config (sails.config)
   |
   |- Model (sails.models)
   |
   |- Sockets (sails.sockets)
   |
   |- Sails CLI
   |
   |- Blueprint API
   |
   |- Browser SDK (sails.io.js)

 |
 |- Concepts
    |
    |- Security
    |
    |- Deployment
       |
       |- FAQ
       |- Hosting
       |- Scaling
    |
    |- Testing
    |
    |- Internationalization
    |
    |- Logging
    |
    |- File Uploads
    |
    |- Assets & Tasks
    |
    |- Middleware
    |
    |- Routes
    |
    |- Blueprints
    |
    |- Policies
    |
    |- Controllers
    |
    |- Custom Responses
    |
    |- Models
       |
       |- Attributes
       |- Validations
       |- Associations
       |- Lifecycle Callbacks
       |- Custom Schemas
       |- Migrations
    |
    |- Services
       |- todo: add example: Sending Email
    |
    |- Views

 |
 |- Advanced
    |
    |- Plugins
    |
    |- Programmatic Usage
    |
    |- Globals
    |
    |- .sailsrc 
```

<docmeta value="README541912" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="error" name="displayName" class="calibre17"></docmeta>

# Blueprint Api

# Blueprint API

### Overview

Together, blueprint routes and blueprint actions constitute the **blueprint API**, the built-in logic that powers the [RESTful JSON API](http://en.wikipedia.org/wiki/Representational_state_transfer) you get every time you create a model and controller.

For example, if you create a `User.js` model and `UserController.js` controller file in your project, then with blueprints enabled you will be able to immediately visit `/user/create?name=joe` to create a user, and visit `/user` to see an array of your app's users. All without writing a single line of code!

Blueprints are great for prototyping, but they are also a powerful tool in production due to their ability to be overridden, protected, extended or disabled entirely.

##### Blueprint Routes

When you run `sails lift` with blueprints enabled, the framework inspects your controllers, models, and configuration in order to bind certain routes automatically. These implicit blueprint routes (sometimes called "shadows") allow your app to respond to certain requests without you having to bind those routes manually in your `config/routes.js` file. By default, the blueprint routes point to their corresponding blueprint *actions* (see "Blueprint Actions" below), any of which can be overridden with custom code.

There are three types of blueprint routes in Sails:

*   **RESTful routes**, where the path is always `/:modelIdentity` or `/:modelIdentity/:id`. These routes use the HTTP "verb" to determine the action to take; for example a `POST` request to `/user` will create a new user, and a `DELETE` request to `/user/123` will delete the user whose primary key is 123\. In a production environment, RESTful routes should generally be protected by policies to avoid unauthorized access.
*   **Shortcut routes**, where the action to take is encoded in the path. For example, the `/user/create?name=joe` shortcut creates a new user, while `/user/update/1?name=mike` updates user #1\. These routes only respond to `GET` requests. Shortcut routes are very handy for development, but generally should be disabled in a production environment.
*   **Action routes**, which automatically create routes for your custom controller actions. For example, if you have a `FooController.js` file with a `bar` method, then a `/foo/bar` route will automatically be created for you as long as blueprint action routes are enabled. Unlike RESTful and shortcut routes, action routes do *not* require that a controller has a corresponding model file.

See the blueprints subsection of the configuration reference for blueprint configuration options, including how to enable / disable different blueprint route types.

##### Blueprint Actions

Blueprint actions (not to be confused with blueprint action *routes*) are generic actions designed to work with any of your controllers that have a model of the same name (e.g. `ParrotController` would need a `Parrot` model). Think of them as the default behavior for your application. For instance, if you have a `User.js` model and an empty `UserController.js` controller, `find`, `create`, `update`, `destroy`, `populate`, `add` and `remove` actions exist implicitly, without you having to write them.

By default, the blueprint RESTful routes and shortcut routes are bound to their corresponding blueprint actions. However, any blueprint action can be overridden for a particular controller by creating a custom action in that controller file (e.g. `ParrotController.find`). Alternatively, you can override the blueprint action *everywhere in your app* by creating your own custom blueprint action. (e.g. `api/blueprints/create.js`).

The current version of Sails ships with the following blueprint actions:

*   find
*   findOne
*   create onto a collection attribute of this record (the "primary" record).

*   If `:record_to_add` of an existing record is supplied, it will be associated with the primary record.
*   If no `:record_to_add` is supplied, and the body of the **POST** contains values for a new record, that record will be created and associated with the primary record.
*   If the collection within the primary record already contains a reference to the foreign record, this action will be ignored.
*   If the association is 2-way (i.e. reflexive, with "via" on both sides) the association on the foreign record will also be updated.

### Example

Add purchase 47 to the list of purchases that Dolly (employee #7) has been involved in.

**Using [jQuery](http://jquery.com/):**

```
$.post('/employee/7/involvedInPurchases/47', function (purchases) {
  console.log(purchases);
}); 
```

**Using [Angular](https://angularjs.org/):**

```
$http.post('/employee/7/involvedInPurchases/47')
.then(function (purchases) {
  console.log(purchases);
}); 
```

**Using [sails.io.js](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js):**

```
io.socket.post('/employee/7/involvedInPurchases/47', function (purchases) {
  console.log(purchases);
}); 
```

**Using [cURL](http://en.wikipedia.org/wiki/CURL):**

```
curl http://localhost:1337/employee/7/involvedInPurchases/47 -X "POST" 
```

Should return "Dolly", the primary record:

```
{
  "involvedInPurchases": [
    {
      "amount": 10000,
      "createdAt": "2014-08-03T01:50:33.898Z",
      "updatedAt": "2014-08-03T01:51:08.227Z",
      "id": 47,
      "cashier": 7
    }
  ],
  "name": "Dolly",
  "createdAt": "2014-08-03T01:16:35.440Z",
  "updatedAt": "2014-08-03T01:51:41.567Z",
  "id": 7
} 
```

### Notes

> *   This action is for dealing with *plural* ("collection") associations. If you want to set or unset a *singular* ("model") association, just use [update](http://sailsjs.org/#/documentation/reference/blueprint-api/Update.html).
> *   The example above assumes "rest" blueprints are enabled, and that your project contains at least an 'Employee' model with association: `involvedInPurchases: {collection: 'Purchase', via: 'cashier'}` as well as a `Purchase` model with association: `cashier: {model: 'Employee'}`. You'll also need at least an empty `PurchaseController` and `EmployeeController`. You can quickly achieve this by running:
>     
>     
>     
>     ```
>     $ sails new foo
>     $ cd foo
>     $ sails generate api purchase
>     $ sails generate api employee 
>     ```
>     
>     
> 
> ...then editing `api/models/Purchase.js` and `api/models/Employee.js`.

<docmeta value="Add262514" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="add to" name="displayName" class="calibre17"></docmeta>

# Create

# Create a Record

Creates a new model instance in your database then returns it's values.

```
POST /:model 
```

Attributes can be sent in the HTTP body as form-encoded values or JSON.

Responds with a JSON object representing the newly created instance. If a validation error occurred, a JSON response with the invalid attributes and a `400` status code will be returned instead.

Additionally, a `create` event will be published to all listening sockets (see the docs for [.watch()](https://github.com/balderdashy/sails-docs/blob/master/reference/ModelMethods.md#watchrequest) for more info).

If the action is triggered via a socket request, the requesting socket will ALSO be subscribed to the newly created model instance. If the record is subsequently updated or deleted, a message will be sent to that socket's client informing them of the change. See the docs for .subscribe() for more info.

### Parameters

| Parameter | Type | Details |
| --- | --- | --- |
| * | ((string)) ((number))
((object))
((array)) | For `POST` (RESTful) requests, pass in body parameter with the same name as the attribute defined on your model to set those values on your new record. For `GET` (shortcut) requests, add the parameters to the query string. 
Nested objects and arrays passed in as parameters are handled the same way as if they were passed into the model's .create() method. |
| callback | ((string)) | If specified, a JSONP response will be sent (instead of JSON). This is the name of the client-side javascript function to call, passing results as the first (and only) argument 
e.g. `?callback=myJSONPHandlerFn` |

### Examples

#### Create a record (REST)

Create a new pony named "AppleJack" with a hobby of "pickin".

#### Route

`POST /pony`

#### JSON Request Body

```
{
  "name": "AppleJack",
  "hobby": "pickin"
} 
```

#### Example Response

```
{
  "name": "AppleJack",
  "hobby": "pickin",
  "id": 47,
  "createdAt": "2013-10-18T01:23:56.000Z",
  "updatedAt": "2013-11-26T22:55:19.951Z"
} 
```

#### Create a record (shortcuts)

#### Route

`GET /pony/create?name=Shutterfly&best_pony=yep`

#### Expected Response

```
{
 "name": "Shutterfly",
 "best_pony": "yep",
 "createdAt": "2014-02-24T21:02:16.068Z",
 "updatedAt": "2014-02-24T21:02:16.068Z",
 "id": 5
} 
```

### Examples with One Way Associations

You can create associations between models in two different ways. You can either make the association with a record that already exists OR you can create both records simultaneously. Check out the examples to see how.

These examples assume the existence of `Pet` and `Pony` APIs which can be created by hand or using the Sails CLI Tool. The `Pony` model must be configured with a `pet` attribute pointing to the `Pet` model. See Model Association Docs for info on how to do this.

### Create record while associating w/ existing record (REST)

Create a new pony named "Pinkie Pie" and associate it with an existing pet named "Gummy" which has an `id` of 10.

#### Route

`POST /pony`

#### JSON Request Body

```
{
  "name": "Pinkie Pie",
  "hobby": "ice skating",
  "pet": 10
} 
```

#### Example Response

```
{
  "name": "Pinkie Pie",
  "hobby": "ice skating",
  "pet": {
    "name": "Gummy",
    "species": "crocodile",
    "id": 10
  },
  "id": 4,
  "createdAt": "2013-10-18T01:22:56.000Z",
  "updatedAt": "2013-11-26T22:54:19.951Z"
} 
```

### Create new record while associating w/ another new record (REST)

Create a new pony named "Pinkie Pie", an "ice skating" hobby, and a new pet named "Gummy".

#### Route

`POST /pony`

#### JSON Request Body

```
{
  "name": "Pinkie Pie",
  "hobby": "ice skating",
  "pet": {
    "name": "Gummy",
    "species": "crocodile"
  }
} 
```

#### Expected Response

# Destroy

# Destroy a Record

Deletes an existing record specified by `id` from the database forever and returns the values of the deleted record.

```
DELETE /:model/:record 
```

Destroys the model instance which matches the **id** parameter. Responds with a JSON object representing the newly destroyed instance. If no model instance exists matching the specified **id**, a `404` is returned.

Additionally, a `destroy` event will be published to all sockets subscribed to the instance room.

Consequently, all sockets currently subscribed to the instance will be unsubscribed from it.

### Parameters

| Parameter | Type | Details |
| --- | --- | --- |
| id *(required)* | ((number)) *-or-*
((string)) | The primary key value of the record to destroy. For `POST` (RESTful) requests, this can be supplied in the JSON body or as part of the route path. For `GET` (shortcut) requests, it must be supplied in the route path. |
| callback | ((string)) | If specified, a JSONP response will be sent (instead of JSON). This is the name of the client-side javascript function to call, passing results as the first (and only) argument 
e.g. `?callback=myJSONPHandlerFn` |

### Examples

#### Destroy (REST)

Delete Pinkie Pie.

#### Route

`DELETE /pony`

#### JSON Request Body

```
{
  "id": 4
} 
```

#### Expected Response

```
{
  "name": "Pinkie Pie",
  "hobby": "kickin",
  "id": 4,
  "createdAt": "2013-10-18T01:23:56.000Z",
  "updatedAt": "2013-11-26T22:55:19.951Z"
} 
```

#### Destroy (Shortcuts)

#### Route

`GET /pony/destroy/4`

#### Expected Response

Same as above.

<docmeta value="DestroyARecord867513" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="destroy" name="displayName" class="calibre17"></docmeta>

# Find

# Find Records

Returns a list of records from the model as a JSON array of objects.

```
GET /:model 
```

Results may be filtered, paginated, and sorted based on the blueprint configuration and/or parameters sent in the request.

If the action was triggered via a socket request, the requesting socket will be "subscribed" to all records returned. If any of the returned records are subsequently updated or deleted, a message will be sent to that socket's client informing them of the change. See the [docs for Model.subscribe()](https://github.com/balderdashy/sails-docs/blob/master/reference/ModelMethods.md#subscriberequestrecordscontexts) for details.

### Parameters

*All parameters are optional.*

| Parameter | Type | Details |
| --- | --- | --- |
| * | ((string)) | To filter results based on a particular attribute, specify a query parameter with the same name as the attribute defined on your model. 
For instance, if our `Purchase` model has an **amount** attribute, we could send `GET /purchase?amount=99.99` to return a list of $99.99 purchases. |
| where | ((string)) | Instead of filtering based on a specific attribute, you may instead choose to provide a `where` parameter with a Waterline WHERE criteria object, *encoded as a JSON string*. This allows you to take advantage of `contains`, `startsWith`, and other sub-attribute criteria modifiers for more powerful `find()` queries. 
e.g. `?where={"name":{"contains":"theodore"}}` |
| limit | ((number)) | The maximum number of records to send back (useful for pagination). Defaults to 30\. 
e.g. `?limit=100` |
| skip | ((number)) | The number of records to skip (useful for pagination). 
e.g. `?skip=30` |
| sort | ((string)) | The sort order. By default, returned records are sorted by primary key value in ascending order. 
e.g. `?sort=lastName%20ASC` |
| callback | ((number)) | If specified, a JSONP response will be sent (instead of JSON). This is the name of a client-side javascript function to call, to which results will be passed as the first (and only) argument 
e.g. ?callback=my_JSONP_data_receiver_fn |

### `find` Example

Find the 30 newest purchases in our database.

```
[
 {
   "amount": 49.99,
   "id": 1,
   "createdAt": "2013-10-18T01:22:56.000Z",
   "updatedAt": "2013-10-18T01:22:56.000Z"
 },
 {
   "amount": 99.99,
   "id": 47,
   "createdAt": "2013-10-14T01:22:00.000Z",
   "updatedAt": "2013-10-15T01:20:54.000Z"
 }
] 
```

**Using [jQuery](http://jquery.com/):**

```
$.get('/purchase?sort=createdAt DESC', function (purchases) {
  console.log(purchases);
}); 
```

**Using [Angular](https://angularjs.org/):**

```
$http.get('/purchase?sort=createdAt DESC')
.then(function (res) {
  var purchases = res.data;
  console.log(purchases);
}); 
```

**Using [sails.io.js](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js):**

```
io.socket.get('/purchase?sort=createdAt DESC', function (purchases) {
  console.log(purchases);
}); 
```

**Using [cURL](http://en.wikipedia.org/wiki/CURL):**

```
curl http://localhost:1337/purchase?sort=createdAt%20DESC 
```

### Notes

> *   The example above assumes "rest" blueprints are enabled, and that your project contains a `Purchase` model and an empty `PurchaseController`. You can quickly achieve this by running:
>     
>     
>     
>     ```
>     $ sails new foo
>     $ cd foo
>     $ sails generate api purchase 
>     ```

<docmeta value="Find290807" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="find where" name="displayName" class="calibre17"></docmeta>

# Find One

# Find One

Returns a single record from the model as a JSON Object.

```
GET /:model/:id 
```

The **findOne()** blueprint action returns a single record from the model (given by `:modelIdentity`) as a JSON object. The specified `id` is the [primary key](http://en.wikipedia.org/wiki/Unique_key) of the desired record.

If the action was triggered via a socket request, the requesting socket will be "subscribed" to the returned record. If the record is subsequently updated or deleted, a message will be sent to that socket's client informing them of the change. See the docs for .subscribe() for more info.

### Parameters

| Parameter | Type | Details |
| --- | --- | --- |
| id *(required)* | ((number)) *-or-*
((string)) | The desired record's primary key value 
e.g. `/product/7` |
| callback | ((string)) | If specified, a JSONP response will be sent (instead of JSON). This is the name of the client-side javascript function to call, passing results as the first (and only) argument 
e.g. `?callback=myJSONPHandlerFn` |

### Example

Find the purchase with ID #1, E.g. `http://localhost:1337/purchase/1`

#### Route

`GET /purchase/1`

#### Expected Response

```
 {
   "amount": 49.99,
   "id": 1,
   "createdAt": "2013-10-18T01:22:56.000Z",
   "updatedAt": "2013-10-18T01:22:56.000Z"
 } 
```

<docmeta value="FindOne259267" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="find one" name="displayName" class="calibre17"></docmeta>

# Populate

# Populate Where...

If the specified association is plural ("collection"), this action returns the list of associated records as a JSON array of objects. If the specified association is singular ("model"), this action returns the associated record as a JSON object.

```
GET /:model/:record/:association 
```

### Example

Populate the `cashier` who conducted purchase #47.

**Using [jQuery](http://jquery.com/):**

```
$.get('/purchase/47/cashier', function (purchase) {
  console.log(purchase);
}); 
```

**Using [Angular](https://angularjs.org/):**

```
$http.get('/purchase/47/cashier')
.then(function (purchase) {
  console.log(purchase);
}); 
```

**Using [sails.io.js](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js):**

```
io.socket.get('/purchase/47/cashier', function (purchase) {
  console.log(purchase);
}); 
```

**Using [cURL](http://en.wikipedia.org/wiki/CURL):**

```
curl http://localhost:1337/purchase/47/cashier 
```

Should return

```
{
  "amount": 99.99,
  "id": 47,
  "cashier": {
    "name": "Dolly",
    "id": 7,
    "createdAt": "2012-05-14T01:21:05.000Z",
    "updatedAt": "2013-01-15T01:18:40.000Z"
  },
  "createdAt": "2013-10-14T01:22:00.000Z",
  "updatedAt": "2013-10-15T01:20:54.000Z"
} 
```

### Notes

> *   The example above assumes "rest" blueprints are enabled, and that your project contains at least an empty 'Employee' model as well as a `Purchase` model with an association attribute: `cashier: {model: 'Employee'}`. You'll also need at least an empty `PurchaseController` and `EmployeeController`. You can quickly achieve this by running:
>     
>     
>     
>     ```
>     $ sails new foo
>     $ cd foo
>     $ sails generate api purchase
>     $ sails generate api employee 
>     ```
>     
>     
> 
> ...then editing `api/models/Purchase.js`.

<docmeta value="Populate838372" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="populate where" name="displayName" class="calibre17"></docmeta>

# Remove

# Remove from Collection

Removes an association between two records.

```
DELETE /:model/:record/:association/:record_to_remove 
```

This action removes a reference to some other record (the "foreign" record) from a collection attribute of this record (the "primary" record).

*   If the foreign record does not exist, it is created first.
*   If the collection doesn't contain a reference to the foreign record, this action will be ignored.
*   If the association is 2-way (i.e. reflexive, with "via" on both sides) the association on the foreign record will also be updated.

### Example

Remove Dolly (employee #7) from the `employeesOfTheMonth` list of store #16.

**Using [jQuery](http://jquery.com/):**

```
$.delete('/store/16/employeesOfTheMonth/7', function (purchases) {
  console.log(purchases);
}); 
```

**Using [Angular](https://angularjs.org/):**

```
$http.delete('/store/16/employeesOfTheMonth/7')
.then(function (purchases) {
  console.log(purchases);
}); 
```

**Using [sails.io.js](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js):**

```
io.socket.delete('/store/16/employeesOfTheMonth/7', function (purchases) {
  console.log(purchases);
}); 
```

**Using [cURL](http://en.wikipedia.org/wiki/CURL):**

```
curl http://localhost:1337/store/16/employeesOfTheMonth/7 -X "DELETE" 
```

Should return store #16, the primary record:

```
{
  "employeesOfTheMonth": [],
  "name": "Dolly",
  "createdAt": "2014-08-03T01:16:35.440Z",
  "updatedAt": "2014-08-03T01:51:41.567Z",
  "id": 16
} 
```

### Notes

> *   This action is for dealing with *plural* ("collection") associations. If you want to set or unset a *singular* ("model") association, just use [update](http://sailsjs.org/#/documentation/reference/blueprint-api/Update.html).
> *   The example above assumes "rest" blueprints are enabled, and that your project contains at least an empty 'Employee' model as well as a `Store` model with association: `employeesOfTheMonth: {collection: 'Employee'}`. You'll also need at least an empty `PurchaseController` and `EmployeeController`. You can quickly achieve this by running:
>     
>     
>     
>     ```
>     $ sails new foo
>     $ cd foo
>     $ sails generate api purchase
>     $ sails generate api employee 
>     ```
>     
>     
> 
> ...then editing `api/models/Store.js`.

<docmeta value="Remove2294521" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="remove from" name="displayName" class="calibre17"></docmeta>

# Update

# Update a Record

### `PUT /:model/:record`

Update an existing record. Attributes to change should be sent in the HTTP body as form-encoded values or JSON.

### Description

Updates the model instance which matches the **id** parameter. Responds with a JSON object representing the newly updated instance. If a validation error occurred, a JSON response with the invalid attributes and a `400` status code will be returned instead. If no model instance exists matching the specified **id**, a `404` is returned.

### Parameters

| Parameter | Type | Details |
| --- | --- | --- |
| id *(required)* | ((number)) *-or-*
((string)) | The primary key value of the record to update. 
e.g. `PUT /product/5` |
| * | ((string)) ((number))
((object))
((array)) | For `POST` (RESTful) requests, pass in body parameters with the same name as the attributes defined on your model to set those values on the desired record. For `GET` (shortcut) requests, add the parameters to the query string. |
| callback | ((string)) | If specified, a JSONP response will be sent (instead of JSON). This is the name of the client-side javascript function to call, passing results as the first (and only) argument 
e.g. `?callback=myJSONPHandlerFn` |

### Examples

### Update Record (REST)

Change AppleJack's hobby to "kickin".

#### Route

`PUT /pony/47`

#### JSON Request Body

```
{
  "hobby": "kickin"
} 
```

### Expected Response

```
{
  "name": "AppleJack",
  "hobby": "kickin",
  "id": 47,
  "createdAt": "2013-10-18T01:23:56.000Z",
  "updatedAt": "2013-11-26T22:55:19.951Z"
} 
```

### Update Record (Shortcuts)

`GET /pony/update/47?hobby=kickin`

#### Expected Response

Same as above.

### Add association between two existing records (REST)

Give Pinkie Pie the pre-existing pet named "Bubbles" who has ID 15.

#### Route

`POST /pony/4/pets`

#### JSON Request Body

```
{
  "id": 15
} 
```

#### Expected Response

```
{
  "name": "Pinkie Pie",
  "hobby": "kickin",
  "id": 4,
  "pets": [{
      "name": "Gummy",
      "species": "crocodile"
      "id": 10,
      "createdAt": "2014-02-13T00:06:50.603Z",
      "updatedAt": "2014-02-13T00:06:50.603Z"
    },{
      "name": "Bubbles",
      "species": "wiggleworm"
      "id": 15,
      "createdAt": "2014-02-13T00:06:50.603Z",
      "updatedAt": "2014-02-13T00:06:50.603Z"
    }],
  "createdAt": "2013-10-18T01:23:56.000Z",
  "updatedAt": "2013-11-26T22:55:19.951Z"
} 
```

### Add association between two existing records (Shortcuts)

`GET /pony/4/pets/add/15`

### Remove Association (Many-To-Many) (REST)

Remove Pinkie Pie's pet, "Gummy" (ID 12)

#### Route

`DELETE /pony/4/pets`

#### JSON Request Body

```
{
  "id": 12
} 
```

#### Expected Response

```
 {
  "name": "Pinkie Pie",
  "hobby": "ice skating",
  "pets": [{
      "name": "Bubbles",
      "species": "crackhead"
      "id": 15,
      "createdAt": "2014-02-13T00:06:50.603Z",
      "updatedAt": "2014-02-13T00:06:50.603Z"
    }],
  "id": 4,
  "createdAt": "2013-10-18T01:22:56.000Z",
  "updatedAt": "2013-11-26T22:54:19.951Z"
} 
```

#### Remove Association (Many-To-Many) (Shortcuts)

#### Route

`GET /pony/4/pets/remove/12`

#### Expected Response

Same as above.

<docmeta value="UpdateARecord421031" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="update" name="displayName" class="calibre17"></docmeta>

# Cli

# Command Line Interface (CLI)

### Overview

Sails comes with a convenient command line tool to quickly get your app scaffolded and running.

<docmeta value="cli83196" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Command Line Interface" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# Sailsconsole

# sails console

Quietly lift your sails app (i.e. with logging silenced), and enter the [node REPL](http://nodejs.org/api/repl.html). This means you can access and use all of your models, services, configuration, and much more. Useful for trying out Waterline queries, quickly managing your data, and checking out your project's runtime configuration.

### Example

```
$ sails console

info: Starting app in interactive mode...

info: Welcome to the Sails console.
info: ( to exit, type <CTRL>+<C> )

sails> 
```

> Note that `sails console` still lifts the server, so your routes will be accessible via HTTP and sockets (e.g. in a browser.)

### Global variables in sails console

Sails exposes the same [global variables](http://beta.sailsjs.org/#/documentation/reference/Globals) in the console as it does in your app code. This is particularly useful in the REPL. By default, you have access to the `sails` app instance, your models, and your services, as well as Lo-Dash (`sails.util._`) and async (`async`).

> **Warning**
> 
> Be careful when using `_` as a variable name in the Node REPL- and when possible, don't. (It doesn't work quite like you'd expect.)
> 
> Instead, use lodash as `sails.util._`, e.g.:
> 
> ```
> sails> sails.util._.keys(sails.config) 
> ```
> 
> Or alternatively, build yourself a local variable to use for familiarity:
> 
> ```
> sails> var lodash = _; 
> ```
> 
> Then you can do:
> 
> ```
> sails> lodash.keys(sails.config); 
> ```

### More Examples

#### Waterline

The format `Model.action(query).exec(console.log)` console.log is good for seeing the results.

```
sails> User.create({name: 'Brian', password: 'sailsRules'}).exec(console.log)
undefined
sails> null { name: 'Brian',
  password: 'sailsRules',
  createdAt: "2014-08-07T04:29:21.447Z",
  updatedAt: "2014-08-07T04:29:21.447Z",
  id: 1 } 
```

Pretty cool, it inserts it into the database. However, you might be noticing the undefined and null. Don't worry about those. Remember that the .exec() returns error and data for values. So doing `.exec(console.log)` is the same as doing .exec(console.log(err, data))` The second method will remove the undefined message, but add null on a new line. It's up to you if you want to type more.

#### Exposing Sails

In sails console, type in `sails` to view a list of sails properties. You can use this to learn more about sails, override properties, or check to see if you disabled globals.

```
sails> sails
  |>   [a lifted Sails app on port 1337]
\___/  For help, see: http://links.sailsjs.org/docs

Tip: Use `sails.config` to access your app's runtime configuration.

1 Models:
User

1 Controllers:
UserController

20 Hooks:
moduleloader,logger,request,orm,views,blueprints,responses,controllers,sockets,p
ubsub,policies,services,csrf,cors,i18n,userconfig,session,grunt,http,userhooks

sails> 
```

<docmeta value="sailsconsole198558" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails console" name="displayName" class="calibre17"></docmeta>

# Sailsdebug

# sails debug

Attach the node debugger and lift the sails app; similar to running `node --debug app.js`. Takes the same options as `sails lift`. You can then use [node-inspector](https://github.com/node-inspector/node-inspector) to debug your app as it runs.

### Example

```
$ sails debug

info: Running node-inspector on this app...
info: If you don't know what to do next, type `help`
info: Or check out the docs:
info: http://nodejs.org/api/debugger.html

info: ( to exit, type <CTRL>+<C> )

debugger listening on port 5858 
```

> To use the standard (command-line) node debugger with sails, you can always just run `node debug app.js`.

<docmeta value="sailsdebug521538" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails debug" name="displayName" class="calibre17"></docmeta>

# Sailsgenerate

# sails generate

Sails ships with several *generators* to help you scaffold new projects. You can also [create your own generators](http://beta.sailsjs.org/#/documentation/concepts/extending-sails/Generators/customGenerators.html) to handle frequent tasks, or extend functionality (for example, by creating a generator that outputs view files for your [favorite templating language](https://github.com/balderdashy/sails-generate-views-jade)).

The following generators are bundled with Sails:

#### `sails generate new <appName>`

Create a new Sails project in a folder called **appName**. See [`sails new`](http://beta.sailsjs.org/#/documentation/reference/cli/sailsnew.html) for usage options.

#### `sails generate api <foo>`

Generate **api/models/Foo.js** and **api/controllers/FooController.js**

#### `sails generate model <foo> [attribute1:type1, attribute2:type2 ... ]`

Generate **api/models/Foo.js**, optionally include attributes with the specified types.

#### `sails generate controller <foo> [action1, action2, ...]`

Generate **api/controllers/FooController.js**, optionally include actions with the specified names.

#### `sails generate adapter <foo>`

Generate a **api/adapters/foo** folder containing the files necessary for building a new adapter.

#### `sails generate generator <foo>`

Generate a **foo** folder containing the files necessary for building a new generator.

<docmeta value="sailsgenerate197041" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails generate" name="displayName" class="calibre17"></docmeta>

# Sailslift

# sails lift

Run the Sails app in the current dir (if `node_modules/sails` exists, it will be used instead of the globally installed Sails)

##### Options:

*   `--dev` - in development environment (the default). In the development environment Sails use *grunt-watch* to keep a eye on your files in `/assets`. If you change something (for example in one of our css-files) and reload your browser Sails will automatically show your changes. Also you views won't be cached so you can change your view-files without restarting Sails like the assets.
*   `--prod` - in production environment
*   `--port <portNum>` - on the port specified by `portNum` instead of the default (1337)
*   `--verbose` - with verbose logging enabled
*   `--silly` - with insane logging enabled

### Example

```
$ sails lift

info: Starting app...

info: 
info: 
info:    Sails              <|
info:    v0.11.3             |\
info:                       /|.\
info:                      / || \
info:                    ,'  |'  \
info:                 .-'.-==|/_--'
info:                 `--'-------' 
info:    __---___--___---___--___---___--___
info:  ____---___--___---___--___---___--___-__
info: 
info: Server lifted in `/Users/mikermcneil/code/sandbox/second`
info: To see your app, visit http://localhost:1337
info: To shut down Sails, press <CTRL> + C at any time.

debug: --------------------------------------------------------
debug: :: Sat Apr 05 2014 17:03:39 GMT-0500 (CDT)

debug: Environment : development
debug: Port        : 1337
debug: -------------------------------------------------------- 
```

<docmeta value="sailslift482554" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails lift" name="displayName" class="calibre17"></docmeta>

# Sailsnew

# sails new

`sails new <appName>` creates a new Sails project in a folder called **appName**.

##### Options:

*   `--no-linker` Disable automatic asset linking in your view and static HTML files (the relevant grunt tasks will not be created)
*   `--no-frontend` Disable the generation of the `assets` folder and files. Views will be created with hardcopied linked resources off of sailsjs.org.
*   `--template=[template language]` Use a different template language than the default (e.g. `jade`). Requires that a views generator for that language (e.g. `sails-generate-views-jade`) be installed in your global node path (e.g. `~/node_modules/` works).

> `sails new` is really just a special [generator](http://beta.sailsjs.org/#/documentation/concepts/extending-sails/Generators) which runs [`sails-generate-new`](http://github.com/balderdashy/sails-generate-new). In other words, running `sails new foo` is an alias for running `sails generate new foo`, and like any Sails generator, the actual generator module which gets run can be overridden in your global `~/.sailsrc` file.

<docmeta value="sailsnew912235" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails new" name="displayName" class="calibre17"></docmeta>

# Sailsversion

# sails version

Get the current globally installed Sails version.

### Example

```
$ sails version
0.10.0-rc5 
```

<docmeta value="sailsversion892721" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails version" name="displayName" class="calibre17"></docmeta>

# Req

# Request (`req`)

Sails is built on [Express](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md), and uses [Node's HTTP server](http://nodejs.org/api/http.html) conventions. Because of this, you can access all of the Node and Express methods and properties on the `req` object whereever it is accessible (i.e. in your controllers, policies, and custom responses.)

A nice side effect of this compatibility is that, in many cases, you can paste existing Node.js code into a Sails app and it will work. And since Sails implements a transport-agnostic request interpreter, the code in your Sails app is WebSocket-compatible as well.

Sails adds a few methods and properties of its own to the `req` object, like [`req.wantsJSON`](http://beta.sailsjs.org/#/documentation/reference/req/req.wantsJSON.html) and [`req.params.all()`](http://beta.sailsjs.org/#/documentation/reference/req/req.allParams.html). These features are syntactic sugar on top of the underlying implementation, and also support both HTTP and WebSockets.

### Protocol Support

The chart below describes support for the methods and properties on the Sails Request object (`req`) across multiple transports:

|  | HTTP | WebSockets |
| --- | --- | --- |
| req.file() | :white_check_mark: | :white_large_square: |
| req.param() | :white_check_mark: | :white_check_mark: |
| req.route | :white_check_mark: | :white_check_mark: |
| req.cookies | :white_check_mark: | :white_large_square: |
| req.signedCookies | :white_check_mark: | :white_large_square: |
| req.get() | :white_check_mark: | :white_large_square: |
| req.accepts() | :white_check_mark: | :white_large_square: |
| req.accepted | :white_check_mark: | :white_large_square: |
| req.is() | :white_check_mark: | :white_large_square: |
| req.ip | :white_check_mark: | :white_check_mark: |
| req.ips | :white_check_mark: | :white_large_square: |
| req.path | :white_check_mark: | :white_large_square: |
| req.host | :white_check_mark: | :white_large_square: |
| req.fresh | :white_check_mark: | :white_large_square: |
| req.stale | :white_check_mark: | :white_large_square: |
| req.xhr | :white_check_mark: | :white_large_square: |
| req.protocol | :white_check_mark: | :white_check_mark: |
| req.secure | :white_check_mark: | :white_large_square: |
| req.session | :white_check_mark: | :white_check_mark: |
| req.subdomains | :white_check_mark: | :white_large_square: |
| req.method | :white_check_mark: | :white_check_mark: |
| req.originalUrl | :white_check_mark: | :white_large_square: |
| req.acceptedLanguages | :white_check_mark: | :white_large_square: |
| req.acceptedCharsets | :white_check_mark: | :white_large_square: |
| req.acceptsCharset() | :white_check_mark: | :white_large_square: |
| req.acceptsLanguage() | :white_check_mark: | :white_large_square: |
| req.isSocket | :white_check_mark: | :white_check_mark: |
| req.params.all() | :white_check_mark: | :white_check_mark: |
| req.socket.id | :heavy_multiplication_x: | :white_check_mark: |
| req.socket.join | :heavy_multiplication_x: | :white_check_mark: |
| req.socket.leave | :heavy_multiplication_x: | :white_check_mark: |
| req.socket.broadcast | :heavy_multiplication_x: | :white_check_mark: |
| req.transport | :white_large_square: | :white_check_mark: |
| req.url | :white_check_mark: | :white_check_mark: |
| req.wantsJSON | :white_check_mark: | :white_check_mark: |

### Legend

*   :white_check_mark: - fully supported
*   :white_large_square: - feature not yet implemented
*   :heavy_multiplication_x: - unsupported due to protocol restrictions

<docmeta value="req35837" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Request (`req`)" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# req.accepted

# req.accepted

Contains an array of the "media types" this request (`req`) can accept (e.g. `text/html` or `application/json`), ordered from highest to lowest quality.

### Usage

```
req.accepted; 
```

### Example

```
req.accepted;

/*
  [ { value: 'application/json',
      quality: 1,
      type: 'application',
      subtype: 'json' },
  { value: 'text/html',
       quality: 0.5,
       type: 'text',
       subtype: 'html' } ]
*/ 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.

<docmeta value="reqaccepted334477" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.accepted" name="displayName" class="calibre17"></docmeta>

# req.acceptedCharsets

# req.acceptedCharsets

This property is an array that contains the acceptable charsets specified by the user agent in the request.

### Usage

```
req.acceptedCharsets; 
```

### Details

Useful for advanced content negotiation where a client may or may not support certain character sets, such as unicode (utf-8.) This returns all of the "acceptable" charsets specified in this request's `Accept-Charset` header (see [RFC-2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.2).)

### Example

```
req.acceptedCharsets;
// -> ['utf-8', 'utf-16'] 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.

<docmeta value="reqacceptedCharsets230309" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.acceptedCharsets" name="displayName" class="calibre17"></docmeta>

# req.acceptedLanguages

# req.acceptedLanguages

An array containing the "acceptable" response languages specified by the user agent in the "[Accept-Language](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4)" header of this request (`req`).

### Usage

```
req.acceptedLanguages; 
```

### Details

`req.acceptedLanguages` contains all the languages specified by the request's `Accept-Language` header (see [RFC-2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4).)

This method is used by Sails internally for its implementation of internationalization and localization. The [i18n](http://beta.sailsjs.org/#/documentation/concepts/Internationalization) hook automatically serves different content to different locales, based on the request.

### Example

```
req.acceptedLanguages;
// -> ['en-US', 'en'] 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.
> *   Browsers send the "Accept-Language" header automatically based on the user's language settings.
> *   You can expect the "Accept-Language" header to exist in most requests which originate from web browsers.

<docmeta value="reqacceptedLanguages311952" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.acceptedLanguages" name="displayName" class="calibre17"></docmeta>

# req.accepts

# req.accepts()

Checks whether this request's stated list of "accepted" [media types](http://www.iana.org/assignments/media-types/media-types.xhtml) includes the specified `type`. Returns true or false.

### Usage

```
req.accepts(type); 
```

### Example

```
req.accepts('application/json');
// -> true
req.accepts('json');
// -> true 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.

<docmeta value="reqaccepts89101" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.accepts()" name="displayName" class="calibre17"></docmeta>

# req.acceptsCharset

# req.acceptsCharset()

Returns whether this request (`req`) is able to handle a specified `characterSet`.

### Usage

```
req.acceptsCharset(characterSet); 
```

### Details

Useful for advanced content negotiation where a client may or may not support certain character sets, such as unicode (utf-8.) This method determines whether or not a request has specified the given `characterSet` as "acceptable" its `Accept-Charset` header (see [RFC-2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.2).)

### Example

If a request is sent with a `"Accept-Charset: utf-8"` header:

```
req.acceptsCharset('utf-8');
// -> true 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.

<docmeta value="reqacceptsCharset303007" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.acceptsCharset()" name="displayName" class="calibre17"></docmeta>

# req.acceptsLanguage

# req.acceptsLanguage()

Returns whether this request (`req`) considers a certain `language` "acceptable".

### Usage

```
req.acceptsLanguage(language); 
```

### Details

`req.acceptsLanguage()` returns true if a request has specified the given `language` as "acceptable" its `Accept-Language` header (see [RFC-2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4).)

This method is used by Sails internally for its implementation of internationalization and localization. The [i18n](http://beta.sailsjs.org/#/documentation/concepts/Internationalization) hook automatically serves different content to different locales, based on the request.

### Example

If a request is sent with a `"Accept-Charset: utf-8"` header:

```
req.acceptsCharset('utf-8');
// -> true 
```

### Notes

> *   See the [`accepts` module](https://github.com/expressjs/accepts) for the finer details of the header parsing algorithm used in Sails/Express/Koa/Connect.
> *   Browsers send the "Accept-Language" header automatically based on the user's language settings.
> *   You can expect the "Accept-Language" header to exist in most requests which originate from web browsers.

<docmeta value="reqacceptsLanguage170988" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.acceptsLanguage()" name="displayName" class="calibre17"></docmeta>

# req.allParams

# req.allParams()

Returns the value of *all* parameters sent in the request, merged together into a single object. Includes parameters parsed from the url path, the query string, and the request body. See `req.param()` for details.

### Usage

```
req.allParams(); 
```

### Example

Update the product with the specified `sku`, setting new values using the parameters which were passed in:

```
var values = req.allParams();

// Don't allow `price` or `isAvailable` to be edited.
delete values.price;
delete values.isAvailable;

// At this point, `values` might look something like this:
// values ==> { displayName: 'Bubble Trouble Bubble Bath' }

Product.update({sku: sku})
.set(values)
.then(function (newProduct) {
  // ...
}); 
```

### Notes

> *   This method can also be called as `req.params.all()` - they are synonyms.

<docmeta value="reqallParams817828" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.allParams()" name="displayName" class="calibre17"></docmeta>

# req.body

# req.body

An object containing text parameters from the parsed request body, defaulting to `{}`.

By default, the request body can be url-encoded or stringified as JSON. Support for other formats, such as serialized XML, is possible using the [middleware](http://beta.sailsjs.org/#/documentation/concepts/Middleware) configuration.

### Usage

```
req.body; 
```

### Notes

> *   If a request contains one or more file uploads, only the text parameters sent ***before*** the first file parameter will be available in `req.body`.

<docmeta value="reqbody1481" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.body" name="displayName" class="calibre17"></docmeta>

# req.cookies

# req.cookies

An object containing all of the [**unsigned cookies**](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) from this request (`req`).

### Usage

```
req.cookies; 
```

### Example

Assuming the request contained a cookie named "chocolatechip" with value "Yummy:

```
req.cookies.chocolatechip;
// "Yummy" 
```

<docmeta value="reqcookies576909" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.cookies" name="displayName" class="calibre17"></docmeta>

# req.file

# req.file()

Returns a [readable Node stream](http://nodejs.org/api/stream.html#stream_class_stream_readable) of incoming multipart file uploads (an [`Upstream`](https://github.com/balderdashy/skipper/blob/master/lib/Upstream.js)) from the specified `field`.

### Usage

```
req.file(field); 
```

### Details

`req.file()` comes from [Skipper](https://github.com/balderdashy/skipper), an opinionated variant of the original Connect body parser that allows you to take advantage of high-performance, streaming file uploads without any dramatic changes in your application logic.

This is a great simplification, but comes with a minor caveat: **Text parameters must be included before files in the request body.** Typically, these text parameters contain string metadata which provides additional information about the file upload.

Multipart requests to Sails should send all of their **text parameters**. before sending *any* **file parameters**. For instance, if you're building a web frontend that communicates with Sails, you should include text parameters *first* in any form upload or AJAX file upload requests. The term "text parameters" refers to the metadata parameters you might send along with the file(s) providing some additional information about this upload.

### How It Works

Skipper treats *all* file uploads as streams. This allows users to upload monolithic files with minimal performance impact and no disk footprint, all the while protecting your app against nasty denial-of-service attacks involving tmp files.

When a multipart request hits your server, instead of writing temporary files to disk, Skipper buffers the request just long enough to run your app code, giving you an opportunity to "plug in" to a compatible blob receiver. If you don't "plug in" the data from a particular field, the Upstream hits its "high water mark", the buffer is flushed, and subsequent incoming bytes on that field are ignored.

### Example

In a controller action or policy:

```
var SomeReceiver = require('../services/SomeReceiver');

req.file('avatar').upload( SomeReceiver(), function (err, files) {
    if (err) return res.serverError(err);
    return res.json({
      message: files.length + ' file(s) uploaded successfully!',
      files: files
    });
  });
}); 
```

### Notes

> *   Remember that the client request's **text parameters must be sent first**, before the file parameters.
> *   `req.file()` supports multiple files sent over the same field, but it's important to realize that, as a consequence, the Upstream it returns is actually a stream (buffered event emitter) of potential binary streams (files).
> *   If you prefer to work directly with the Upstream as a stream of streams, you can omit the `.upload()` method and bind "finish" and "error" events (or use `.pipe()`) instead. [Under the covers](https://github.com/balderdashy/skipper/blob/master/lib/Upstream.js#L126), all `.upload()` is doing is piping the **Upstream** into the specified receiver instance, then running the specified callback when the Upstream emits either a `finish` or `error` event.

<docmeta value="reqfile784692" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.file()" name="displayName" class="calibre17"></docmeta>

# req.fresh

# req.fresh

A flag indicating the user-agent sending this request (`req`) wants "fresh" data (as indicated by the "[if-none-match](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.26)", "[cache-control](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)", and/or "[if-modified-since](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.25)" request headers.)

If the request wants "fresh" data, usually you'll want to `.find()` fresh data from your models and send it back to the client.

### Usage

```
req.fresh; 
```

### Example

```
if (req.fresh) {
  // The user-agent is asking for a more up-to-date version of the requested resource.
  // Let's hit the database to get some stuff and send it back.
} 
```

### Notes

> *   See the [`node-fresh`](https://github.com/visionmedia/node-fresh) module for details specific to the implementation in Sails/Express/Koa/Connect.

<docmeta value="reqfresh718346" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.fresh" name="displayName" class="calibre17"></docmeta>

# req.get

# req.get()

Returns the value of the specified `header` field in this request (`req`). Note that header names are case-*insensitive*.

### Usage

```
req.get(header); 
```

### Example

Assuming `req` contains a header named 'myField' with value 'cat':

```
req.get('myField');
// -> cat 
```

### Notes

> *   The `header` argument is case-insensitive.
> *   The `header` argument treats both "referrer" and "referer" as synonyms, because sp3ll1n6.

<docmeta value="reqget839626" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.get()" name="displayName" class="calibre17"></docmeta>

# req.host

# req.host

The hostname of this request, without the port number, as specified by its "Host" header.

### Usage

```
req.host; 
```

### Example

If this request's "Host" header was: "ww3.staging.ibm.com:1492":

```
req.host;
// -> "ww3.staging.ibm.com" 
```

<docmeta value="reqhost35719" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.host" name="displayName" class="calibre17"></docmeta>

# req.ip

# req.ip

### Purpose

The IP address of the client who sent this request (`req`).

If the `trust proxy` option is disabled, this is the "remote address". Otherwise, if `trust proxy` is enabled, this is the "upstream address".

### Usage

```
req.ip; 
```

### Example

```
req.ip;
// -> "127.0.0.1" 
```

<docmeta value="reqip681943" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.ip" name="displayName" class="calibre17"></docmeta>

# req.ips

# req.ips

If "trust proxy" is enabled, this variable contains the IP addresses in this request's "X-Forwarded-For" header as an array of the IP address strings. Otherwise an empty array is returned.

### Usage

```
req.ips; 
```

### Example

If a request contains a header: "X-Forwarded-For: client, proxy1, proxy2":

```
req.ips;
// -> ["client", "proxy1", "proxy2"]`

// ("proxy2" is the furthest "down-stream" IP address) 
```

<docmeta value="reqips78262" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.ips" name="displayName" class="calibre17"></docmeta>

# req.is

# req.is()

Returns true if this request's declared "Content-Type" matches the specified media/mime `type`.

Specifically, this method matches the given `type` against this request's "Content-Type" header.

### Usage

```
req.is(type); 
```

### Example

Assuming the request contains a "Content-Type" header, "text/html; charset=utf-8":

```
req.is('html');
// -> true
req.is('text/html');
// -> true
req.is('text/*');
// -> true 
```

<docmeta value="reqis371514" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.is()" name="displayName" class="calibre17"></docmeta>

# req.isSocket

# req.isSocket

A flag indicating whether or not this request (`req`) originated from a Socket.io connection.

### Usage

```
req.isSocket; 
```

### Example

```
if (req.isSocket){
  // You're a socket.  Do cool socket stuff.
}
else {
  // Just another HTTP request.
} 
```

### Notes

> *   Useful for allowing HTTP requests to skip calls to pubsub or WebSocket-centric methods like `subscribe()` or `watch()` that depend on an actual Socket.io request. This allows you to reuse backend code, using it for both WebSocket and HTTP clients.
> *   As you might expect, `req.isSocket` doesn't need to be checked before running methods which **publish to other** connected sockets. Those methods don't depend on the request, so they work either way.

<docmeta value="reqisSocket87074" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.isSocket" name="displayName" class="calibre17"></docmeta>

# req.method

# req.method

The request method (aka "verb".)

### Usage

```
req.method; 
```

### Example

If a client sends a POST request to `/product`:

```
req.method;
// -> "POST" 
```

### Notes

> *   All requests to a Sails server have a "method", even via WebSockets (this is thanks to the request interpreter)

<docmeta value="reqmethod305728" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.method" name="displayName" class="calibre17"></docmeta>

# req.param

# req.param()

Returns the value of the parameter with the specified name.

### Usage

```
req.param(name); 
```

### Details

`req.param()` searches the url path, query string, and body of the request for the specified parameter. If no parameter value exists anywhere in the request with the given `name`, it returns `undefined`.

*   url path parameters ([`req.params`](http://beta.sailsjs.org/#/documentation/reference/req/req.params.html))
    *   e.g. a request "/foo/4" to route `/foo/:id` has url path params `{ id: 4 }`
*   query string parameters ([`req.query`](http://beta.sailsjs.org/#/documentation/reference/req/req.query.html))
    *   e.g. a request "/foo?email=5" has query params `{ email: 5 }`
*   body parameters ([`req.body`](http://beta.sailsjs.org/#/documentation/reference/req/req.body.html))
    *   e.g. a request with a parseable body (e.g. JSON, url-encoded, or XML) has body parameters equal to its parsed value

### Example

Consider a route (`POST /product/:sku`) which points to a blueprint, controller, or policy with the following code:

```
req.param('sku');
// -> 123 
```

We can get the expected result by sending the `sku` parameter any of the following ways:

*   `POST /product/123`
*   `POST /product?sku=123`
*   `POST /product`
    *   with a JSON request body: `{ "sku": 123 }`

### Notes

> *   If you'd like to get ALL parameters from ALL sources (including the URL path, query string, and parsed request body) you can use [`req.allParams()`](http://beta.sailsjs.org/#/documentation/reference/req/req.allParams.html).

<docmeta value="reqparam149618" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.param()" name="displayName" class="calibre17"></docmeta>

# req.params

# req.params

An object containing parameter values parsed from the URL path.

For example if you have the route `/user/:name`, then the "name" from the URL path wil be available as `req.params.name`. This object defaults to `{}`.

### Usage

```
req.params; 
```

### Notes

> *   When a route address is defined using a regular expression, each capture group match from the regex is available as `req.params[0]`, `req.params[1]`, etc.This strategy is also applied to unnamed wild-card matches in string routes such as `/file/*`.

<docmeta value="reqparams977271" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.params" name="displayName" class="calibre17"></docmeta>

# req.path

# req.path

The URL pathname from the [request URL string](http://nodejs.org/api/http.html#http_message_url) of the current request (`req`). Note that this is the part of the URL after and including the leading slash (e.g. `/foo/bar`), but without the query string (e.g. `?name=foo`) or fragment (e.g. `#foobar`.)

### Usage

```
req.path; 
```

### Example

Assuming a client sends the following request:

> [`localhost:1337/donor/37?name=foo#foobar`](http://localhost:1337/donor/37?name=foo#foobar)

`req.path` will be defined as follows:

```
req.path;
// -> "/donor/37" 
```

<docmeta value="reqpath216836" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.path" name="displayName" class="calibre17"></docmeta>

# req.protocol

# req.protocol

The protocol used to send this request (`req`).

### Usage

```
req.protocol; 
```

### Example

```
switch (req.protocol) {
  case 'http':
    // this is an HTTP request
    break;
  case 'https':
    // this is a secure HTTPS request
    break;
} 
```

<docmeta value="reqprotocol732076" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.protocol" name="displayName" class="calibre17"></docmeta>

# req.query

# req.query

An object containing the parsed query-string, defaulting to `{}`.

### Usage

```
req.query; 
```

### Example

If the request is `GET /search?q=mudslide`:

```
req.query.q
// -> "mudslide" 
```

<docmeta value="reqquery553014" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.query" name="displayName" class="calibre17"></docmeta>

# req.secure

# req.secure

Indicates whether or not the request was sent over a secure [TLS](http://en.wikipedia.org/wiki/Transport_Layer_Security) connection (i.e. `https://` or `wss://`).

### Usage

```
req.secure; 
```

<docmeta value="reqsecure698791" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.secure" name="displayName" class="calibre17"></docmeta>

# req.signedCookies

# req.signedCookies

### Purpose

An object containing all of the [**signed cookies**](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) from this request (`req`).

### Usage

```
req.signedCookies; 
```

### Example

Assuming the request contained a signed cookie named "chocolatechip" with value "Yummy:

```
req.cookies.chocolatechip;
// "Yummy" 
```

<docmeta value="reqsignedCookies113713" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.signedCookies" name="displayName" class="calibre17"></docmeta>

# req.socket

# req.socket

If the current Request (`req`) originated from a connected Socket.io client, `req.socket` refers to the raw Socket.io socket instance.

### Usage

```
req.socket; 
```

### Details

> **Warning:**
> 
> `req.socket` may be deprecated in a future release of Sails. You should use the `sails.sockets.*` methods instead.

If the current request (`req`) did NOT originate from a Socket.io client, `req.socket` does not have the same meaning. In the most common scenario, HTTP requests, `req.socket` actually *does exist*, but it refers instead to the underlying TCP socket. Before using `req.socket`, you should check the [`req.isSocket`](http://beta.sailsjs.org/#/documentation/reference/req/req.isSocket.html) flag to ensure the request arrived via a connected Socket.io client.

`req.socket.id` is a unique identifier representing the current socket. This is generated by the Socket.io server when a client first connects, and is a valid unique identifier until the socket is disconnected (e.g. if the client is a web browser, until the user closes her browser tab.)

Sails also provides direct, low-level access to all of the other methods and properties from a Socket.io `Socket`, including `req.socket`, including `req.socket.join`, `req.socket.leave`, `req.socket.broadcast`, and more. See the relevant docs in the [Socket.io wiki](https://github.com/LearnBoost/socket.io/wiki/Rooms) for more information.

### Example

```
if (req.isSocket) {
  // Low-level Socket.io methods and properties accessible on req.socket.
  // ...
}
else {
  // This is not a request from a Socket.io client, so req.socket
  // may or may not exist.  If this is an HTTP request, req.socket is actually
  // the underlying TCP socket.
  // ...
} 
```

<docmeta value="reqsocket572002" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.socket" name="displayName" class="calibre17"></docmeta>

# req.subdomains

# req.subdomains

An array of all the subdomains in this request's URL.

### Usage

```
req.subdomains; 
```

### Example

If the requested URL was "[`ww3.staging.ibm.com`](https://ww3.staging.ibm.com)":

```
req.subdomains;
// -> ['ww3', 'staging'] 
```

<docmeta value="reqsubdomains686204" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.subdomains" name="displayName" class="calibre17"></docmeta>

# req.url

# req.url

Like [`req.path`](http://sailsjs.org/#/documentation/reference/req/req.path.html), but also includes the query string suffix.

```
req.url;

// => "/search?q=worlds%20largest%20dogs" 
```

### Notes

> *   It is worth mentioning that the URL fragment/hash (e.g. "#some/clientside/route") part of the url is [not available on the server](https://github.com/strongloop/express/issues/1083#issuecomment-5179035). This is an [open issue with the current HTTP specification](http://stackoverflow.com/a/2305927/486547). So if you write an action to redirect from one subdomain to another, for instance, you won't be able to peek at the URL fragment in that action.
> *   However, if you respond with a 302 redirect (i.e. `res.redirect()`) the user agent on the other end will preserve the URL fragment/hash and tack it on to the end of the new redirected URL. In many cases, this is exactly what you want!

<docmeta value="requrl810500" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.url" name="displayName" class="calibre17"></docmeta>

# req.wantsJSON

# req.wantsJSON

A flag indicating whether the requesting client would prefer a JSON response (as opposed to some other format, like XML or HTML.)

`req.wantsJSON` is used by all of the built-in custom responses in Sails.

### Usage

```
req.wantsJSON; 
```

### Details

The intended purpose of `req.wantsJSON` is to provide a clean, reusable indication of whether the server should respond with JSON, or send back something else (like an HTML page or a 302 redirect.) It is not the right answer for *every* content negotiation problem, but it is a simple, go-to solution for most use cases.

For instance, for requests typed into the URL bar, all major browsers set an "Accept: text/plain;" request header. In that case, `req.wantsJSON` is false. But for many other cases, the distinction is not quite as clear. In those scenarios, Sails uses heuristics to determine the best value for `req.wantsJSON`.

Technically, `req.wantsJSON` inspects the request's `"Content-type"`, `"Accepts"`, and `"X-Requested-With"` headers to make an inference as to whether the request is expecting a JSON response. If the request did not provide enough information to know for sure, Sails errs on the side of JSON (i.e. `req.wantsJSON` will be set to `true`.)

This all makes your app more future-proof and less brittle: as best-practices for content negotiation change over time (e.g. a new type of consumer device or enterprise user-agent introduces a new header) Sails can patch `req.wantsJSON` at the framework level and modify the heuristics accordingly. Not to mention that it reduces code duplication and saves you the annoyance of manually inspecting headers in each of your routes.

### Example

```
if (req.wantsJSON) {
  return res.json(data);
}
else {
  return res.view(data);
} 
```

### Details

Here is the specific order in which `req.wantsJSON` inspects the request. **If any of the following match, subsequent checks are ignored.**

A request "wantsJSON" if:

*   if this looks like an AJAX request
*   if this is a virtual request from a socket
*   if this request DOESN'T explicitly want HTML
*   if this request has a "json" content-type AND ALSO has its "Accept" header set
*   if `req.options.wantsJSON` is truthy

### Notes

> *   Lower-level content negotiation is, of course, still possible using `req.is()`, `req.accepts()`, `req.xhr`, and `req.get()`.
> *   As of Sails v0.11, requests originating from a WebSocket client always "want JSON".

<docmeta value="reqwantsJSON30891" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.wantsJSON" name="displayName" class="calibre17"></docmeta>

# req.xhr

# req.xhr

A flag indicating whether the current request (`req`) appears to be an AJAX request (i.e. it was issued with its "X-Requested-With" header set to "XMLHttpRequest".)

### Usage

```
req.xhr; 
```

### Example

```
if (req.xhr) {
  // Yup, it's AJAX alright.
} 
```

### Notes

> *   Whenever possible, you should prefer the `req.wantsJSON` flag. Avoid writing custom content-negotiation negotiation logic into your app - it makes your code more brittle and more verbose.

<docmeta value="reqxhr450203" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="req.xhr" name="displayName" class="calibre17"></docmeta>

# Res

# Response (`res`)

### Overview

Sails is built on [Express](https://github.com/expressjs/), and uses [Node's HTTP server](http://nodejs.org/api/http.html#http_http_createserver_requestlistener) conventions. Because of this, you can access all of the Node and Express methods and properties on the `res` object whereever it is accessible (i.e. in your controllers, policies, and custom responses.)

A nice side effect of this compatibility is that, in many cases, you can paste existing Node.js code into a Sails app and it will work. And since Sails implements a transport-agnostic request interpreter, the code in your Sails app is WebSocket-compatible as well.

Sails adds a few methods of its own to the `res` object, like `res.view()`. These features are syntactic sugar on top of the underlying implementation, and also support both HTTP and WebSockets.

### Protocol Support

The chart below describes support for the methods and properties on the Sails Request object (`req`) across multiple transports:

The chart below describes support for the methods and properties on the Sails Response object (`res`) across multiple transports:

|  | HTTP | WebSockets |
| --- | --- | --- |
| res.status() | :white_check_mark: | :white_check_mark: |
| res.set() | :white_check_mark: | :white_large_square: |
| res.get() | :white_check_mark: | :white_large_square: |
| res.cookie() | :white_check_mark: | :white_large_square: |
| res.clearCookie() | :white_check_mark: | :white_large_square: |
| res.redirect() | :white_check_mark: | :white_check_mark: |
| res.location() | :white_check_mark: | :white_large_square: |
| res.charset | :white_check_mark: | :white_check_mark: |
| res.send() | :white_check_mark: | :white_check_mark: |
| res.json() | :white_check_mark: | :white_check_mark: |
| res.jsonp() | :white_check_mark: | :white_check_mark: |
| res.type() | :white_check_mark: | :white_large_square: |
| res.format() | :white_check_mark: | :white_large_square: |
| res.attachment() | :white_check_mark: | :white_large_square: |
| res.sendfile() | :white_check_mark: | :white_large_square: |
| res.download() | :white_check_mark: | :white_large_square: |
| res.links() | :white_check_mark: | :white_large_square: |
| res.locals | :white_check_mark: | :white_check_mark: |
| res.render() | :white_check_mark: | :white_large_square: |
| res.view() | :white_check_mark: | :white_large_square: |

### Legend

*   :white_check_mark: - fully supported
*   :white_large_square: - feature not yet implemented
*   :heavy_multiplication_x: - unsupported due to protocol restrictions

<docmeta value="res550242" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Response (`res`)" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# res.attachment

# res.attachment()

Sets the "Content-Disposition" header of the current response to "attachment". If a `filename` is given, then the "Content-Type" will be automatically set based on the extension of the file (e.g. `.jpg` or `.html`), and the "Content-Disposition" header will be set to "filename=`filename`".

### Usage

```
res.attachment([filename]); 
```

### Example

```
res.attachment();
// -> response header will contain:
//   Content-Disposition: attachment

res.attachment('path/to/logo.png');
// -> response header will contain:
//   Content-Disposition: attachment; filename="logo.png"
//   Content-Type: image/png 
```

<docmeta value="resattachment107506" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.attachment()" name="displayName" class="calibre17"></docmeta>

# res.badRequest

# res.badRequest()

This method is used to send a [400](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error) ("Bad Request") response back down to the client indicating that the request is invalid. This usually means it contained invalid parameters or headers, or tried to do something impossible based on your app logic.

### Usage

```
return res.badRequest(); 
```

*Or:*

*   `return res.badRequest(data);`
*   `return res.badRequest(data, pathToView);`

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

By default, it works as follows:

*   If the request "wants JSON" (e.g. the request originated from AJAX, WebSockets, or a REST client like cURL), Sails will send the provided error `data` as JSON. If no `data` is provided a default response body will be sent (the string `"Bad Request"`).
*   If the request *does not* "want JSON" (e.g. a URL typed into a web browser), Sails will attempt to serve one of your views.
    *   If a specific `pathToView` was provided, Sails will attempt to use that view.
    *   Alternatively if `pathToView` was *not* provided, Sails will try to guess an appropriate view (see `res.view()` for details). If Sails cannot guess a workable view, it will just send JSON.
    *   If Sails serves a view, the `data` argument will be accessible as a view local: `data`.

### Example

Using the default view:

```
if ( req.param('amount') < 500 )
  return res.badRequest(
    'Transaction limit exceeded. Please try again with an amount less than $500.'
  );
} 
```

With a custom view:

```
if ( req.param('amount') < 500 )
  return res.badRequest(
    'Transaction limit exceeded. Please try again with an amount less than $500.',
    'salesforce/leads/edit'
  );
} 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.badRequest()` (like other userland response methods) can be overridden or modified. It runs the response method defined in `/responses/badRequest.js`, which is bundled automatically in newly generated Sails apps. If a `badRequest.js` response method does not exist in your app, Sails will implicitly use the default behavior.
> *   This method is called automatically if a call to [`req.validate()`](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) fails any of its validation checks.
> *   By default, the specified error (`err`) will be excluded if the app is running in the "production" environment (i.e. `process.env.NODE_ENV === 'production'`).

<docmeta value="resbadRequest631019" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.badRequest()" name="displayName" class="calibre17"></docmeta>

# res.clearCookie

# res.clearCookie()

Clears cookie (`name`) in the response.

### Usage

```
res.clearCookie(name [,options]); 
```

### Details

The path option defaults to "/".

### Example

```
res.cookie('name', 'tobi', { path: '/admin' });
res.clearCookie('name', { path: '/admin' }); 
```

<docmeta value="resclearCookie314533" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.clearCookie()" name="displayName" class="calibre17"></docmeta>

# res.cookie

# res.cookie()

Sets a cookie with name (`name`) and value (`value`) to be sent along with the response.

### Usage

```
res.cookie(name, value [,options]); 
```

### Details

The "path" option defaults to "/".

The "maxAge" option is a convenience option for setting "expires" relative to the current time in milliseconds. The following is equivalent to the previous example.

```
res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true }) 
```

An object may be passed which is then serialized as JSON, which is automatically parsed by the bodyParser() middleware.

```
res.cookie('cart', { items: [1,2,3] });
res.cookie('cart', { items: [1,2,3] }, { maxAge: 900000 }); 
```

Signed cookies are also supported through this method. Simply pass the signed option. When given res.cookie() will use the secret passed to express.cookieParser(secret) to sign the value.

```
res.cookie('name', 'tobi', { signed: true }); 
```

### Example

```
res.cookie('name', 'tobi', {
  domain: '.example.com',
  path: '/admin',
  secure: true
});

res.cookie('rememberme', '1', {
  expires: new Date(Date.now() + 900000),
  httpOnly: true
}); 
```

<docmeta value="rescookie624994" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.cookie()" name="displayName" class="calibre17"></docmeta>

# res.forbidden

# res.forbidden()

This method is used to send a [403](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error) ("Forbidden") response back down to the client indicating that the request is not allowed. This usually means the user-agent tried to do something it was not allowed to do, like change the password of another user.

### Usage

```
return res.forbidden(); 
```

*Or:*

*   `return res.forbidden(data);`
*   `return res.forbidden(data, pathToView);`

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

By default, it works as follows:

*   If the request "wants JSON" (e.g. the request originated from AJAX, WebSockets, or a REST client like cURL), Sails will send the provided error `data` as JSON. If no `data` is provided a default response body will be sent (the string `"Forbidden"`).
*   If the request *does not* "want JSON" (e.g. a URL typed into a web browser), Sails will attempt to serve one of your views.
    *   If a specific `pathToView` was provided, Sails will attempt to use that view.
    *   Alternatively if `pathToView` was *not* provided, Sails will serve a default error page (the view located at `views/403.ejs`). If that view does not exist, Sails will just send JSON.
    *   If Sails serves a view, the `data` argument will be accessible as a view local: `data`.

### Example

Using the default view:

```
if ( !req.session.canEditSalesforceLeads ) {
  return res.forbidden('Write access required');
} 
```

With a custom view:

```
if ( !req.session.canEditSalesforceLeads ) {
  return res.forbidden(
    ''Write access required'',
    'salesforce/leads/edit'
  );
} 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.forbidden()` (like other userland response methods) can be overridden or modified. It runs the response method defined in `/responses/forbidden.js`, which is bundled automatically in newly generated Sails apps. If a `forbidden.js` response method does not exist in your app, Sails will implicitly use the default behavior.
> *   If `pathToView` refers to a missing view, this method will respond as if the request "wants JSON". +By default, the specified error (`err`) will be excluded if the app is running in the "production" environment (i.e. `process.env.NODE_ENV === 'production'`).

<docmeta value="resforbidden97443" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.forbidden()" name="displayName" class="calibre17"></docmeta>

# res.get

# res.get()

Returns the current value of the specified response header (`header`).

### Usage

```
res.get(header); 
```

### Example

```
res.get('Content-Type');
// -> "text/plain" 
```

### Notes

> *   The `header` argument is case-insensitive. +Response headers can be changed up until the response is sent - see `res.set()`.

<docmeta value="resget697790" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.get()" name="displayName" class="calibre17"></docmeta>

# res.json

# res.json()

Sends a JSON response composed of a stringified version of the specified `data`.

### Usage

```
return res.json([statusCode, ] data); 
```

### Details

This method is identical to res.send() when an object or array is passed, however it may be used for explicit JSON conversion of non-objects (null, undefined, etc), though these are technically not valid JSON.

### Example

```
res.json(null)
res.json({ user: 'tobi' })
res.json(500, { error: 'message' }) 
```

### Notes

> *   Don't forget this method's name is all lowercase.
> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).

<docmeta value="resjson72272" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.json()" name="displayName" class="calibre17"></docmeta>

# res.jsonp

# res.jsonp()

Send a JSON or JSONP response.

Identical to `res.json()`, except if a "callback" parameter exists, a [JSONP](http://en.wikipedia.org/wiki/JSONP) response will be sent instead, using the value of the "callback" parameter as the name of the function wrapper.

### Usage

```
return res.jsonp([statusCode, ] data); 
```

### Example

```
return res.jsonp({
  users: [{
    name: 'Thelma',
    id: 1
  }, {
    name: 'Leonardo'
    id: 2
  }]
}); 
```

### Notes

> *   Don't forget this method's name is all lowercase.
> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).

<docmeta value="resjsonp798206" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.jsonp()" name="displayName" class="calibre17"></docmeta>

# res.location

# res.location()

Sets the "Location" response header to the specified URL expression (`url`).

### Usage

res.location(url);

### Example

```
res.location('/foo/bar');
res.location('foo/bar');
res.location('http://example.com');
res.location('../login');
res.location('back'); 
```

### Notes

> *   You can use the same kind of URL expressions as in res.redirect().

<docmeta value="reslocation779137" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.location()" name="displayName" class="calibre17"></docmeta>

# res.negotiate

# res.negotiate()

Given an error (`err`), send an appropriate error response back down to the client. Especially handy for handling potential validation errors from Model.create() or Model.update().

### Usage

```
return res.negotiate(err); 
```

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

`res.negotiate()` examines the provided error (`err`) and determines the appropriate error-handling behavior from one of the following methods:

*   `res.badRequest()` (400)
*   `res.forbidden()` (403)
*   `res.notFound()` (404)
*   `res.serverError()` (500)

The determination is made based on `err`'s "status" property. If a more specific diagnosis cannot be determined (e.g. `err` doesn't have a "status" property, or it's a string), Sails will default to `res.serverError()`.

### Example

```
// Add Fido's birthday to the database:
Pet.update({name: 'fido'})
  .set({birthday: new Date('01/01/2010')})
  .exec(function (err, fido) {
    if (err) return res.negotiate(err);
    return res.ok(fido);
   }); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.negotiate()` (like other userland response methods) can be overridden - just define a response module (`/responses/negotiate.js`) and export a function definition.
> *   This method is used as the default handler for uncaught errors in Sails. That means it is called automatically if an error is thrown in *any* request handling code, *but only within the initial step of the event loop*. You should always specifically handle errors that might arise in callbacks/promises from asynchronous code.

<docmeta value="resnegotiate730536" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.negotiate()" name="displayName" class="calibre17"></docmeta>

# res.notFound

# res.notFound()

Sends a [404](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error) ("Not Found") response using either res.json() or res.view(). Called automatically when Sails receives a request which doesn't match any of its explicit routes or route blueprints (i.e. serves the 404 page).

When called manually from your app code, this method is normally used to indicate that the user-agent tried to find, update, or delete something that doesn't exist.

### Usage

```
return res.notFound(); 
```

*Or:*

*   `return res.notFound(data);`
*   `return res.notFound(data, pathToView);`

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

By default, it works as follows:

*   If the request "wants JSON" (e.g. the request originated from AJAX, WebSockets, or a REST client like cURL), Sails will send the provided error `data` as JSON. If no `data` is provided a default response body will be sent (the string `"Not Found"`).
*   If the request *does not* "want JSON" (e.g. a URL typed into a web browser), Sails will attempt to serve one of your views.
    *   If a specific `pathToView` was provided, Sails will attempt to use that view.
    *   Alternatively if `pathToView` was *not* provided, Sails will try to guess an appropriate view (see `res.view()` for details). If Sails cannot guess a workable view, it will just send JSON.
    *   If Sails serves a view, the `data` argument will be accessible as a view local: `data`.

### Example

Using the default view:

```
return res.notFound(); 
```

With a custom view:

```
Pet.findOne()
.where(name: 'fido')
.exec(function(err, fido) {
  if (err) return res.serverError(err);
  if (!fido) return res.notFound(undefined,'pet/sorry-that-pet-has-moved');
  // ...
}) 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.notFound()` (like other userland response methods) can be overridden or modified. It runs the response method defined in `/responses/notFound.js`, which is bundled automatically in newly generated Sails apps. If a `notFound.js` response method does not exist in your app, Sails will implicitly use the default behavior.
> *   If `pathToView` refers to a missing view, this method will respond as if the request "wants JSON". +By default, the specified error (`err`) will be excluded if the app is running in the "production" environment (i.e. `process.env.NODE_ENV === 'production'`).

<docmeta value="resnotFound130366" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.notFound()" name="displayName" class="calibre17"></docmeta>

# res.ok

# res.ok()

Send a 200 ("OK") response back down to the client with the provided data. Performs content-negotiation on the request and calls either `res.json()` or `res.view()`.

### Usage

```
return res.ok(); 
```

*Or:*

*   `return res.ok(data);`
*   `return res.ok(data, pathToView);`

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

By default, it works as follows:

*   If the request "wants JSON" (e.g. the request originated from AJAX, WebSockets, or a REST client like cURL), Sails will send the provided `data` as JSON. If no `data` is provided a default response body will be sent (the string `"OK"`).
*   If the request *does not* "want JSON" (e.g. a URL typed into a web browser), Sails will attempt to serve one of your views.
    *   If a specific `pathToView` was provided, Sails will attempt to use that view.
    *   Alternatively if `pathToView` was *not* provided, Sails will try to guess an appropriate view (see `res.view()` for details). If Sails cannot guess a workable view, it will fall back and send JSON.
    *   If Sails serves a view, the `data` argument will be accessible as a view local: `data`.

### Example

```
return res.ok({
  name: 'Loïc',
  occupation: 'developer'
}); 
```

If the request originated from a socket or AJAX request, the response sent from the usage above would contain the following JSON:

```
{
  "name": "Loïc",
  "occupation": "developer"
} 
```

Alternatively, if the code that calls `res.ok()` was located somewhere where a view file could be guessed, that view would be served, with with Loïc available as the `data` local. For example if `res.ok()` was called in `UserController.update`, then we might create the following view as `views/user/update.ejs`:

```
<input type="text" placeholder="Name" value="<%= data.name %>"/>
<input type="text" placeholder="Occupation" value="<%= data.occupation %>"/> 
```

If the code that calls `res.ok()` is not in a controller action, a conventional view cannot be guessed, so Sails will just send back JSON instead.

Finally, if a custom `pathToView` is provided as the second argument, Sails will always use that view instead of guessing, e.g. the following usage will compile and respond with a view located in `views/user/detail.ejs`:

```
return res.ok({
  name: 'Loïc',
  occupation: 'developer'
}, 'user/detail'); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.ok()` (like other userland response methods) can be overridden or modified. It runs the response method defined in `api/responses/ok.js`, which is bundled automatically in newly generated Sails apps. If an `ok.js` response method does not exist in your app, Sails will implicitly use the default behavior.
> *   This method is used by blueprint actions to send a success response. Therefore as you might expect, it is a great place to marshal response data for clients which expect data in a specific format, i.e. to convert data to XML, or it wrap in an additional object (for Ember clients).

<docmeta value="resok847363" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.ok()" name="displayName" class="calibre17"></docmeta>

# res.redirect

# res.redirect()

Redirect the requesting user-agent to the given absolute or relative url.

### Usage

```
return res.redirect(url); 
```

### Arguments

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `url` | ((string)) | A URL expression (see below for complete specification). e.g. `"http://google.com"` or `"/login"` |

### Details

Sails/Express/Koa/Connect support a few forms of redirection, first being a fully qualified URI for redirecting to a different domain:

```
return res.redirect('http://google.com'); 
```

The second form is the domain-relative redirect. For example, if you were on [`example.com/admin/post/new`](http://example.com/admin/post/new), the following redirect to `/admin` would land you at [`example.com/admin`](http://example.com/admin):

```
return res.redirect('/checkout'); 
```

Pathname relative redirects are also possible. If you were on [`example.com/admin/post/new`](http://example.com/admin/post/new), the following redirect would land you at http//example.com/admin/post:

```
return res.redirect('..'); 
```

The final special-case is a back redirect, which allows you to redirect a request back where it came from using the "Referer" (or "Referrer") header (if omitted, redirects to `/` by default)

```
return res.redirect('back'); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   When your app calls `res.redirect()`, Sails sends a response with status code [302](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes#3xx_Redirection). This instructs the user-agent to send a new request to the indicated URL. There is no way to *force* a user-agent to follow redirects, but most clients play nicely.
> *   In general, you should not need to use `res.redirect()` if a request "wants JSON" (i.e. `req.wantsJSON`).
> *   If a request originated from a Socket.io client, it always "wants JSON". If you do call `res.redirect(/#/documentation/reference/res/res.redirect.html)` for a socket request, Sails reroutes the request internally on the server, effectively "forcing" the redirect to take place (i.e. instead of sending a 302 status code, the server simply creates a new request to the redirect URL).
>     *   As a result, redirects to external domains are not supported for socket requests (although this is technically possible by proxying).
>     *   This behavior may change to more closely reflect HTTP in future versions of Sails.

<docmeta value="resredirect444617" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.redirect()" name="displayName" class="calibre17"></docmeta>

# res.send

# res.send()

Send a simple response. `statusCode` defaults to 200 ("OK").

This method is used in the underlying implementation of most of the other terminal response methods.

### Usage

```
return res.send([statusCode,] body); 
```

### Details

This method performs a myriad of useful tasks for simple non-streaming responses such as automatically assigning the Content-Length unless previously defined and providing automatic HEAD and HTTP cache freshness support.

When a Buffer is given the Content-Type is set to "application/octet-stream" unless previously defined as shown below:

```
res.set('Content-Type', 'text/html');
res.send(new Buffer('some html')); 
```

When a String is given the Content-Type is set defaulted to "text/html":

```
res.send('some html'); 
```

When an Array or Object is given Express will respond with the JSON representation:

```
res.send({ user: 'tobi' })
res.send([1,2,3]) 
```

Finally when a Number is given without any of the previously mentioned bodies, then a response body string is assigned for you. For example 200 will respond will the text "OK", and 404 "Not Found" and so on.

```
res.send(200)
res.send(404)
res.send(500) 
```

### Example

```
res.send(new Buffer('whoop'));
res.send({ some: 'json' });
res.send('some html');
res.send(404, 'Sorry, we cannot find that!');
res.send(500, { error: 'something blew up' });
res.send(200); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).

<docmeta value="ressend588955" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.send()" name="displayName" class="calibre17"></docmeta>

# res.serverError

# res.serverError()

This method is used to send a [500](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_Error) ("Server Error") response back down to the client indicating that some kind of server error occurred.

### Usage

```
return res.serverError(); 
```

*Or:*

*   `return res.serverError(data);`
*   `return res.serverError(data, pathToView);`

### Details

Like the other built-in custom response modules, the behavior of this method is customizable.

By default, it works as follows:

*   If the request "wants JSON" (e.g. the request originated from AJAX, WebSockets, or a REST client like cURL), Sails will send the provided error `data` as JSON. If no `data` is provided a default response body will be sent (the string `"Server Error"`).
*   If the request *does not* "want JSON" (e.g. a URL typed into a web browser), Sails will attempt to serve one of your views.
    *   If a specific `pathToView` was provided, Sails will attempt to use that view.
    *   Alternatively if `pathToView` was *not* provided, Sails will serve a default error page (the view located at `views/500.ejs`). If that view does not exist, Sails will just send JSON.
    *   If Sails serves a view, the `data` argument will be accessible as a view local: `data`.

### Example

Using the default error view:

```
return res.serverError('Salesforce could not be reached'); 
```

With a custom view:

```
return res.serverError(
  'Salesforce could not be reached',
  'salesforce/leads/edit'
); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.serverError()` (like other userland response methods) can be overridden or modified. It runs the response method defined in `/responses/serverError.js`, which is bundled automatically in newly generated Sails apps. If a `serverError.js` response method does not exist in your app, Sails will implicitly use the default behavior.
> *   If `pathToView` refers to a missing view, this method will respond as if the request "wants JSON". +By default, the specified error (`err`) will be excluded if the app is running in the "production" environment (i.e. `process.env.NODE_ENV === 'production'`).

<docmeta value="resserverError551750" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.serverError()" name="displayName" class="calibre17"></docmeta>

# res.set

# res.set()

Sets specified response header (`header`) to the specified value (`value`).

Alternatively, you can pass in a single object argument (`headers`) to set multiple header fields at once, where the keys are the header field names, and the corresponding values are the desired values.

### Usage

```
res.set(header, value); 
```

-or-

```
res.set(headers); 
```

### Example

```
 res.set('Content-Type', 'text/plain');

res.set({
  'Content-Type': 'text/plain',
  'Content-Length': '123',
  'ETag': '12345'
}) 
```

<docmeta value="resset167965" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.set()" name="displayName" class="calibre17"></docmeta>

# res.status

# res.status()

Set the status code of this response.

### Usage

```
res.status(200); 
```

### Example

```
res.status(404);
res.send('oops'); 
```

### Notes

> *   The status code may be set up until the response is sent.
> *   `res.status()` is effectively just a chainable alias of node's '`res.statusCode=`.

<docmeta value="resstatus819458" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.status()" name="displayName" class="calibre17"></docmeta>

# res.type

# res.type()

Sets the "Content-Type" response header to the specified `type`.

This method is pretty forgiving (see examples below), but note that if `type` contains a `"/"`, `res.type()` assumes it is a MIME type and interprets it literally.

### Usage

```
res.type(type); 
```

### Example

```
res.type('.html');
res.type('html');
res.type('json');
res.type('application/json');
res.type('png'); 
```

<docmeta value="restype43929" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.type()" name="displayName" class="calibre17"></docmeta>

# res.view

# res.view()

Respond with an HTML page.

### Usage

```
return res.view(pathToView, locals); 
```

*Or:*

*   `return res.view(pathToView);`
*   `return res.view(locals);`
*   `return res.view();`

Uses the [configured view engine](http://beta.sailsjs.org/#/documentation/concepts/Views/ViewEngines.html) to compile the view template at `pathToView` into HTML. If `pathToView` is not provided, serves the conventional view based on the current controller and action.

The specified `locals` are merged with your configured app-wide locals, as well as certain built-in locals from Sails and/or your view engine, then passed to the view engine as data.

### Arguments

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `pathToView` | ((string)) | The path to the desired view file relative to your app's `views` folder (usually `views/`), without the file extension (e.g. `.ejs`), and with no trailing slash. Defaults to "identityOfController/nameOfAction". |
| 2 | `locals` | ((object)) | Data to pass to the view template. These explicitly specified locals will be merged in to Sails' built-in locals and your [configured app-wide locals](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md). Defaults to `{}`. |

### Example

Consider a conventionally configured Sails app with a call to `res.view()` in the `cook()` action of its `OvenController.js`.

With no `pathToView` argument, `res.view()` will decide the path by combining the identity of the controller (`oven`) and the name of the action (`cook`):

```
return res.view();
// -> responds with `views/oven/cook.ejs` 
```

Here's how you would load the same view using an explicit `pathToView`:

```
return res.view('oven/cook');
// -> responds with `views/oven/cook.ejs` 
```

Finally, here's a more involved example demonstrating how `res.view` can be combined with Waterline queries:

```
// Find the 5 hottest oven brands on the market
Oven.find().sort('heat ASC').exec(function (err, ovens){
  if (err) return res.serverError(err);

  return res.view('oven/top5', {
    hottestOvens: ovens
  });
  // -> responds using the view at `views/oven/top5.ejs`,
  // and with the oven data we looked up as view locals.
  //
  // e.g. in the view, we might have something like:
  // ...
  // <% _.each(hottestOvens, function (aHotOven) { %>
  //  <li><%= aHotOven.name %></li>
  // <% }) %>
  // ...
}); 
```

### Notes

> *   This method is **terminal**, meaning it is generally the last line of code your app should run for a given request (hence the advisory usage of `return` throughout these docs).
> *   `res.view()` reads a view file from disk, compiles it into HTML, then streams it back to the client. If you already have the view in memory, or don't want to stream the compiled HTML directly back to the client, use `sails.hooks.views.render()` instead.

<docmeta value="resview916814" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="res.view()" name="displayName" class="calibre17"></docmeta>

# sails.config

# Configuration (`sails.config`)

The `sails.config` object contains the runtime values of your app's configuration. It is assembled automatically when Sails loads your app; merging together command-line arguments, environment variables, your `.sailsrc` file, and the configuration objects exported from any and all modules in your app's `config/` directory.

More specifically, when you load your app, whether that's using `node app`, [programmatic usage inside of a script](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md), or `sails lift`, Sails will look in a [few different places](https://github.com/dominictarr/rc#standards) for configuration. Here they are listed in order of descending priority:

*   an optional object of configuration overrides passed-in programmatically
*   a local `.sailsrc` file in your app's directory, or the first found looking in `../`, `../../` etc.
*   a global `.sailsrc` file in your home folder (e.g. `~/.sailsrc`)
*   command-line arguments (parsed by minimist)
*   environment variables (prefixed with `SAILS_`, e.g. `SAILS_PORT=1492`)
*   files in your app's `config/` directory (if one exists)

<docmeta value="sailsconfig238825" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Configuration" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# sails.config.blueprints

# sails.config.blueprints

By default, Sails controllers automatically bind routes for each of their functions. Additionally, each controller will automatically bind routes for a CRUD API controlling the model which matches its name, if one exists.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `actions` | ((boolean)) | true | Whether routes are automatically generated for every action in your controllers (also maps `index` to `/:controller`) '/:controller', '/:controller/index', and '/:controller/:action' |
| `rest` | ((boolean)) | true | Automatic REST blueprints enabled? e.g. `'get /:controller/:id?'` `'post /:controller'` `'put /:controller/:id'` `'delete /:controller/:id'` |
| `shortcuts` | ((boolean)) | true | These CRUD shortcuts exist for your convenience during development, but you'll want to disable them in production.: `'/:controller/find/:id?'`, `'/:controller/create'`, `'/:controller/update/:id'`, and `'/:controller/destroy/:id'` |
| `prefix` | ((string)) | '' | Optional mount path prefix for blueprints (the automatically bound routes in your controllers) e.g. '/api/v2' |
| `pluralize` | ((boolean)) | false | Optionally use plural controller names in blueprint routes, e.g. `/users` for `api/controllers/UserController.js`. |
| `populate` | ((boolean)) | true | Whether the blueprint controllers should populate model fetches with data from other models which are linked by associations. If you have a lot of data in one-to-many associations, leaving this on may result in very heavy api calls. |
| `defaultLimit` | ((integer)) | 30 | The default number of records to show in the response from a "find" action. Doubles as the default size of populated arrays if `populate` is `true`. |
| `autoWatch` | ((boolean)) | true | Whether to run [`Model.watch()`](http://beta.sailsjs.org/#/documentation/reference/websockets/resourceful-pubsub/watch.html) in the `find` and `findOne` blueprint actions. Can be overridden on a per-model basis. |
| `jsonp` | ((boolean)) | false | Optionally wrap blueprint JSON responses in a JSONP callback using `res.jsonp()` from Express 3. |

<docmeta value="Blueprints187690" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.blueprints" name="displayName" class="calibre17"></docmeta>

# sails.config.bootstrap

# sails.config.bootstrap

### What is this?

This is an asynchronous boostrap function that runs before your Sails app gets lifted (i.e. starts up). This gives you an opportunity to set up your data model, run jobs, or perform some special logic.

### Description

```
module.exports.bootstrap = function (cb) {

  // It's very important to trigger this callback method when you are finished
  // with the bootstrap!  (otherwise your server will never lift, since it's waiting on the bootstrap)
  cb();
}; 
```

<docmeta value="Bootstrap85232" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.bootstrap" name="displayName" class="calibre17"></docmeta>

# sails.config.connections

# sails.config.connections

### What is this?

Adapters are the middle man between your Sails app and some kind of storage (typically a database)

Adapters are configured in the `connections.js` file located in your project's `config` directory. Here you can create different global “saved settings” that you can mix and match in your models.

Sails adapters have been written for a variety of popular databases such as MySQL, Postgres and Mongo. You can find a list of supported adapters [here](https://github.com/balderdashy/sails-wiki/blob/0.9/Database-Support.md).

### Example

To use the `sails-memory` adapter (for DEVELOPMENT ONLY), first install the module with `npm install sails-memory`, then define it in `connections.js`:

Here is an example adapter configuration file

`myApp/config/connections.js`

```
 module.exports.connections = {
  // sails-disk is installed by default.
  localDiskDb: {
    adapter: 'sails-disk'
  },
  memory: {
    adapter: 'sails-memory'
  }
}; 
```

If you wanted to set `memory` as the default adapter for your models, you would do this. `myApp/config/models.js`

```
module.exports.models = {

  connection: 'memory'
}; 
```

> Keep in mind that options you define directly in your model definitions will override these settings. Prior to v0.11, adapters were defined in `myApp/config/Adapters.js`. See v0.9 docs for more info.

### Multiple connections for an adapter

You can set up more than one connection using the same adapter. For example, if you had two mysql databases, you could configure them as:

```
 module.exports.connections = {
  localMysql: {
    adapter: 'sails-mysql',
    user: 'root',
    host: 'localhost',
    database: 'someDbase'
  },
  remoteMysql: {
    adapter: 'sails-mysql',
    user: 'remoteUser',
    password: 'remotePassword',
    host: 'http://remote-mysql-host.com',
    database: 'remoteDbase'
  }
}; 
```

> **Note** If *any* connection to an adapter is used by a model, then *all* connections to that adapter will be loaded on `sails.lift`, whether or not models are actually using them. In the example above, if a model was configured to use the `localMysql` connection, then both `localMysql` and `remoteMysql` would attempt to connect at run time. It is therefore good practice to comment out any connection configurations that you aren't using!

<docmeta value="Connections100765" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.connections" name="displayName" class="calibre17"></docmeta>

# sails.config.cors

# sails.config.cors

Configuration for Sails' [built-in support for Cross-Origin Resource Sharing](http://beta.sailsjs.org/#/documentation/concepts/CORS). CORS specifies how HTTP requests to your app originating from foreign domains should be treated. It is primarily used to allow third-party sites to make AJAX requests to your app, which are normally blocked by browsers following the [same-origin policy](http://en.wikipedia.org/wiki/Same-origin_policy).

These options are conventionally set in the **config/cors.js** configuration file. Note that these settings (with the exception of `allRoutes`) can be changed on a per-route basis in the [**config/routes.js** file](http://beta.sailsjs.org/#/documentation/concepts/Routes/RouteTargetSyntax.html?q=route-target-options).

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `allRoutes` | ((boolean)) | false | Indicates whether the other CORS configuration settings should apply to every route in the app by default. |
| `origin` | ((string)) | `*` | Comma-delimited list of default hosts (beginning with http:// or https://) to give access to, or `*` to allow all domains CORS access. If `allRoutes` is `true` and `origin` is `*`, then your app will be fully accessible to sites hosted on foreign domains (except for routes which have their own CORS settings). |
| `methods` | ((string)) | GET, POST, PUT, DELETE, OPTIONS, HEAD | Comma-delimited list of methods that are allowed to be used in CORS requests. This is only used in response to [preflight requests](https://developer.mozilla.org/en-US/docs/HTTP/Access_control_CORS#Preflighted_requests), so the inclusion of GET, POST, OPTIONS and HEAD, although customary, is not necessary. |
| `headers` | ((string)) | content-type | Comma-delimited list of headers that are allowed to be sent with CORS requests. This is only used in response to [preflight requests](https://developer.mozilla.org/en-US/docs/HTTP/Access_control_CORS#Preflighted_requests). |
| `credentials` | ((boolean)) | true | Indicates whether cookies can be shared in CORS requests. |

### Custom route config example

The following will allow cross-origin AJAX GET, PUT and POST requests to `/foo/bar` from sites hosted `http://foobar.com` and `https://owlhoot.com`. DELETE requests, or requests from sites on any other domains, will be blocked by the browser.

```
'/foo/bar': {
  target: 'FooController.bar',
  cors: {
    origin: 'http://foobar.com,https://owlhoot.com',
    methods: 'GET,PUT,POST,OPTIONS,HEAD'
  }
} 
```

<docmeta value="sailsconfigcors588825999999" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.cors" name="displayName" class="calibre17"></docmeta>

# sails.config.csrf

# sails.config.csrf

Configuration for Sails' built-in [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) protection middleware. These options are conventionally set in the `config/csrf.js` configuration file. See the docs on Cross-Site Request Forgery in the security section for detailed usage instructions.

This option protects your Sails app against cross-site request forgery (or CSRF) attacks. A would-be attacker needs not only a user's session cookie, but also this timestamped, secret CSRF token, which is refreshed/granted when the user visits a URL on your app's domain.

This allows you to have certainty that your users' requests haven't been hijacked, and that the requests they're making are intentional and legitimate.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `csrf` | ((boolean)) or ((object)) | false | CSRF protection is disabled by default to facilitate development. To turn it on, just set `sails.config.csrf` to true, or to an object as described below. |

### csrf object settings

Besides `true` and `false`, you can set `sails.config.csrf` to an object with the following properties:

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `grantTokenViaAjax` | ((boolean)) | true | Whether to activate the **/csrfToken** route, which will return the current CSRF token value which can then be used in AJAX requests. |
| `origin` | ((string)) | '' | Comma-delimited list of origins that are allowed to access the CSRF token via the **/csrfToken** route. This is separate from the other [CORS](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.cors.html) settings, which *do not apply* to **/csrfToken**. |
| `routesDisabled` | ((string)) | '' | Comma-delimited list of routes where CSRF protection is disabled. |

<docmeta value="CSRF353281" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.csrf" name="displayName" class="calibre17"></docmeta>

# sails.config.globals

# sails.config.globals

Configuration for the global variables that Sails exposes to its Node process. The options are conventionally specified in the `config/globals.js` configuration file.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `sails` | ((boolean)) | `true` | Expose the `sails` instance representing your app. If this is disabled, you can still get access via `req._sails`. |
| `models` | ((boolean)) | `true` | Expose each of your app's models as global variables (using their "globalId"). E.g. a model defined in `api/models/User.js` would have a globalId of `User` by default. If this is disabled, you can still access your models via `sails.models.*`. |
| `services` | ((boolean)) | `true` | Expose each of your app's services as global variables (using their "globalId"). E.g. a service defined in `api/models/NaturalLanguage.js` would have a globalId of `NaturalLanguage` by default. If this is disabled, you can still access your services via `sails.services.*`. |
| `_` | ((boolean)) | `true` | Expose the `lodash` installed in Sails core as a global variable. If this is disabled, like [any other node module](https://soundcloud.com/marak/marak-the-node-js-rap) you can always run `npm install lodash --save`, then `var _ = require('lodash')` at the top of any file. |
| `async` | ((boolean)) | `true` | Expose the `async` installed in Sails core as a global variable. If this is disabled, like [any other node module](https://soundcloud.com/marak/marak-the-node-js-rap) you can always run `npm install async --save`, then `var async = require('async')` at the top of any file. |

### Notes

> *   To disable all global variables, you can set `sails.config.globals` to `false`.

<docmeta value="sailsconfigglobals588825999999" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.globals" name="displayName" class="calibre17"></docmeta>

# sails.config.http

# sails.config.http

Configuration for your app's underlying HTTP server. These properties are conventionally specified in the `config/http.js` configuration file.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `middleware` | ((object)) | See [conventional defaults for HTTP middleware](http://beta.sailsjs.org/#/documentation/concepts/Middleware?q=conventional-defaults) | A configuration object of all HTTP middleware functions your app will run on every incoming HTTP request. All [Express](https://github.com/expressjs/) or Connect middleware is supported. [Example](https://gist.github.com/mikermcneil/9cbd68c95839da480e97) |
| `middleware.order` | ((array)) | See [conventional defaults for HTTP middleware order](https://github.com/balderdashy/sails/blob/master/lib/hooks/http/index.js#l51-66) | The order in which middleware should be run for HTTP request (the Sails router, which runs the appropriate explicit routes, policies, controllers, etc. from your app is invoked by the "router" middleware). |
| `cache` | ((number)) | `cache: 31557600000` | The number of seconds to cache flat files on disk being served by Express static middleware (by default, these files are in `.tmp/public`) The HTTP static cache is only active in a 'production' environment (default 1 year), since that's the only time Express will cache flat-files. |
| `serverOptions` | ((object)) | TODO | TODO |

### Notes

> *   Note that this HTTP middleware stack configured in `sails.config.http.middleware` is only applied to true HTTP requests-- it is ignored when handling virtual requests (e.g. sockets)
>     
>     
> *   You cannot define a custom middleware function with the key `order` (since `sails.config.http.middleware.order` has special meaning)

<docmeta value="sailsconfighttp178274" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.http" name="displayName" class="calibre17"></docmeta>

# sails.config.i18n

# sails.config.i18n

Configuration for Sails' built-in internationalization & localization features. For more information see the [concepts section on internationalization](http://beta.sailsjs.org/#/documentation/concepts/Internationalization).

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `locales` | ((array)) | ['en','es','fr','de'] | List of supported [locale codes](http://en.wikipedia.org/wiki/BCP_47) |
| `localesDirectory` | ((string)) | '/config/locales' | The project-relative path to the folder containing your locale translations (i.e. stringfiles) |
| `defaultLocale` | ((string)) | 'en' | The default locale for the site. Note that this setting will be overridden for any request that sends an "Accept-Language" header (i.e. most browsers), but it's still useful if you need to localize the response for requests made by non-browser clients (e.g. cURL). |
| `updateFiles` | ((boolean)) | false | Whether to automatically add new keys to locale (translation) files when they are encountered during a request. |

<docmeta value="sailsconfigi18n588825999999" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.i18n" name="displayName" class="calibre17"></docmeta>

# sails.config.log

# sails.config.log

Configuration for the instance of the [Sails logger](http://beta.sailsjs.org/#/documentation/reference/Logs) (`sails.log`) used in your Sails app. The options are conventionally specified in the config/log.js configuration file.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `level` | ((string)) | `'info'` | Set the level of detail to be shown in your app's log |

<docmeta value="sailsconfiglog812909" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.log" name="displayName" class="calibre17"></docmeta>

# sails.config.models

# sails.config.models

Your default project-wide **model settings**. Can also be overridden on a per-model basis by providing a top-level property with the same name in that model definition. For more details, see the conceptual docs on Model Settings. These options are conventionally specified in the config/models.js configuration file.

```
sails.config.models; 
```

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `attributes` | ((object)) | `{}` | The basic pieces of information to store about a model. See Attributes. |
| `migrate` | ((string)) | *see Model Settings* | How & whether Sails will attempt to automatically rebuild the tables/collections/etc. in your schema |
| `connection` | ((string)) | `"localDiskDb"` | The default database [connection](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.connections.html) any given model will use without a configured override |
| `autoPK` | ((boolean)) | `true` | Toggle the automatic definition of a primary key in your model |
| `autoCreatedAt` | ((boolean)) | `true` | Toggle the automatic definition of a property createdAt in your model |
| `autoUpdatedAt` | ((boolean)) | `true` | Toggle the automatic definition of a property updatedAt in your model |
| `tableName` | ((string)) | *identity* | Used to specify database table name for the model |

<docmeta value="sailsconfigmodels258825" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.models" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# sails.config.policies

# sails.config.policies

> TODO:
> 
> Merge most of the contents of this file into the main reference section on policies. Include a simple config reference table (with only one row with property: `*`) explaining how this particular config module is read. But don't worry about trying to explain what policies are here-- instead, link to the full docs on the subject (again, to reduce duplicate content and make this all more maintainable)

### What is this?

Policies are like any other system for authentication control. You can allow or deny access in fine granularity with policies.

### Description

Your app's ACL (access control list) is located in **config/policies.js**.

#### Applying a Policy

##### To a Specific Action

To apply a policy to a specific action in particular, you should specify it on the right-hand side of that action:

```
{
  ProfileController: {
      edit: 'isLoggedIn'
  }
} 
```

##### To an Entire Controller

To set the default policy mapping for a controller, use the `*` notation:

> **Note:** Default policy mappings do not "cascade" or "trickle down." Specified mappings for the controller's actions will override the default mapping. In this example, `isLoggedIn` is overriding `false`.

```
{
  ProfileController: {
    '*': false,
    edit: 'isLoggedIn'
  }
} 
```

##### Globally

> **Note:** Global policy mappings do not "cascade" or "trickle down" either. Specified mappings, whether they're default controller mappings or for specific actions, will **ALWAYS** override the global mapping. In this example, `isLoggedIn` is overriding `false`.

```
{

  // Anything you don't see here (the unmapped stuff) is publicly accessible
  '*': true,

  ProfileController: {
    '*': false,
    edit: 'isLoggedIn'
  }
} 
```

##### Built-in policies

###### true

> This is the default policy mapped to all controllers and actions in a new project. In production, it's good practice to set this to `false` to prevent access to any logic you might have inadvertently exposed.

Allow public access to the mapped controller/action. This will allow any request to get through, no matter what.

```
module.exports = {
  UserController: {

    // login should always be accessible
    login: true

  }
} 
```

###### false

**NO** access to the mapped controller/action. No requests get through. Period.

```
module.exports = {
  MathController: {

    // This fancy algorithm we're working on isn't done yet
    // so we set it to false to disable it
    someFancyAlgorithm: false

  }
} 
```

##### Custom policies

You can apply one or more policies to a given controller or action. Any file in your `/policies` folder (e.g. `authenticated.js`) is referable in your ACL (`config/policies.js`) by its filename minus the extension, (e.g. `'authenticated'`).

```
module.exports = {
  FileController: {
    upload: ['isAuthenticated', 'canWrite', 'hasEnoughSpace']
  }
} 
```

##### Multiple Policies

To apply two or more policies to a given action, (order matters!) you can specify an array, each referring to a specific policy.

```
UserController: {
    lock: ['isLoggedIn', 'isAdmin']
} 
```

In each of the policies, the next policy in the chain will only be run if `next()`, the third argument, is called. When and if the last policy calls `next()`, the requested controller action is run.

<docmeta value="sailsconfigpolicies753862" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.policies" name="displayName" class="calibre17"></docmeta>

# sails.config.routes

# sails.config.routes

Configuration for custom (aka "explicit") routes. `sails.config.routes` consists of a single Javascript object whose keys are URL paths (the "address") and whose values are one of several types of route handler configurations (the "target"), for example:

```
module.exports.routes = {

    "GET /": {view: "homepage"},
    "POST /foo/bar": {controller: "FooController", action: "bar"}

} 
```

Please see the routes concept overview for a full discussion of Sails routes, and the custom routes documentation for a detailed description of the available configurations for both the route address and target.

<docmeta value="sailsconfigroutes141736" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.routes" name="displayName" class="calibre17"></docmeta>

# sails.config.session

# sails.config.session

### What is this?

Sails session integration leans heavily on the great work already done by Express, but also unifies Socket.io with the Connect session store.

### Description

Sails session integration leans heavily on the great work already done by Express, but also unifies Socket.io with the Connect session store. It uses Connect’s cookie parser to normalize configuration differences between Express and Socket.io and hooks into Sails’ middleware interpreter to allow you to access and auto-save to `req.session` with Socket.io the same way you would with Express.

#### `secret`

Session secret is automatically generated when your new app is created. Replace at your own risk in production-- you will invalidate the cookies of your users, forcing them to log in again.

#### Shared Redis session store

In production, uncomment the following line to set up a shared redis session store that can be shared across multiple Sails.js servers.

```
adapter: 'redis', 
```

The following values are optional, if no options are set a redis instance running on localhost is expected. Read more about options at: [`github.com/visionmedia/connect-redis`](https://github.com/visionmedia/connect-redis)

```
 host: 'localhost',
        port: 6379,
        ttl: <redis session TTL in seconds>,
        db: 0,
        pass: <redis auth password>
        prefix: 'sess:' 
```

Uncomment the following lines to use your Mongo adapter as a session store

```
 adapter: 'mongo',

        host: 'localhost',
        port: 27017,
        db: 'sails',
        collection: 'sessions', 
```

Optional Values:

```
 // Note: url will override other connection settings
        // url: 'mongodb://user:pass@host:port/database/collection',

        username: '',
        password: '',
        auto_reconnect: false,
        ssl: false,
        stringify: true 
```

<docmeta value="sailsconfigsession786744" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.session" name="displayName" class="calibre17"></docmeta>

# sails.config.sockets

# sails.config.sockets

### What is this?

These configuration options provide transparent access to Socket.io, the WebSocket/pubsub server encapsulated by Sails.

### Commonly-Used Options

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `onConnect` | ((function)) | see [config/sockets.js](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/sockets.js.html) | A function to run every time a new client-side socket connects to the server. |
| `onDisconnect` | ((function)) | see [config/sockets.js](http://beta.sailsjs.org/#/documentation/anatomy/myApp/config/sockets.js.html) | A function to run every time a new client-side socket disconnects from the server. |
| `adapter` | ((string)) | `'memory'` | The database where socket.io will store its message queue and answer pubsub logic. Can be set to either `'memory'` or `'redis'` |
| `host` | ((string)) | `'127.0.0.1'` | Hostname of your redis instance (only applicable if using the redis socket store adapter) |
| `port` | ((integer)) | `6379` | Port of your redis instance (only applicable if using the redis socket store adapter) |
| `db` | ((string)) | `'sails'` | The name of the database to use within your redis instance (only applicable if using the redis socket store adapter) |
| `pass` | ((string)) | ((undefined)) | The password for your redis instance (only applicable if using the redis socket store adapter) |

### Advanced Configuration

These configuration options provide lower-level access to the underlying Socket.io server settings for complete customizability.

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `transports` | ((array)) | `['websocket', 'htmlfile', 'xhr-polling', 'jsonp-polling']` | A array of allowed transport methods which the clients will try to use. The flashsocket transport is disabled by default You can enable flashsockets by adding 'flashsocket' to this list. |
| `origins` | ((string)) | `'*:*'` | Match string representing the origins that are allowed to connect to the Socket.IO server |
| `heartbeats` | ((boolean)) | `true` | Sets whether we should use heartbeats to check the health of Socket.IO connections |
| `close timeout` | ((integer)) | `60` | When client closes connection, the number of seconds to wait before attempting a reconnect. This value is sent to the client after a successful handshake. |
| `heartbeat timeout` | ((integer)) | `60` | The max number of seconds between heartbeats sent from the client to the server. This value is sent to the client after a successful handshake. |
| `heartbeat interval` | ((integer)) | `25` | The max number of seconds to wait for an expcted heartbeat before declaring the pipe broken. This number should be less than the `heartbeat timeout` |
| `polling duration` | ((integer)) | `20` | The maximum duration of one HTTP poll; if it exceeds this limit it will be closed. |
| `flash policy server` | ((boolean)) | `true` | Enables the flash policy server if the flashsocket transport is enabled. |
| `flash policy port` | ((integer)) | `10843` | TODO |
| `destroy buffer size` | ((integer)) | `10E7` | Used by the HTTP transports. The Socket.io server buffers HTTP request bodies up to this limit. This limit is not applied to websocket or flashsockets. |
| `destroy upgrade` | ((boolean)) | `true` | Whether we need to destroy non-socket.io upgrade requests |
| `browser client` | ((boolean)) | `true` | Whether Sails/Socket.io should serve the `socket.io.js` client (as well as WebSocketMain.swf for Flash sockets, etc.) |
| `browser client cache` | ((boolean)) | `true` | Whether to cache the Socket.io file generation in the memory of the process to speed up the serving of the static files. |
| `browser client minification` | ((boolean)) | `false` | Whether Socket.io needs to send a minified build of the static client script |
| `browser client etag` | ((boolean)) | `false` | Whether Socket.io needs to send an ETag header for the static requests |
| `browser client expires` | ((integer)) | `315360000` | TODO |
| `browser client gzip` | ((boolean)) | `false` | Whet |

# sails.config.views

# sails.config.views

Configuration for your app's server-side views. The options are conventionally specified in the `config/views.js` configuration file.

### Properties

| Property | Type | Default | Details |
| --- | --- | --- | --- |
| `layout` | ((string)) -or- ((boolean)) | `"layout"` | Set the default layout for your app by specifying the relative path to the desired layout file from your views folder (i.e. `views/`.) Or disable layout support altogether with `false`. |
| `engine` | ((string)) | `"ejs"` | The view engine your app will use to compile server-side markup into HTML. |
| `locals` | ((object)) | `{}` | Default data to be included as view locals every time a server-side view is compiled anywhere in this app. |

### Notes

> *   If your app is NOT using `ejs` (the default view engine) Sails will function as if the `layout` option was set to `false`. To take advantage of layouts when using a custom view engine like Jade or Handlebars, check out that view engine's documentation to find the appropriate syntax.

<docmeta value="sailsconfigviews588825" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.config.views" name="displayName" class="calibre17"></docmeta>

# Waterline

# Waterline (ORM)

By default, Sails comes bundled with an ORM called Waterline (implemented in the [orm hook](https://github.com/balderdashy/sails/tree/master/lib/hooks/orm).)

<docmeta value="Waterline537291" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Waterline (ORM)" name="displayName" class="calibre17"></docmeta>

# Models

# Working with Models

This section of the documentation focuses on the model methods provided by Waterline out of the box. In addition to these, additional methods can come from hooks (i.e. the resourceful pubsub methods), be exposed by the underlying adapters to provide custom functionality, or be hand-written in your app to wrap reusable custom code.

> For an in-depth introduction to models in Sails/Waterline, see [`sailsjs.org/#/documentation/concepts/ORM/Models.html`](http://sailsjs.org/#/documentation/concepts/ORM/Models.html).

![screenshot of a Waterline/Sails model in Sublime Text 2](img/deade1d3.png)

### Built-In Model Methods

In general, model methods are *asynchronous*, meaning you cannot just call them and use the return value. Instead, you must use callbacks, or promises. Most built-in model methods accept a callback as an optional final argument. If the callback is not supplied, a chainable Query object is returned, which has methods like `.where()` and `.exec()`. See Working with Queries for more on that.

| Method | Summary |
| --- | --- |
| `.find()` | Lookup an array of records which match the specified criteria |
| `.findOne()` | Lookup a single record which matches the specified criteria, or send back `null` if it doesn't. |
| `.update()` | Update records matching the specified criteria, setting the specified object of `attrName:value` pairs. |
| `.destroy()` | Destroy records matching the specified criteria. |
| `.findOrCreate()` | Lookup a single record which matches the specified criteria, or create it if it doesn't. |
| `.count()` | Get the total count of records which match the specified criteria. |
| `.native()`/`query()` | Make a direct call to the underlying database driver. |
| `.stream()` | Return a readable (object-mode) stream of records which match the specified criteria |

### `sails.models`

If you need to disable global variables in Sails, you can still use `sails.models.<model_identity>` to access your models.

A model's `identity` is different than its `globalId`. The `globalId` is determined automatically from the name of the model, whereas the `identity` is the all-lowercased version. For instance, you the model defined in `api/models/Kitten.js` has a globalId of `Kitten`, but its identity is `kitten`. For example:

```
// Kitten === sails.models.kitten
sails.models.kitten.find().exec(function (err, allTheKittens) {
  // We also could have just used `Kitten.find().exec(...)`
  // if we'd left the global variable exposed.
}) 
```

<docmeta value="Models537291" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Models" name="displayName" class="calibre17"></docmeta>

# Count

# .count( [`criteria`, ] `callback` )

### Purpose

Returns the number of records in your database that meet the given search criteria.

### Overview

#### Parameters

| # | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | No |
| 2 | Callback | `function` | No |

#### Callback Parameters

| # | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Number of Records | `int` |

### Example Usage

```
User.count({name:'Flynn'}).exec(function countCB(error, found) {
  console.log('There are ' + found + ' users called "Flynn"');

  // There are 1 users called 'Flynn'
  // Don't forget to handle your errors
}); 
```

### Notes

> Any string arguments passed must be the ID of the record.

<docmeta value="count42579" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".count()" name="displayName" class="calibre17"></docmeta>

# Create

# .create( `values`, [`callback`] )

### Purpose

Creates a new instance of this model in the database.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Record(s) to Create | `{}`, `[{}]` | Yes |
| 2 | Callback | `function` | No |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Records Created | `{}`, `[{}]` |

### Example Usage

```
// create a new record with name 'Walter Jr'

User.create({name:'Walter Jr'}).exec(function createCB(err,created){
  console.log('Created user with name '+created.name);
  });

// Created user with name Walter Jr
// Don't forget to handle your errors and abide by the rules you defined in your model 
```

<docmeta value="create312605" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".create()" name="displayName" class="calibre17"></docmeta>

# Destroy

# .destroy( `criteria` , [`callback`] )

### Purpose

Destroys all records in your database that match the given criteria.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | Yes |
| 2 | Callback | `function` | No |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Deleted Records | `[{}]` |

### Example Usage

```
User.destroy({name:'Flynn'}).exec(function deleteCB(err){
  console.log('The record has been deleted');
  });

// If the record existed, then it has been deleted
// Don't forget to handle your errors 
```

### Notes

> If you want to confirm the record exists before you delete it, you must first perform a find() Any string arguments passed must be the ID of the record.

<docmeta value="destroy398816" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="instance" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".destroy()" name="displayName" class="calibre17"></docmeta>

# Find

# .find(`criteria` , [`callback`])

### Purpose

Finds and returns all records that meet the criteria object(s) that you pass it.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | Yes |
| 2 | Callback | `function` | Yes |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Found Records | `[{}]` |

### Example Usage

```
User.find({}).exec(function findCB(err,found){
  while (found.length)
    console.log('Found User with name '+found.pop().name)
  });

// Found User with name Flynn
// Found User with name Jessie

// Don't forget to handle your errors 
```

### Notes

> Any string arguments passed must be the ID of the record. This method will ALWAYS return records in an array. If you are trying to find an attribute that is an array, you must wrap it in an additional set of brackets otherwise Waterline will think you want to perform an inQuery.

<docmeta value="find816978" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="10" name="importance" class="calibre25"></docmeta>

<docmeta value=".find()" name="displayName" class="calibre17"></docmeta>

# Find One

# .findOne( `criteria` , [`callback`] )

### Purpose

This finds and returns a single record that meets the criteria.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`, `string` | Yes |
| 2 | Callback | `function` | Yes |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Found Record | `{}` |

### Example Usage

```
User.findOne({name:'Jessie'}).exec(function findOneCB(err,found){
  console.log('We found '+found.name);
  });

// We found Jessie
// Don't forget to handle your errors 
```

### Notes

> Any string arguments passed must be the ID of the record. If you are trying to find an attribute that is an array, you must wrap it in an additional set of brackets otherwise Waterline will think you want to perform an inQuery.
> 
> If no matching record is found, the value of `found` will be `undefined`. Not finding a record does *not* constitute an error for `findOne`.

<docmeta value="findOne423345" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="10" name="importance" class="calibre25"></docmeta>

<docmeta value=".findOne()" name="displayName" class="calibre17"></docmeta>

# Find Or Create

# .findOrCreate( `criteria` , `record` , [`callback`] )

### Purpose

Checks for the existence of the record in the first parameter. If it can't be found, the record in the second parameter is created.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | Yes |
| 2 | Records to Create | `{}`,`[{}]` | Yes |
| 2 | Callback | `function` | No |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Records Created | `{}`, `[{}]` |

### Example Usage

```
User.findOrCreate({name:'Walter'},{name:'Jessie'}).exec(function createFindCB(err,record){
  console.log('What\'s cookin\' '+record.name+'?');
  });

// What's cookin' Jessie?
// Don't forget to handle your errors and abide by the rules you defined in your model 
```

### Notes

> Any string arguments passed must be the ID of the record. If you are trying to find an attribute that is an array, you must wrap it in an additional set of brackets otherwise Waterline will think you want to perform an inQuery.

<docmeta value="findOrCreate760631" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".findOrCreate()" name="displayName" class="calibre17"></docmeta>

# Native

# .native()

`.native()` is only available when using Sails/Waterline with MongoDB.

Returns a raw Mongo collection instance representing the specified model, allowing you to perform raw Mongo queries.

For full documentation and usage examples, check out the [native Node Mongo driver](https://github.com/mongodb/node-mongodb-native#introduction).

Note that `sails-mongo` maintains a single Mongo connection for each of your configured connections/datastores. Consequently, when using `.native()`, you don't need to close or open `db` manually. For lower-level usage, you can `require('mongodb')` directly.

### Example

```
Pet.native(function(err, collection) {
  if (err) return res.serverError(err);

  collection.find({}, {
    name: true
  }).toArray(function (err, results) {
    if (err) return res.serverError(err);
    return res.ok(results);
  });
}); 
```

Source: [`gist.github.com/mikermcneil/483987369d54512b6104`](https://gist.github.com/mikermcneil/483987369d54512b6104)

### Notes

> *   This method only works with Mongo! For raw functionality in SQL databases, use `.query()`.

<docmeta value="native900002" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".native()" name="displayName" class="calibre17"></docmeta>

# Query

# .query()

`.query()` is only available on Sails/Waterline models using a SQL database (PostgreSQL and mySQL) adapter. Its purpose is to perform raw SQL queries.

### Example

```
Pet.query('SELECT pet.name FROM pet', function(err, results) {
  if (err) return res.serverError(err);
  return res.ok(results);
}); 
```

### Notes

> This method only works with PostgreSQL and mySQL! use .native() for Mongo.

<docmeta value="query546204" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".query()" name="displayName" class="calibre17"></docmeta>

# Stream

# .stream( `criteria` )

### Purpose

This method uses a [node write stream](http://nodejs.org/api/stream.html) to pipe model data as it is retrieved without first having to buffer all of the results to memory.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | Yes |
| 2 | Custom Write/End Methods | `{}` | No |

#### Returned

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Stream of Records | `stream` |

### Example Usage

UsersController.js

```
module.exports = {

  testStream: function(req,res){

    if (req.param('startStream') && req.isSocket){

        var getSocket = req.socket;

        // Start the stream.  Pipe it to sockets.
        User.stream({name:'Walter'}).pipe(getSocket.emit);

    } else {

      res.view();

    }

  }
}
` 
```

views/users/testSocket.ejs

```
<script type="text/javascript">
window.onload = function startListening(){
    socket.on('gotUser',function(data){
      console.log(data.name+' number '+data.id+' has joined the party');
    });
};

</script>
<div class="addButton" onClick="socket.get('/users/testStream/',{startStream:true})">Stream all the Users !</div> 
```

### Notes

> This method is useful for piping data from VERY large models straight to res. You can also pipe it other places. See the node stream docs for more info. Only the mongo, mysql, and posgresql adapters support this method. This won't work with the disk adapter. Any string arguments passed must be the ID of the record.

<docmeta value="stream427721" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".stream()" name="displayName" class="calibre17"></docmeta>

# Update

# .update()

### Purpose

Updates existing records in the database that match the specified criteria.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Find Criteria | `{}`,`[{}]`, `string`, `int` | Yes |
| 2 | Updated Records | `{}`,`[{}]` | Yes |
| 3 | Callback | `function` | No |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Sucessfully Updated Records | `[{}]` |

### Example Usage

```
User.update({name:'Walter Jr'},{name:'Flynn'}).exec(function afterwards(err,updated){

  if (err) {
    // handle error here- e.g. `res.serverError(err);`
    return;
  }

  console.log('Updated user to have name '+updated[0].name);
}); 
```

### Notes

> *   An array of primary key values passed to `.update()` for a `collection` association will set the association to contain **only** the records with those primary key values provided. That is- it **unlinks all other** records from the association.
> *   Although you may pass .update() an object or an array of objects, it will always return an array of objects.
> *   If you specify a primary key (e.g. `7` or `"50c9b254b07e040200000028"`) instead of a criteria object, any `.where()` filters will be ignored.
> *   Currently, calling `.populate()` on an `.update()` query has no effect. To populate attributes on the results, you should follow up your update with a `find().populate()` query.

<docmeta value="update727440" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".update()" name="displayName" class="calibre17"></docmeta>

# Populated Values

# Populated Values

In addition to basic attribute data like email addresses, phone numbers, and birthdates, Waterline can dynamically store and retrieve linked sets of records using associations. When `.populate()` is called on a query, each of the resulting records will contain one or more **populated values**. Each one of those **populated values** is a snapshot of the record(s) linked to that particular association at the time of the query.

The type of a populated value is either:

*   `null`, or a plain old JavaScript object (POJO), or *(if it corresponds to a "model" association)*
*   an empty array, or an array of plain old JavaScript objects *(if it corresonds to a "collection" association)*

For example, assuming we're dealing with orders of adorable wolf puppies:

```
Order.find()
.populate('buyers')  // a "collection" association
.populate('seller')  // a "model" association
.exec(function (err, orders){

  // this array is a snapshot of the Customers who are associated with the first Order as "buyers"
  orders[0].buyers;
  // => [ {id: 1, name: 'Rob Stark'}, {id: 6, name: 'Arya Stark'} ]

  // this object is a snapshot of the Company that is associated with the first Order as the "seller"
  orders[0].seller;
  // => { id: 42941, corporateName: 'WolvesRUs Inc.' }

  // this array is empty because the second Order doesn't have any "buyers"
  orders[1].buyers;
  // => []

  // this is `null` because there is no "seller" associated with the second Order
  orders[1].seller;
  // => null
}); 
```

### Modifying populated values

Changes to populated values are persisted (i.e. saved to the database) by calling `.save()` on the record they are attached to. You cannot call `.save()` directly on a populated value.

Changing or remove the linked record of a "model" association can be accomplished by simply setting the property directly on the original record:

```
orders[1].seller = { corporateName: 'Wolf Orphanage' }; 
```

"collection" associations, on the other hand, *do* have a couple of special (non-enumerable) methods for associating and disassociating linked records. However, `.save()` must still be called on the original record in order for changes to be persisted to the database.

```
orders[1].buyers.add({ name: 'Jon Snow' });
orders[1].save(function (err) { ... }); 
```

### Example

Finally, to put it all together:

```
Order.find()
.populate('buyers')
.exec(function (err, orders){

  orders[1].buyers.add({ name: 'Jon Snow' });
  orders[1].seller = { corporateName: 'Wolf Orphanage' };
  orders[1].save(function (err) {
    // We successfully created a new Customer named Jon and added
    // him to `order[1]` as one of its "buyers".
    // We also created a new company and set it as `order[1]`'s "seller".
    //
    // If we had provided only a primary key value instead of an object,
    // in both cases Waterline would have tried to associate existing
    // Customer and Company records rather than creating new ones.
  });

}); 
```

<docmeta value="populatedvalues790682" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Populated Values" name="displayName" class="calibre17"></docmeta>

# Add

# * .add( `primary key` )

### Purpose

Used to add records to the join table that is automatically generated during a Many-to-Many association. It accepts either the primary key of the model instance (defaults to record ID) or a new record (object) that you want created and to be associated with.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Records | `{}`, `string`, `int` | Yes |

### Example Usage

```
User.find({name:'Mike'}).populate('pets').exec(function(e,r){
  r[0].pets.add(7);
  r[0].save(function(err,res){
    console.log(res);
  }
});

/*

{ pets:
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 7,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Rainbow Dash',
       color: 'blue',
       id: 8,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Applejack',
       color: 'orange',
       id: 9,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) } ],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 19:30:54 GMT-0600 (CST),
  id: 7 }

*/ 
```

### Notes

> *   .add() does not accept arrays of any kind. Don't try it.
> *   Any string arguments passed must be the primary key of the record.
> *   `.add()` alone won't actually persist the change in associations to the databse. You should call `.save()` after using `.add()` or `.remove()`.

<docmeta value="add574043" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="instance" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".add()" name="displayName" class="calibre17"></docmeta>

# Remove

# *.remove( `primary key` )

### Purpose

Used to remove records from the join table that is automatically generated during a many-to-many association. Unlike .add(), it only accepts the primary key of the model instance (defaults to record ID).

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Primary Key | `string`, `int` | Yes |

### Example Usage

```
 User.find({name:'Mike'}).populate('pets').exec(function(e,r){
  r[0].pets.remove(7);
  r[0].save(console.log)
});

  /*

{ pets:
   [ { name: 'Rainbow Dash',
       color: 'blue',
       id: 8,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Applejack',
       color: 'orange',
       id: 9,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) } ],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 19:30:54 GMT-0600 (CST),
  id: 7 }

  */ 
```

### Notes

> *   Any string arguments passed must be the primary key of the record.
> *   `.remove()` alone won't actually persist the change in associations to the databse. You should call `.save()` after using `.add()` or `.remove()`.

<docmeta value="remove790682" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="association" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".remove()" name="displayName" class="calibre17"></docmeta>

# Queries

# Working with Queries

Chainable deferred objects returned from Waterline model methods like `.find()` and `.create()`.

```
var query = Stuff.find(); 
```

You have likely already interacted with query objects in your Sails app. Most of the time, you probably won't think about them as objects *per se*, rather just another part of the syntax for communicating with the database.

The primary purpose of Waterline query instances is to provide a convenient, chainable syntax for working with your models. Methods like `.populate()`, `.where()`, and `.sort()` allow you to refine database calls *before* they're sent down the wire. When you're ready to fire the query off to the database, you can just call `.exec()`.

### Promises

In addition to the `.exec()` method, Waterline queries implement a partial integration with the [q](https://github.com/kriskowal/q) promise library, exposing `.then()` and `.catch()` methods.

```
Stuff.find()
.then(function (allTheStuff) {...})
.catch(function (err) {...}); 
```

If you are a fan of promises, and have a reasonable amount of experience with them, you should have no problem working with this interface. However if you are not very familiar with promises, or don't care one way or another, you will probably have an easier time working with `.exec()`, which uses standard Node.js callback conventions.

```
Stuff.find()
.exec(function (err, allTheStuff) {...}) 
```

### Query Execution

When you **execute** a query, a lot happens:

```
Zookeeper.find().exec(function (err, zookeepers){
  // would you look at all those zookeepers?
}); 
```

First, it is "shaken out" by Waterline core into a normalized criteria object. Then it passes through the relevant Waterline adapter(s) for translation to the raw query syntax of your database(s) (e.g. Redis or Mongo commands, various SQL dialects, etc.) Finally, each involved adapter uses its native Node.js database driver to send the query out over the network to the corresponding physical database.

When the adapter receives a response, it is marshalled to the Waterline interface spec and passed back up to Waterine core, where it is integrated with any other raw adapter responses into a coherent result set. At that point, it undergoes one last normalization before being passed back to your callback for consumption by your app.

### Notes

> *   Waterline model methods will **NOT** return a query instance if an optional callback is directly passed as the final argument. Instead, that callback will be triggered when the query is complete.

<docmeta value="query820682" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Queries" name="displayName" class="calibre17"></docmeta>

# Exec

# .exec(`callback`)

### Purpose

This is run at the end of a chain of stringable methods. It signals the adapter to run the query.

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Callback | `function` | Yes |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Data Returned | `{}`, `[{}]`, `int` |

### Example Usage

```
// refer to any of the examples above 
```

### Notes

> The .find() method returns a chainable object if you don't supply a callback. This method can be chained to .find() to further filter your results.
> 
> If you don't run .exec(), your query will not execute.

<docmeta value="exec550068" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".exec()" name="displayName" class="calibre17"></docmeta>

# Limit

# .limit(`integer`)

### Purpose

### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Number to Return | `int` | Yes |

### Example Usage

```
var myQuery = User.find();
myQuery.limit(12);

myQuery.exec(function callBack(err,results){
    console.log(results)
    }); 
```

### Notes

> The .find() method returns a chainable object if you don't supply a callback. This method can be chained to .find() to further filter your results.

<docmeta value="limit203606" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".limit()" name="displayName" class="calibre17"></docmeta>

# Populate

# .populate( `foreignKey`, [`query`] )

### Purpose

This chainable method is used between .find()/.update() and .exec() in order to retrieve records associated with the model being queried. You must supply the Foreign Key specified in your model config.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Foreign Key | `string` | Yes |
| 2 | Query | `object` | No |

### Example Usage

```
 User.find({name:'Mike'}).exec(function(e,r){
  console.log(r[0].toJSON())
})

/* 
{ name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/

User.find({name:'Mike'}).populate('pets').exec(function(e,r){
  console.log(r[0].toJSON())
});

/*
{ pets: 
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 7,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Rainbow Dash',
       color: 'blue',
       id: 8,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Applejack',
       color: 'orange',
       id: 9,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) } ],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/

User.find({name:'Mike'}).populate('pets',{color:'pink'}).exec(function(e,r){
  console.log(r[0].toJSON())
});

/*
{ pets: 
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 7,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) }],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/ 
```

### Notes

> Any string arguments passed must be the primary key of the record.

<docmeta value="populate245634" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="association" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".populate()" name="displayName" class="calibre17"></docmeta>

# Populate All

# .populateAll( [`query`] )

### Purpose

This chainable method is used between .find()/.update() and .exec() in order to retrieve records associated with the model being queried. All known associations of your model will be populated and the query will be applied to each of them.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Query | `object` | No |

### Example Usage

```
 User.find({name:'Mike'}).exec(function(e,r){
  console.log(r[0].toJSON())
})

/* 
{ name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/

User.find({name:'Mike'}).populateAll().exec(function(e,r){
  console.log(r[0].toJSON())
});

/*
{ poneys:
   [ { name: 'Twinky',
       color: 'brown',
       id: 1,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) } ],
  pets: 
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 7,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Rainbow Dash',
       color: 'blue',
       id: 8,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) },
     { name: 'Applejack',
       color: 'orange',
       id: 9,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) } ],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/

User.find({name:'Mike'}).populateAll({color:'pink'}).exec(function(e,r){
  console.log(r[0].toJSON())
});

/*
{ pets: 
   [ { name: 'Pinkie Pie',
       color: 'pink',
       id: 7,
       createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
       updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) }],
  name: 'Mike',
  age: 16,
  createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
  id: 7 }
*/ 
```

### Notes

> Any string arguments passed must be the primary key of the record.

<docmeta value="populate245634" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="association" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".populateAll()" name="displayName" class="calibre17"></docmeta>

# Skip

# .skip(`integer`)

### Purpose

### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Number to Skip | `int` | Yes |

### Example Usage

```
var myQuery = User.find();
myQuery.skip(12);

myQuery.exec(function callBack(err,results){
    console.log(results)
    }); 
```

### Notes

> The .find() method returns a chainable object if you don't supply a callback. This method can be chained to .find() to further filter your results.

<docmeta value="skip128737" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".skip()" name="displayName" class="calibre17"></docmeta>

# Sort

# .sort(`string`)

### Purpose

### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Sort String | `string` | Yes |

### Example Usage

```
var myQuery = User.find();

var sortString= 'name ASC';

// Sort strings look like this

// '<Model Attribute> <sort type>' 

myQuery.sort('name ASC');

myQuery.exec(function callBack(err,results){
    console.log(results)
    }); 
```

### Notes

> The .find() method returns a chainable object if you don't supply a callback. This method can be chained to .find() to further filter your results.
> 
> Other Sort Types include
> 
> *   ASC
> *   DESC

<docmeta value="sort822396" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".sort()" name="displayName" class="calibre17"></docmeta>

# Where

# .where(`criteria`)

### Purpose

### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Criteria Object | `{}` | Yes |

### Example Usage

```
var myQuery = User.find();
myQuery.where({'name':{startsWith:'W'}});

myQuery.exec(function callBack(err,results){
    console.log(results)
    }); 
```

### Notes

> The .find() method returns a chainable object if you don't supply a callback. This method can be chained to .find() to further filter your results.

<docmeta value="where700717" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="mcm" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".where()" name="displayName" class="calibre17"></docmeta>

# Records

# Records

A record is a uniquely identifiable object that corresponds 1-to-1 with a database entry; e.g. a row in Oracle/MSSQL/PostgreSQL/MySQL, a document in MongoDB, or a hash in Redis.

```
Order.findOne().exec(function (err, order){
  var record = order;
}); 
```

For the most part, records are just plain old JavaScript objects (aka POJOs). However they do have a few protected (non-enumerable) methods for formatting their wrapped data, as well as a special method (`.save()`) for persisting [programmatic changes](http://en.wikipedia.org/wiki/Active_record_pattern) to the database.

<docmeta value="record890682" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Records" name="displayName" class="calibre17"></docmeta>

# Save

# * .save(`callback`)

### Purpose

The `save()` method updates your record in the database using the current attributes. It then returns the newly saved object in the callback.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Callback | `function` | Yes |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |
| 2 | Saved Record | `{ }` |

### Example Usage

```
User.find().exec(
  function(err,myRecords){

    // Grab a record off the top of the returned array and save a new attribute to it
    var getOneRecord = myRecords.pop();
    getOneRecord.name = 'Hank';
    getOneRecord.save(
      function(err,s){
        console.log('User with ID '+s.id+' now has name '+s.name);
      });
  });

// User with ID 1 now has name Hank

// Don't forget to handle your errors.
// Don't forget to abide by the rules you set in your model 
```

### Notes

> This is an instance method. Currently, instance methods ARE NOT TRANSACTIONAL. Because of this, it is recommended that you use the equivalent model method instead.

<docmeta value="save581656" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="association" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".save()" name="displayName" class="calibre17"></docmeta>

# To JSON

# .toJSON()

### Purpose

This method also returns a cloned model instance. This one however includes all instance methods. Be sure to read the notes on this one.

### Overview

#### Return Value

|  | Description | Possible Data Types |
| --- | --- | --- |
|  | Cloned Record | `{ }` |

### Example Usage

```
User.find().exec(
  function(err,myRecord){
    var datUser = myRecord.pop().toObject();
    console.log(datUser);
  });

/* { id: 2,
  createdAt: '2013-10-31T22:42:25.459Z',
  updatedAt: '2013-11-01T20:12:55.534Z',
  name: 'Hank',
  phoneNumber: '101-150-1337' } */

User.find().exec(
  function(err,myRecord){
    var datUser = myRecord.pop().toJSON();
    console.log(datUser);
  });

/* { id: 2,
  createdAt: '2013-10-31T22:42:25.459Z',
  updatedAt: '2013-11-01T20:12:55.534Z',
  name: 'Hank' } */

// Don't forget to handle your errors 
```

For model

```
module.exports = {
  attributes: {
    name: 'string',
    phoneNumber: 'string',

    // Override the default toJSON method

    toJSON: function() {
      var obj = this.toObject();
      delete obj.phoneNumber;
      return obj;
    }
  }
} 
```

### Notes

> The real power of toJSON relies on the fact every model instance sent out via res.json is first passed through toJSON. Instead of writing custom code for every controller action that uses a particular model (including the "out of the box" blueprints), you can manipulate outgoing records by simply overriding the default toJSON function in your model.
> You would use this to keep private data like email addresses and passwords from being sent back to every client.
> 
> This is an instance method. Currently, instance methods ARE NOT TRANSACTIONAL. Because of this, it is recommended that you use the equivalent model method instead.

<docmeta value="toJSON161307" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="instance" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".toJSON()" name="displayName" class="calibre17"></docmeta>

# To Object

# .toObject()

### Purpose

The toObject method returns a cloned model instance (record) but stripped of all instance methods.

### Overview

#### Return Value

|  | Description | Possible Data Types |
| --- | --- | --- |
|  | Cloned Record | `{ }` |

### Example Usage

*See usage in .toJSON()*

### Notes

> You will only want to use .toObject when overriding the default .toJSON instance method.

<docmeta value="toObject330342" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="instance" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".toObject()" name="displayName" class="calibre17"></docmeta>

# Validate

# * .validate(`callback`)

### Purpose

Checks the current keys/values on the record against the validations specified in the attributes object of your model.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Callback | `function` | Yes |

#### Callback Parameters

|  | Description | Possible Data Types |
| --- | --- | --- |
| 1 | Error | `Error` |

### Example Usage

```
User.find().exec(
  function(err,myRecords){

    // Grab a record off the top, change it to the wrong data type, then try to validate
    var getOneRecord = myRecords.pop();
    getOneRecord.name = ['Marie','Hank'];
    getOneRecord.name.validate(
      function(err){
        if (err)
          console.log(JSON.stringify(err));
      });
  });

// {"ValidationError":{"name":[{"data":["Marie","Hank"],"message":"Validation error: \"Marie,Hank\" is not of type \"string\"","rule":"string"}]}} 
```

For model

```
module.exports = {

  attributes: {
    name: 'string'

  }

}; 
```

### Notes

> This is shorthand for `Model.validate({ attributes }, cb)` If you `.save()` without first validating, Waterline tries to convert. If it can't, it will throw an error. In this case, it would have converted the array to the string 'Marie,Hank'
> 
> There will be no parameters in the callback unless there is an error. No news is good news.
> 
> This is an instance method. Currently, instance methods ARE NOT TRANSACTIONAL. Because of this, it is recommended that you use the equivalent model method instead.

<docmeta value="validate76690" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="instance" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".validate()" name="displayName" class="calibre17"></docmeta>

# Websockets

# WebSockets

### Overview

There are two main continents in the world of WebSockets- the client (e.g. browser) and the server (e.g. your routes, controllers, and so forth).

<docmeta value="websockets293545" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="WebSockets" name="displayName" class="calibre17"></docmeta>

# Resourceful Pubsub

# Resourceful PubSub

### Overview

For apps that rely heavily on real-time client-server communication--for example, peer-to-peer chat and social networking apps--sending and listening for socket events can quickly become overwhelming. Sails helps smooth away some of this complexity by introducing the concept of Resourceful PubSub ([Publish / Subscribe](http://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)). Every model (AKA *resource*) in your app is automatically equipped with class methods for subscribing sockets to notifications about instance creations, updates and deletions. If you’re using the Blueprint API, socket messages are automatically broadcast to subscribed sockets when a model event occurs. If not, you can use the methods described in this section to manually communicate model events to clients.

### Listening for events on the client

While you are free to use any Javascript library to listen for socket events on the client, Sails does provide its own Socket Client as a convenient way to communicate with the server. Using the Sails socket client makes listening for resourceful pubsub events as easy as:

```
io.socket.on("<model name>", listenerFunction) 
```

### Example

Let’s say you have a model named `User` in your app, with a single “name” attribute. First, we’ll add a listener for “user” events:

```
io.socket.on("user", function(event){console.log(event);}) 
```

This will log any notifications about `User` models to the console. However, we won’t receive any such messages until we *subscribe* to the existing `User` model instances. If you’re using the default blueprints, you can subscribe by making a socket request from the client to `/user`:

```
io.socket.get("/user", function(resData, jwres) {console.log(resData);}) 
```

This requests the current list of users from the Sails server, and subscribes the client to events about each user. Additionally, if the [`autoWatch` setting](http://beta.sailsjs.org/#/documentation/reference/sails.config/sails.config.blueprints.html?q=properties) is on (the default), the client will also be notified whenever a new `User` is created, and will automatically be subscribed to the new user. The callback in this example simply logs the user list to the console. See the [socket.get](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js/socket.get.html) reference for more info about this method.

It’s important to note that in order for the subscription to take place, the `/user` request must be made via a websocket call, *not* a regular HTTP request. That is, using an AJAX request (e.g. `jQuery.get("/user")`) will *not* result in the client being subscribed to resourceful pubsub messages about `User`. However, once the subscription is made, *any* changes to models--whether they be the result of a socket call, an AJAX request, even a cURL request from the command line--will cause the client to receive a notification. Continuing with the above example, if you were to open up a new browser window and go to the following URL:

```
/user/create?name=joe 
```

You would see something like the following in the console of the first window:

```
{
    data: {
        createdAt: "2014-08-01T05:50:19.855Z"
        id: 1
        name: "joe"
        updatedAt: "2014-08-01T05:50:19.855Z"
    },
    id: 1,
    verb: "created"
} 
```

The `verb` indicates the kind of action that occurred. The `id` refers to the instance that the action occurred on, and `data` contains more information about the `User` that was acted upon. Each event type sends back slightly different information; see the individual resourceful pubsub method reference documents for more info.

<docmeta value="resourcefulpubsub293545" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Resourceful PubSub" name="displayName" class="calibre17"></docmeta>

# Message

# .message( `models`,`data`, [`request`] )

### Purpose

Publishes a custom message to a model’s subscribers.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Record (or ID of record) to send message to | `int`, `string`, `object` | Yes |
| 2 | Message payload | `object` | Yes |
| 3 | Request | `request object` | No |

`message()` emits a socket message using the model identity as the event name. The message is broadcast to all sockets subscribed to the model instance via the `.subscribe` model method.

The socket message is an object with the following properties:

*   **id** - the `id` attribute of the model instance
*   **verb** - `"messaged"` (a string)
*   **data** - the message payload

#### `data`

Arbitrary data to send to the subscribed sockets.

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

<docmeta value="message373731" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".message()" name="displayName" class="calibre17"></docmeta>

# Publish Add

# .publishAdd( `{id}`,`attribute`, `idAdded`, [`request`], [`options`] )

### Purpose

Publishes a notification when an associated record is added to a model's collection. For example, if a `User` model has an association with the `Pet` model so that a user can have one or more pets available in its `pets` attribute, then any time a new pet is associated with a user `publishAdd` may be called.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | ID of Updated Record | `int`, `string` | Yes |
| 2 | Attribute of associated collection | `string` | Yes |
| 3 | ID of associated record that was added | `int`, `string` | Yes |
| 4 | Request | `request object` | No |
| 5 | Additional Options | `object` | No |

`publishAdd()` emits a socket message using the model identity as the event name. The message is broadcast to all sockets subscribed to the model instance via the `.subscribe` model method.

The socket message is an object with the following properties:

*   **id** - the `id` attribute of the model instance
*   **verb** - `"addedTo"` (a string)
*   **attribute** - the name of the model attribute that was added to
*   **addedId** - the ID of the record that was added

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

#### `options.noReverse`

See the documentation for `publishUpdate` for information about `options.noReverse`. In general, you should not have to set this argument unless you are writing your own implementation of `publishAdd` for a model.

<docmeta value="publishAdd129964" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".publishAdd()" name="displayName" class="calibre17"></docmeta>

# Publish Create

# .publishCreate( `data`,[`request`] )

### Purpose

PublishCreate doesn't actually create anything. It simply publishes information about the creation of a model instance via websockets. PublishCreate is called automatically by the [blueprint `create` action](https://github.com/balderdashy/sails-docs/blob/0.10/reference/Blueprints.md#create-a-record).

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Data to Send | `object` | Yes |
| 2 | Request | `Request object` | No |

The default implementation of publishCreate only publishes messages to the firehose, and to sockets subscribed to the model class using the `watch` method. It also subscribes all sockets "watching" the model class to the new instance. The socket message to subscribers will include the following properties:

*   **id** - the `id` attribute of the new model instance
*   **verb** - `"created"` (a string)
*   **data** - an object-- the attributes and values of the new model instance

#### `data`

An object containing the attributes and values of the new model instance.

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

### Example Usage

UsersController.js

```
module.exports = {

  testSocket: function(req,res){

        var nameSent = req.param('name');

        if (nameSent && req.isSocket){

          User.create({name:nameSent}).exec(function created(err,newGuy){
            User.publishCreate({id:newGuy.id,name:newGuy.name});
            console.log('A new user called '+newGuy.name+' has been created');
          });

        } else if (req.isSocket){

          User.watch(req);
          console.log('User with socket id '+sails.sockets.id(req)+' is now subscribed to the model class \'users\'.');

        } else {

          res.view();

        }
    }
}

    // Don't forget to handle your errors 
```

views/users/testSocket.ejs

```
 <script type="text/javascript"> window.onload = function subscribeAndListen(){
    // When the document loads, send a request to users.testSocket
    // The controller code will subscribe you to the model 'users'
    socket.get('/users/testSocket/');

    // Listen for the event called 'user' emited by the publishCreate() method.
    socket.on('user',function(obj){
      if (obj.verb == 'created') {
         var data = obj.data;
         console.log('User '+data.name+' has been created.');
      }
    });
};

function makeNew(){

    // Send the new users name to the 'testSocket' action on the 'users' contoller

    socket.get('/users/testSocket/',{name:'Walter'});
} </script>
<div class="addButton" onClick="makeNew()">Click Me to add a new 'Walter' ! </div> 
```

<docmeta value="publishCreate671839" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".publishCreate()" name="displayName" class="calibre17"></docmeta>

# Publish Destroy

# .publishDestroy( `{id}`, [`request`], [`options`] )

### Purpose

Publish the destruction of a model

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | ID of Destroyed Record | `int`, `string` | Yes |
| 2 | Request | `request object` | No |
| 3 | Additional options | `object` | No |

`publishDestroy()` emits a socket message using the model identity as the event name. The message is broadcast to all sockets subscribed to the model instance via the `.subscribe` model method.

The socket message is an object with the following properties:

*   **id** - the `id` attribute of the model instance
*   **verb** - `"destroyed"` (a string)
*   **previous** - an object--if present, contains the attributes and values of the object that was destroyed.

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

#### `options.previous`

If this is set, it is expected to be a representation of the model before it was destroyed. This may be used to send out additional notifications to associated records.

### Example Usage

UsersController.js

```
module.exports = {

  testSocket: function(req,res){

        var nameSent = req.param('name');

        if (nameSent && req.isSocket){

          User.findOne({name:nameSent}).exec(function findIt(err,foundHim){
            User.destroy({id:foundHim.id}).exec(function destroy(err){
              User.publishDestroy(foundHim.id);
            });
          });

        } else if (req.isSocket){

        User.find({}).exec(function(e,listOfUsers){
          User.subscribe(req.socket,listOfUsers);
        console.log('User with socket id '+req.socket.id+' is now subscribed to all of the model instances in \'users\'.');
        });

        } else {

          res.view();

        }

  }
}

    // Don't forget to handle your errors 
```

views/users/testSocket.ejs

```
 <script type="text/javascript"> window.onload = function subscribeAndListen(){
    // When the document loads, send a request to users.testSocket
    // The controller code will subscribe you to all of the 'users' model instances (records)
    socket.get('/users/testSocket/');

    // Listen for the event called 'message' emited by the publishDestroy() method.
    socket.on('message',function(obj){
      if (obj.verb == 'destroyed') {
        console.log('User '+obj.previous.name+' has been destroyed .');
      }
    });
};

function destroy(){

    // Send the name to the testSocket action on the 'Users' contoller
    socket.get('/users/testSocket/',{name:'Walter'});
} </script>
<div class="addButton" onClick="destroy()">Click Me to destroy user 'Walter' ! </div> 
```

### Notes

> Any string arguments passed must be the ID of the record.

<docmeta value="publishDestroy732227" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".publishDestroy()" name="displayName" class="calibre17"></docmeta>

# Publish Remove

# .publishRemove( `{id}`,`attribute`, `idRemoved`, [`request`], [`options`] )

### Purpose

Publishes a notification when an associated record is removed to a model's collection. For example, if a `User` model has an association with the `Pet` model so that a user can have one or more pets available in its `pets` attribute, then any time a pet is removed from a user's `pets` collection, `publishRemove` may be called.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | ID of Updated Record | `int`, `string` | Yes |
| 2 | Attribute of associated collection | `string` | Yes |
| 3 | ID of associated record that was removed | `int`, `string` | Yes |
| 4 | Request | `request object` | No |
| 5 | Additional Options | `object` | No |

`publishRemove()` emits a socket message using the model identity as the event name. The message is broadcast to all sockets subscribed to the model instance via the `.subscribe` model method.

The socket message is an object with the following properties:

*   **id** - the `id` attribute of the model instance
*   **verb** - `"removedFrom"` (a string)
*   **attribute** - the name of the model attribute that was removed from
*   **removedId** - the ID of the record that was removed

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

#### `options.noReverse`

See the documentation for `publishUpdate` for information about `options.noReverse`. In general, you should not have to set this argument unless you are writing your own implementation of `publishRemove` for a model.

<docmeta value="publishRemove468150" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".publishRemove()" name="displayName" class="calibre17"></docmeta>

# Publish Update

# .publishUpdate( `{id}`,[`changes`],[`request`],[`options`] )

### Purpose

PublishUpdate updates nothing. It publishes information about the update of a model instance via websockets.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | ID of Updated Record | `int`, `string` | Yes |
| 2 | Updated values | `{}` | No |
| 3 | Request | `request object` | No |
| 4 | Additional Options | `object` | No |

`publishUpdate()` emits a socket message using the model identity as the event name. The message is broadcast to all sockets subscribed to the model instance via the `.subscribe` model method.

The socket message is an object with the following properties:

*   **id** - the `id` attribute of the model instance
*   **verb** - `"updated"` (a string)
*   **data** - an object-- the attributes that were updated
*   **previous** - an object--if present, the previous values of the updated attributes

#### `changes`

This should be an object containing any changed attributes and their new values.

#### `request`

If this argument is included then the socket attached to that request will *not* receive the notification.

#### `options.previous`

If the `options` object contains a `previous` property, it is expected to be a representation of the model instance's attributes *before* they were updated. This may be used to determine whether or not to publish additional messages (see the `options.noReverse` flag below for more info).

#### `options.noReverse`

The default implementation of `publishUpdate` will, if `options.previous` is present, check whether any associated records were affected by the update, and possibly send out additional notifications. For example, if a `Pet` model has an `owner` attribute that is associated with the `User` model so that a user may own several pets, and the data sent with the call to `publishUpdate` indicates that the value of a pet's `owner` changed, then an additional `publishAdd` or `publishRemove` call may be made. To suppress these notifications, set the `options.noReverse` flag to `true`. In general, you should not have to set this flag unless you are writing your own implementation of `publishUpdate` for a model.

### Example Usage

UsersController.js

```
module.exports = {

  testSocket: function(req,res){

        var nameSent = req.param('name');

        if (nameSent && req.isSocket){

          User.update({name:nameSent},{name:'Heisenberg'}).exec(function update(err,updated){
            User.publishUpdate(updated[0].id,{ name:updated[0].name });
          });

        } else if (req.isSocket){

        User.find({}).exec(function(e,listOfUsers){
          User.subscribe(req.socket,listOfUsers);
        console.log('User with socket id '+req.socket.id+' is now subscribed to all of the model instances in \'users\'.');
        });

        } else {

          res.view();

        }
    }
}

    // Don't forget to handle your errors 
```

views/users/testSocket.ejs

```
<script type="text/javascript"> window.onload = function subscribeAndListen(){
    // When the document loads, send a request to users.testSocket
    // The controller code will subscribe you to all of the 'users' model instances (records)
    socket.get('/users/testSocket/');

    // Listen for the event called 'user'
    socket.on('user',function(obj){
      if (obj.verb == 'updated') {
        var previous = obj.previous;
        var data = obj.data;
        console.log('User '+previous.name+' has been updated to '+data.name);
      }
    });
};

function doEdit(){

    // Send the name to the testSocket action on the 'Users' contoller

    socket.get('/users/testSocket/',{name:'Walter'});
} </script>
<div class="addButton" onClick="doEdit()">Click Me to add a new User! </div> 
```

<docmeta value="publishUpdate712330" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta name="dis

# Subscribe

# .subscribe(`request`,`records`,[`contexts`])

### Purpose

This subscribes clients to one or more existing model instances (records). It allows clients to see message emitted by .publishUpdate(), .publishDestroy(), .publishAdd() and .publishRemove().

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Request | `Request object` | Yes |
| 2 | Records | `[]`, `object` | Yes |
| 3 | Contexts to subscribe to | `string`, `array` | No |

*Note*: `subscribe` will only work when the request is made over a socket connection (e.g. using `socket.get`), *not* over an http connection (e.g. using `jquery.get`).

#### `context`

If you specify a specific context (or array of contexts) to subscribe to, you will only get messages sent in that context. For example, `User.subscribe(socket, user, 'update')` will cause the socket to receive messages only when `publishUpdate` is called for `user`. Subsequent calls to `subscribe` are cumulative, so if you called `User.subscribe(socket, user, 'destroy')` later with the same socket, that socket would then be subscribed to messages from both `publishUpdate` and `publishDestroy`.

You can omit `context` to subscribe a socket to the default contexts for that model class. The default contexts are defined by the `autosubscribe` property of the model class. If `autosubscribe` is not present, then the default contexts are `update`, `destroy`, `message` (for custom messages), `add:*` and `remove:*` (publishAdd and publishRemove messages for associated models).

### Example Usage

Controller Code

```
 // Subscribes client to ONLY the create and destroy events for every `User` record.

    User.find({}).exec(function(e,listOfUsers){
        User.subscribe(req.socket,listOfUsers,['create','destroy']);
    });

    // Don't forget to handle your errors 
```

### Blueprints and .subscribe()

> By default, the blueprint `find` and `findOne` actions will call `.subscribe()` to subscribe a requesting socket to all returned records. However, the blueprint `update` and `delete` actions will *not* cause a message to be sent to the requesting socket by default--only to the *other* connected sockets. This is intended to allow the caller of `io.socket.update()` (for example) to use the client-side SDK's callback to handle the server response separately. To force the blueprint actions to send messages to all sockets, *including the requesting socket*, set `sails.config.blueprints.mirror` to `true`.

<docmeta value="subscribe342218" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".subscribe()" name="displayName" class="calibre17"></docmeta>

# Unsubscribe

# .unsubscribe(`request`,`records`,[`contexts`])

### Purpose

This method will unsubscribe a socket from one or more model instances.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Request | `Request object` | Yes |
| 2 | Records | `[]`, `object` | Yes |
| 3 | Contexts to unsubscribe from | `string`, `array` | No |

*Note*: `unsubscribe` will only work when the request is made over a socket connection (e.g. using `socket.get`), *not* over an http connection (e.g. using `jquery.get`).

#### `context`

See `.subscribe()` for a discussion of pubsub contexts. Omit this argument to unsubscribe a socket from all contexts.

### Example Usage

Controller Code

```
User.findOne({id: 123}).exec(function(err, userInstance) {
    User.unsubscribe(req.socket, userInstance);
}); 
```

<docmeta value="unsubscribe354769" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".unsubscribe()" name="displayName" class="calibre17"></docmeta>

# Unwatch

# .unwatch(`request`)

### Purpose

This unsubscribes a client from publishCreate events for the model.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Request | `request object` | Yes |

*Note*: `unwatch` will only work when the request is made over a socket connection (e.g. using `socket.get`), *not* over an http connection (e.g. using `jquery.get`).

<docmeta value="unwatch872661" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".unwatch()" name="displayName" class="calibre17"></docmeta>

# Watch

# .watch(`request`)

### Purpose

This subscribes a client to publishCreate events for the model. Any connections that are "watching" the model class will be automatically subscribed to new model instances that are created using the blueprint `create` method.

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Request | `request object` | Yes |

*Note*: `watch` will only work when the request is made over a socket connection (e.g. using `socket.get`), *not* over an http connection (e.g. using `jquery.get`).

### Blueprints and .watch()

> By default, the blueprint `find` and `findOne` actions will call `.watch()` on the model class. This behavior can be changed for all models by setting the `sails.config.blueprints.autoWatch` to `false`, or for a specific model by setting `autoWatch` to `false` in the model's class file.

<docmeta value="watch67265" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="pubsub" name="methodType" class="calibre25"></docmeta>

<docmeta value="undefined" name="importance" class="calibre25"></docmeta>

<docmeta value=".watch()" name="displayName" class="calibre17"></docmeta>

# sails.io.js

# Socket Client (`sails.io.js`)

> This section of the docs is about the Sails socket client SDK for the browser. It is written in JavaScript and is also usable on the server.
> 
> There are also a handful of community projects implementing Sails/Socket.io clients for native iOS, Android, and Windows Phone.

### Overview

The Sails socket client ([`sails.io.js`](https://github.com/balderdashy/sails.io.js)) is a tiny browser library that is bundled by default in new Sails apps. It is a lightweight wrapper that sits on top of the Socket.IO client whose purpose is to make sending and receiving messages from your Sails backend as simple as possible.

The main responsibility of `sails.io.js` is to provide a familiar ajax-like interface for communicating with your Sails app using WebSockets/Socket.io. That basically means providing `.get()`, `.post()`, `.put()`, and `.delete()` methods that let you take advantage of realtime features while still reusing the same backend routes you're using for the rest of your app. In other words, running `io.socket.post('/user')` in your browser will be routed within your Sails app exactly the same as an HTTP POST request to the same route.

### Can I use this with...

Yes. The Sails socket client can be used to great effect with any front-end framework-- no matter whether it's angular, backbone, ember, knockout, etc.

### Do I have to use this?

No. The Sails socket client is extremely helpful when building realtime/chat features in a browser-based UI, but like the rest of the `assets/` directory, it is probably not particularly useful if you are building a native Android app, or an API with no user interface.

Fortunately, like every other boilerplate file and folder in Sails, the socket client is completely optional. To remove it, just delete `assets/js/depencencies/sails.io.js`.

<docmeta value="BrowserSDK293544" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Socket Client" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# io.socket.on

# io.socket.on()

Starts listening for server-sent events from Sails with the specified `eventIdentity`. Will trigger the provided callback function when a matching event is received.

### Usage

```
io.socket.on(eventIdentity, function (msg) {
  // ...
}); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `eventIdentity` | ((string)) | The unique identity of a server-sent event, e.g. "recipe" |
| 2 | `callback` | ((function)) | Will be called when the server emits a message to this socket. |

##### Callback

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `msg` | ((object)) | Message sent from the Sails server |

Note that the callback will NEVER trigger until one of your back-end controllers, models, services, etc. sends a message to this socket. Typically that is achieved one of the following ways:

###### Resourceful Pubsub Methods

*   server publishes a message about a record to which this socket is subscribed (see Model.publishUpdate(), Model.publishDestroy(), and Model.subscribe())
*   server publishes a message informing all permitted watcher sockets that a new record has been created in the model with the same identity as `eventIdentity` (see Model.publishCreate(/#/documentation/reference/websockets/resourceful-pubsub/publishCreate.html) and Model.watch())

###### Low-Level Socket Methods

*   server emits a message to all known sockets (see sails.sockets.blast())
*   server emits a message directly to this socket (`io.socket`) using its unique id (see sails.sockets.emit())
*   server broadcasts to a room in which this socket (`io.socket`) has been allowed to join (remember that a socket only stays subscribed as long as it is connected-- i.e. as long as the browser tab is open)

### Example

Listen for new orders and updates to existing orders:

```
io.socket.on('order', function onServerSentEvent (msg) {
  // msg => {...whatever the server published/emitted...}
}); 
```

##### Another example, this time using Angular:

> Note that this Angular example assumes the backend calls `publishCreate()` at some point.

```
angular.module('cafeteria').controller('CheckoutCtrl', function ($scope) {

  $scope.orders = $scope.orders || [];

  if (!io.socket.alreadyListeningToOrders) {
    io.socket.alreadyListeningToOrders = true;
    io.socket.on('order', function onServerSentEvent (msg) {

      // Let's see what the server has to say...
      switch(msg.verb) {

        case 'created':
          $scope.orders.push(msg.data); // (add the new order to the DOM)
          $scope.$apply();              // (re-render)
          break;

        default: return; // ignore any unrecognized messages
      }
    });
  }
}); 
```

### Notes

> *   When listening for resourceful pubsub calls, the `eventIdentity` is the same as the identity of the calling model (e.g. if you have a model "UserComment", the identity is "usercomment".)
> *   For context-- these types of server-sent events are sometimes referred to as ["comet"](http://en.wikipedia.org/wiki/Comet_(programming)) messages.

<docmeta value="socketon682488" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.on()" name="displayName" class="calibre17"></docmeta>

# socket.delete

# socket.delete()

Sends a virtual DELETE request to a Sails server using Socket.io.

### Usage

```
io.socket.delete(url, data, function (data, jwres){
  // ...
}); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `url` | ((string)) | The destination URL path, e.g. "/checkout". |
| 2 | `data` | ((*)) | Optional request data- if provided, will be URL encoded and appended to `url` (existing query string params in url will be preserved) |
| 3 | `callback` | ((function)) | Optional callback- if provided, will be called when the server responds. |

##### Callback

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `resData` | ((*)) | Data received in the response from the Sails server (=== `jwres.body`, equivalent to the HTTP response body.) |
| 2 | `jwres` | ((JWR)) | The [JSON WebSocket Response](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) object. Has `headers`, a `body`, and a `statusCode`. |

### Example

```
<script> io.socket.delete('/users/9', function (resData) {
  resData; // => {id:9, name: 'Timmy Mendez', occupation: 'psychic'}
}); </script> 
```

<docmeta value="socketdelete671580" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.delete()" name="displayName" class="calibre17"></docmeta>

# socket.get

# socket.get()

Sends a virtual GET request to a Sails server using Socket.io.

### Usage

```
io.socket.get(url, data, function (data, jwres){
  // ...
}); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `url` | ((string)) | The destination URL path, e.g. "/checkout". |
| 2 | `data` | ((*)) | Optional request data- if provided, will be URL encoded and appended to `url` (existing query string params in url will be preserved) |
| 3 | `callback` | ((function)) | Optional callback- if provided, will be called when the server responds. |

##### Callback

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `resData` | ((*)) | Data received in the response from the Sails server (=== `jwres.body`, equivalent to the HTTP response body.) |
| 2 | `jwres` | ((JWR)) | The [JSON WebSocket Response](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) object. Has `headers`, a `body`, and a `statusCode`. |

### Example

```
<script> io.socket.get('/users/9', function (resData) {
  resData; // => {id:9, name: 'Timmy Mendez'}
}); </script> 
```

<docmeta value="socketget480208" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.get()" name="displayName" class="calibre17"></docmeta>

# socket.post

# socket.post()

Sends a virtual POST request to a Sails server using Socket.io.

### Usage

```
io.socket.post(url, data, function (data, jwres){
  // ...
}); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `url` | ((string)) | The destination URL path, e.g. "/checkout". |
| 2 | `data` | ((*)) | Optional request data- if provided, will be JSON-encoded and included as the virtual HTTP body |
| 3 | `callback` | ((function)) | Optional callback- if provided, will be called when the server responds. |

##### Callback

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `resData` | ((*)) | Data received in the response from the Sails server (=== `jwres.body`, equivalent to the HTTP response body.) |
| 2 | `jwres` | ((JWR)) | The [JSON WebSocket Response](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) object. Has `headers`, a `body`, and a `statusCode`. |

### Example

```
<script> io.socket.post('/users', { name: 'Timmy Mendez' }, function (resData) {
  resData; // => {id:9, name: 'Timmy Mendez'}
}); </script> 
```

<docmeta value="socketpost175407" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.post()" name="displayName" class="calibre17"></docmeta>

# socket.put

# socket.put()

Sends a virtual PUT request to a Sails server using Socket.io.

### Usage

```
io.socket.put(url, data, function (data, jwres){
  // ...
}); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `url` | ((string)) | The destination URL path, e.g. "/checkout". |
| 2 | `data` | ((*)) | Optional request data- if provided, will be JSON-encoded and included as the virtual HTTP body |
| 3 | `callback` | ((function)) | Optional callback- if provided, will be called when the server responds. |

##### Callback

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `resData` | ((*)) | Data received in the response from the Sails server (=== `jwres.body`, equivalent to the HTTP response body.) |
| 2 | `jwres` | ((JWR)) | The [JSON WebSocket Response](https://github.com/balderdashy/sails-docs/blob/master/PAGE_NEEDED.md) object. Has `headers`, a `body`, and a `statusCode`. |

### Example

```
<script> io.socket.put('/users/9', { occupation: 'psychic' }, function (resData) {
  resData; // => {id:9, name: 'Timmy Mendez', occupation: 'psychic'}
}); </script> 
```

<docmeta value="socketput168503" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.put()" name="displayName" class="calibre17"></docmeta>

# socket.request

# io.socket.request()

Sends a virtual request to a Sails server using Socket.io.

This method is wrapped by the other `io.socket.*`() request methods, which should be used instead.

*   [io.socket.get()](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js/socket.get.html)
*   [io.socket.post()](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js/socket.post.html)
*   [io.socket.put()](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js/socket.put.html)
*   [io.socket.delete()](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.io.js/socket.delete.html)

Please do not use `io.socket.request()` directly unless you know what you're doing.

<docmeta value="socketrequest682488" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="io.socket.request()" name="displayName" class="calibre17"></docmeta>

# sails.sockets

# Sockets (sails.sockets)

### Overview

Sails exposes several low-level methods for realtime communication with the client via `sails.sockets`. These methods are implemented using a [Socket.io](http://socket.io) connection which is available as `sails.io`; however, using the `sails.sockets` methods instead will future-proof your app against possible changes in underlying implementation. If your app is mainly sending messages to the client regarding changes in your models, you should try and use the [model PubSub methods](https://github.com/balderdashy/sails-docs/blob/0.10/reference/ModelMethods.md#publishcreate-datasocket-) instead.

### Looking for `sails.io`?

For raw access to the underlying [socket.io](http://socket.io/) singleton, you can still access `sails.io`. But starting with Sails v0.11, you should use `sails.sockets` for most low-level use-cases involving sockets, since `sails.io` may be deprecated in an upcoming release to allow for more flexibility/extensibility in the underlying socket implementation.

<docmeta value="Sockets505826" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets" name="displayName" class="calibre25"></docmeta>

<docmeta value="3" name="stabilityIndex" class="calibre17"></docmeta>

# sails.sockets.blast

# sails.sockets.blast()

Broadcast a message to all sockets connected to the server.

```
sails.sockets.blast(data); 
```

*Or:*

*   `sails.sockets.blast(eventName, data);`
*   `sails.sockets.blast(data, socketToOmit);`
*   `sails.sockets.blast(eventName, data, socketToOmit);`

### Usage

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | eventName | ((string)) | Optional. Defaults to `'message'`. |
| 2 | data | ((*)) | The data to send in the message. |
| 3 | socketToOmit | ((Socket)) | Optional. If provided, that request socket will **not** receive the message blasted out to everyone else. Useful when the broadcast-worthy event is triggered by a requesting user who doesn't need to hear about it again. |

### Example

In a controller action...

```
sails.sockets.blast('user_logged_in', {
  msg: 'User #' + req.session.userId + ' just logged in.',
  user: {
    id: req.session.userId,
    username: req.session.username
  }
}, req.socket); 
```

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketsblast345475" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.blast()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.broadcast

# sails.sockets.broadcast( `roomName`, [`event`], `data`, [`socketToOmit`] )

Broadcast a message to a room.

```
sails.sockets.broadcast(roomName, data); 
```

*Or:*

*   `sails.sockets.broadcast(roomName, eventName, data);`
*   `sails.sockets.broadcast(roomName, data, socketToOmit);`
*   `sails.sockets.broadcast(roomName, eventName, data, socketToOmit);`

### Usage

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | roomName | ((string)) | The room to broadcast a message in (see [sails.sockets.join](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.sockets/sails.sockets.join.html)) |
| 2 | eventName | ((string)) | Optional. Defaults to `'message'`. |
| 3 | data | ((*)) | The data to send in the message. |
| 4 | socketToOmit | ((Socket)) | Optional. If provided, that socket will *not* receive the message. This is useful if you trigger the broadcast from a client, but don't want that client to receive the message itself (for example, sending a message to everybody else in a chat room). |

### Example

```
sails.sockets.broadcast('artsAndEntertainment', { msg: 'Hi there!' }); 
```

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketsbroadcast253997" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.broadcast()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.emit

# sails.sockets.emit( `socketIds`, [`event`], `data`)

### Purpose

Send a message to one or more sockets by ID.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | IDs of sockets to receive message | `string`, `array` | Yes |
| 2 | Event name | `string` | No |
| 3 | Message data | `object` | Yes |

### Example Usage

```
// Controller action

sayHiToFriend: function(req, res) {
    var friendId = req.param('friendId');
    sails.sockets.emit(friendId, 'privateMessage', {from: req.session.userId, msg: 'Hi!'});
    res.json({
      message: 'Message sent!'
    });
} 
```

<docmeta value="sailssocketsemit963182" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.emit()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.id

# sails.sockets.id()

Gets the ID of a request socket object.

```
sails.sockets.id(socket); 
```

### Usage

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | socket | ((Socket)) | A request socket (WebSocket/Socket.io) object e.g. `req.socket`. |

Once acquired, the socket object's ID can be used to send direct messages to that socket (see [sails.sockets.emit](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.sockets/sails.sockets.emit.html)) or get information about the rooms that the socket is subscribed to (see [sails.sockets.socketRooms](http://beta.sailsjs.org/#/documentation/reference/websockets/sails.sockets/sails.sockets.rooms.html)).

### Example

```
// Controller action

getSocketID: function(req, res) {
  if (!req.isSocket) return res.badRequest();

  var socketId = sails.sockets.id(req.socket);
  // => "BetX2G-2889Bg22xi-jy"

  return res.ok('My socket ID is: ' + socketId);
} 
```

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketsid240053" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.id()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.join

# sails.sockets.join()

Subscribes a socket to a generic room.

### Usage

```
sails.sockets.join(socket, roomName); 
```

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | `socket` | ((string)) -or- ((socket)) | The socket to be subscribed. May be specified by the socket's id or a raw socket object. |
| 2 | `roomName` | ((string)) | The name of the room to which the socket will be subscribed. If the room does not exist yet, it will be created. |

### Example

In a controller action:

```
subscribeToFunRoom: function(req, res) {
  var roomName = req.param('roomName');
  sails.sockets.join(req.socket, roomName);
  res.json({
    message: 'Subscribed to a fun room called '+roomName+'!'
  });
} 
```

*Note: `req.socket` is only valid if the action is triggered via a socket request, e.g. `socket.get('/subscribeToFunRoom/someRoomName')`*

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketsjoin958690" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.join()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.leave

# sails.sockets.leave( `socket`, `roomName` )

### Purpose

Unsubscribe a socket from a generic room.

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Socket object | `object` | Yes |
| 2 | Room Name | `string` | Yes |

### Example Usage

```
// Controller action

leaveFunRoom: function(req, res) {
    var roomName = req.param('roomName');
    sails.sockets.leave(req.socket, roomName);
    res.json({
      message: 'Left a fun room called '+roomName+'!'
    });
} 
```

*Note: `req.socket` is only valid if the action is triggered via a socket request, e.g. `socket.get('/leaveFunRoom/someRoomName')`*

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketsleave425459" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.leave()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.rooms

# sails.sockets.rooms()

### Purpose

Get the list of all current socket rooms

### Overview

#### Parameters

None.

### Example Usage

```
// Controller action

getRoomsList: function(req, res) {
    var roomNames = JSON.stringify(sails.sockets.rooms());
    res.json({
      message: 'A list of all the rooms: '+roomNames
    });
} 
```

*Note: In Socket.io, all sockets are automatically subscribed to a global room with an empty name (''). This room is not returned as part of the array in `sails.sockets.rooms`*

<docmeta value="sailssocketsrooms183984" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.rooms()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.socketRooms

# sails.sockets.socketRooms( `socket` )

### Purpose

Get the list of rooms a socket is subscribed to

### Overview

#### Parameters

|  | Description | Accepted Data Types | Required ? |
| --- | --- | --- | --- |
| 1 | Socket | `object` | Yes |

### Example Usage

```
// Controller action

getMyRooms: function(req, res) {
    var roomNames = JSON.stringify(sails.sockets.socketRooms(req.socket));
    res.json({
      message: 'I am subscribed to: '+roomNames
    });
} 
```

### Notes

> *   The phrase "request socket" here refers to an application-layer WebSocket/Socket.io connection. `req.socket` also exists for HTTP requests, but it refers to the underlying TCP socket at the transport layer, which is different. Be sure and ensure `req.isSocket == true` before using `req.socket` with this method.

<docmeta value="sailssocketssocketRooms270469" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.socketRooms()" name="displayName" class="calibre17"></docmeta>

# sails.sockets.subscribers

# sails.sockets.subscribers()

Get the IDs of all sockets subscribed to a room.

```
sails.sockets.subscribers(roomName); 
```

### Usage

|  | Argument | Type | Details |
| --- | --- | --- | --- |
| 1 | roomName | ((string)) | The name of the room whose socket ids should be retrieved. e.g. `'supportchat'` |

### Example

```
sails.sockets.subscribers('supportchat');
// => ['BetX2G-2889Bg22xi-jy', 'BTA4G-8126Kr32bi-za'] 
```

<docmeta value="sailssocketssubscribers65666" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="sails.sockets.subscribers()" name="displayName" class="calibre17"></docmeta>