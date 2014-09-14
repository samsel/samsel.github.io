## My Personal Blog - [Learn Log](http://samsel.github.io/ "Learn Log")

### setup
```bash
$ git clone https://github.com/samsel/samsel.github.io.git
$ cd samsel.github.io
$ git submodule sync
$ git submodule update --init --recursive
$ hexo server
```

### deploy
```bash
$ hexo gm
$ hexo deploy
```

#### todos
* enable tagcloud
```
<div class="widget tagcloud">
	<%- tagcloud() %>
</div>
```