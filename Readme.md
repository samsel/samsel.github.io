## My Personal Blog - [Learn Log](http://samsel.github.io/ "Learn Log")

### setup
```bash
$ npm install -g hexo
$ git clone https://github.com/samsel/samsel.github.io.git
$ cd samsel.github.io
$ git submodule sync
$ git submodule update --init --recursive
$ npm install
$ hexo server
```

### deploy
```bash
$ hexo gm
$ hexo deploy
```

### todos
* enable tagcloud
```
<div class="widget tagcloud">
	<%- tagcloud() %>
</div>
```
* use github gist for source code snippets