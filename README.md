# gotpl [![NPM version][npm-image]][npm-url]

A lightweight, high-performance JavaScript template engine.

## Installation

```bash
$ npm install gotpl --save
```

## Examples

```ejs
<h1>Projects</h1>
<ul id="list"></ul>

<% if (projects.length) { %>
	<% for (var i = 0, l = projects.length; i < l; ++i) { %>
		<% var item = projects[i]; %>
		<li class="item">
			<a target="_blank" href="<%=item.url%>"><%= item.name %></a>
		</li>
	<% } %>
<% } %>
```

## Usages

### Browser

```js
var data = {
	projects: [{
		"name": "gotpl",
		"url": "https://github.com/Lanfei/gotpl"
	}, {
		"name": "playable.js",
		"url": "https://github.com/Lanfei/playable.js"
	}, {
		"name": "webpack-isomorphic",
		"url": "https://github.com/Lanfei/webpack-isomorphic"
	}, {
		"name": "websocket-lib",
		"url": "https://github.com/Lanfei/websocket-lib"
	}, {
		"name": "node-cd-cluster",
		"url": "https://github.com/Lanfei/node-cd-cluster"
	}]
};
var tpl = document.getElementById('tpl').innerHTML;
document.getElementById('list').innerHTML = gotpl.render(tpl, data);
```

### Node

```js
gotpl.config(options);

gotpl.render(template, data, options);

gotpl.renderFileSync(path, data, options);

gotpl.renderFile(path, data, options, (err, html) => {
	// Your codes.
});

await gotpl.renderFile(path, data, options);

// Cache the compiled function
let fn = gotpl.compile(template, options);
fn(data);
```

### Express

```js
app.engine('tpl', template.renderFile);
app.set('view engine', 'tpl');
```

## Options

- `root` The root of template files
- `scope` Rendering context, defaults to `global` in node, `window` in browser
- `debug` Enable debug information output, defaults to `false`
- `cache` Enable caching, defaults to `true`
- `minify` Minify indents, defaults to `true`
- `openTag` Open tag, defaults to `<%`
- `closeTag` Close tag, defaults to `%>`

## Tags

- `<% code %>` Logic code
- `<%= value =>` Output the value as escaped HTML
- `<%- value %>` Output the value as unescaped HTML

## includes

Use `include(path[, data, options])` function to import partial templates, and use `<%- value %>` tag to output:

```ejs
<h1>Projects</h1>
<ul id="list"></ul>

<% if (projects.length) { %>
	<% for (var i = 0, l = projects.length; i < l; ++i) { %>
		<%- include('project', projects[i]) %>
	<% } %>
<% } %>
```

[npm-url]: https://npmjs.org/package/gotpl
[npm-image]: https://badge.fury.io/js/gotpl.svg
