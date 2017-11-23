---
title: Creating a theme
category: Themes
order: 3
---

A theme is simply a folder following a given structure.

```bash
theme
  |__ album.hbs    # main view
  |__ style.less   # stylesheets
  |__ partials     # optional partial templates
  |__ helpers      # optional JS helpers
```

It can be loaded using:

```
—theme file://path/to/theme
```

Note that loading a theme from disk will not download any extra code or install dependencies for you.
All dependencies should already have been setup separately if needed (e.g. `npm install`).

To submit a theme to be built-in, please [raise an issue on Github here](https://github.com/thumbsup/thumbsup).

### album.hbs

This template will be called once with the root album.
It should call itself recursively if there are any nested albums to process.
See below for the data that's available to render.

```hbs
{% raw %}<h1>{{title}}</h1>

<h2>Nested albums</h2>
{{#each album}}
  {{>album .}}
{{/each}}

<h2>Photos and videos</h2>
{{#each files}}
  {{filename}}
{{/each}}{% endraw %}
```

### styles.less

This is the entry point for any custom styles.
You can split your styles into multiple files using `@import "other.less";`.

```less
h1 {
  color: #2070ee;
}
```

### partials

Thumbsup automatically loads any `.hbs` partials in the `partials` folder.
These are available in your view as `{% raw %}{{>filename}}{% endraw %}`.
You can pass data to a partial using the `{% raw %}{{>filename arg1, arg2}}{% endraw %}` syntax.

```bash
theme/partials
  |__ caption.hbs
```

```hbs
{% raw %}<!-- summary.hbs -->
<div>Photo caption</div>
```

```hbs
<!-- album.hbs -->
{{> caption}}{% endraw %}
```

### helpers

Thumbsup automatically loads JavaScript helpers from the `helpers` folder.
Each helper is available in the views using `{% raw %}{{#filename}}{% endraw %}`.
You can pass data to a helper using the `{% raw %}{{#filename arg1, arg2}}{% endraw %}` syntax.

```bash
theme/helpers
  |__ hello.js
```

```js
// hello.js
module.exports = (name) => {
  return `hello ${name}`
}
```

```hbs
{% raw %}<!-- album.hbs -->
<div>
  {{#hello world}}
</div>{% endraw %}
```

## Data model

TODO
