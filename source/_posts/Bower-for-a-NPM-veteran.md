title: Bower - for a NPM veteran
date: 2014-12-07 23:44:19
tags: ['Bower', 'frontend','javascript']
---

Me being a [Node.js](http://nodejs.org/) freak, am used to the [npm](https://www.npmjs.org/) ecosystem. But the very first time I came across [Bower](http://Bower.io/), I was confused in getting a grasp of what Bower was and why would any developer need it. Over a period of few months since then, I really got to deep dive into Bower and I was so amazed that how I was working on web projects without using Bower before. In this article, we are going to look at some compelling reasons to start using Bower as a front-end dependency manager wearing the Node.js hat.

#### What is Bower after all?
<sup>*"Web sites are made of lots of things — frameworks, libraries, assets, utilities, and rainbows. Bower manages all these things for you."*  - Source:  [Bower.io](http://Bower.io/) </sup>
In simple terms, Bower is a system that takes care of _managing_ the app's _dependencies_.
By __managing__ meaning, Bower answers the below:
	+ what dependency to install?
	+ where to install?
	+ what version to use?
	+ where is the dependency located?

__dependencies__ could be framework, library, bunch of files, etc.. that your web app depends upon. Example: In my project I might be using jQuery, Backbone, Bootstrap. All those could be dependencies, potentially managed by Bower. Sounds a lot like npm? Bower and npm share many things in common. They both share the common goal of being a great dependency manager and they follow very similar semantics. For example, both have a `json` manifest for the package info, have registries for package sharing, expose a powerful command line interface written in JavaScript, etc. but there are subtle differences that makes Bower standout as a front end package manager. 

#### How is Bower different from npm?
Even though Bower and npm are dependency management tools, the main difference is that npm facilitates nested dependencies using the commonJS style specification. But Bower on the other hand doesn't enforce any dependency structure and also it delegates the responsibility of dependency resolution on to the consumer of the package. Bower's concept of flat dependency makes it a powerful package manager for the front end as it shoots for a minimization of resource loading by avoiding duplicate loading of the same dependency from multiple packages. The only downside is that the package consumer is made to setup all the required dependencies. To clearly understand what I mean by setup, consider the widely popular web application framework [backbone.js](http://backbonejs.org/). Backbone itself has a hard dependency on Underscore library. Like a other good dependency manager, both Bower and npm add Underscore as a dependency in their package manifest file, but npm takes it one step further by internally setting up the Underscore when the consumer of the package uses Backbone but Bower doesn't do that. The consumer has to manually add Underscore either to their html file manually or to the package loader (AMD based Require.js) based on how the consumer's project is written.

<script src="https://gist.github.com/samsel/051fcd2b2b5085d1c40a.js"></script>

#### How to setup Bower?
<script src="https://gist.github.com/samsel/a8a8f8e99e2432d246b5.js"></script>

Interestingly, Bower's command line interface can be installed via npm. It's just a one time thing and from then on, in any project that I want to use Bower, I can simply do

<script src="https://gist.github.com/samsel/6a035ae932ceab470677.js"></script>

The complete list of commands supported by Bower can be found [here](http://Bower.io/docs/api/). Similar to npm's package.json, Bower uses a manifest file called `Bower.json` to store the meta info about the package contents. A sample manifest could look something like below

<script src="https://gist.github.com/samsel/b2a24a65032c34c615dd.js"></script>


#### The Bower registry
Bower enables sharing of modules by publishing to the Bower registry. As of today, Bower registry is open without any authentication or user management. So anybody can publish anything to bower registry on a first come first serve basis as long as they meet Bower's package requirements of having a valid spec file `bower.json`. The other unique thing about Bower registry is that it simply relies on the package being hosted in Github repository accessible to itself. Bower registry does not deal with storing tarballs of packages but rather just stores a hash of the package name to the Github url where the package is located.

<script src="https://gist.github.com/samsel/df53d55b8727b84ee1bb.js"></script>


In conclusion, Bower is a great step forward for enhancing the workflow of modern web application development. Gone are those days of downloading every front end library off their respective websites to get going on a web project. Given Bower's flat dependency tree of dependency management and unrestrictive file type contents to have images, CSS, JavaScript etc as contents of a package, it naturally fits as a great front-end dependency manager.


