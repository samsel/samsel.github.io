title: Powerful Backbone.js Principles
date: 2014-11-25 18:17:18
tags: ['backbone.js', 'single-page-apps', 'javascript']
---

[Backbone.js](http://backbonejs.org/ 'Backbone.js') is a great framework for building web applications in a sane way. Given minimalism philosophy as its core strength, it passes the responsibilty of writing well maintanable business logic on top of Backbone to the developer. Some of the techniques and best practices that I figured out lately after working on multiple Backbone.js projects are below.

##### 1. Keep Backbone Modules Simple
Adopt minimalism from Backbone.js and keep modules tight and simple. Breakdown code into smaller reusable modules for testability and readability. In the below example, we have a `BaseModel` from which all models are extended. This way we can start abstracting out the commanalities into separate modules. A sample use case would be that; you might want to do your app specific logic for every instance of model, like pinging analytics. The key thing to note is that, we call the BaseModel's initialize from the dervied model. Through the prototype chain, this executes the respective function from the module that we extended.
<script src="https://gist.github.com/samsel/1c3ae4487e3482057d67.js"></script>


##### 2. Create a manager or controller
Backbone is great that it provides Models/Collections for business logic and data, Views for DOM stuff and Router for the browser history state. But this leaves the most important thing to the developer, that is tying all these together to create the application. Any app needs to have a bootstrap module to do the startup work when its loaded the first time in the browser. This can be accomplised by coding up a manager or controller. This would be a Singleton and this would be the place to boot up the app and do things like the view to show, set up jQuery config, etc.. This singleton could also serve as the cental hub that could be use as a data bus or messaging bus for the entire app.


##### 3. Make dumb views
Literally try to make the views as dumb as possible. Shove all the business logic to models and always back the views with a template. Ideally views should just deal with DOM operations and updating the state of the model. All the other side effects of updating state to the model should be handled by events the model spits out. Often in large scale apps its important to pull the routing and navigation out of the views and move them into controllers.


##### 4. Scope your DOM Accessors
Backbone View provides a cached version of the view object that can be accessed using `viewObject.$el`. Its preferred to use this cached selector to do DOM manipulations because all the operations are scoped to the cached selector and they naturally run faster.


##### 5. Do n/w ops in model
Often times, it might be tempting to do network calls from views, but don’t use $.ajax ever in views! Do all network operations inside the model. Design the app in such a way that all data operations are scoped to models, this way we keep the app consistent and also get the poweful data manipulation apis of Backbone Model plus MVC is not violated. 


##### 6. Build views as components
Any web application that accepts user input would have characteristics like data type restriction, validation, ranges, etc.. Abstract those user interface elements with their characteristics coded up in one bundle as a component. View components help in avoiding Backbone view code smell limiting the DOM apis surfacing inside them. Below is an example of a phone number view component inside a Backbone view.
<script src="https://gist.github.com/samsel/891fd2f1c319d3cea531.js"></script>

##### 7. Use a module loader
If you have the practice of allowing only one entity/module in a file along with Backbone's notion to separate out things into nice views/models you will see a mammoth file count as the app grows. It soon becomes harder to include them in the html especially if order of loading matters. So simply put, its best to leave the loading dependencies task to a JavaScript module loader like [requirejs](http://requirejs.org).

<br>

On a ending note, not everything is applicable everywhere or for everyone. But I believe that the above pointers are great for anyone venturing into Backbone apps. With the Backbone community so vibrant, most often the things that we need are already available from the community's contribution and that we don't need to write everything from scratch. [backplug.io](http://backplug.io/) is a great aggregator of Backbone plugins and for anybody looking to deep dive into Backbone, [backbone-fundamentals](http://addyosmani.github.io/backbone-fundamentals/) is a great start.

