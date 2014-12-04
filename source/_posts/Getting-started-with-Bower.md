title: Getting started with Bower
date: 2014-12-06 18:45:58
tags: ['bower', 'frontend','javascript']
---

The very first time I came across [Bower](http://bower.io/), I was confused in getting a grasp of what Bower was and why would any developer need it. Over a period of few months since then, I really got to deep dive into Bower and I was so amazed that how I was working on web projects without using Bower before. In this article, I summarize my learings about Bower and why I strongly recommend using it.

#### What is Bower after all?
<sup>*"Web sites are made of lots of things — frameworks, libraries, assets, utilities, and rainbows. Bower manages all these things for you."*  - Source:  [Bower.io](http://bower.io/) </sup>
In simple terms, Bower is a system that takes care of _managing_ the app's _dependencies_.
By __managing__ meaning, Bower answers the below:
	+ what dependency to install?
	+ where to install?
	+ what version to use?
	+ where is the dependency located?

__dependencies__ could be framework, library, bunch of files, etc.. that your web app depends upon. Example: In my project I might be using jQuery, Backbone, Boootstrap. All those could be dependencies, potentially managed by Bower. 

#### How to setup Bower?
<script src="https://gist.github.com/samsel/a8a8f8e99e2432d246b5.js"></script>

Bower's command line interface can be installed via [npm](https://www.npmjs.org/) . Its just a one time thing and from then on, in any project that I want to use Bower, I can simply do

<script src="https://gist.github.com/samsel/6a035ae932ceab470677.js"></script>
The complete list of commands supported by Bower can be found [here](http://bower.io/docs/api/). 


#### How is Bower different from NPM?

#### Can I publish my stuff to Bower?
It modularization of front end web app code into packages and maintain versions of it.