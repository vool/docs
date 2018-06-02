---
title: Creating a theme
category: Themes
order: 3
---

> Coming soon. Custom themes will be available in the next version of `thumbsup`.

---

A theme is simply a folder following a given structure.

```bash
theme
  |__ album.hbs    # main view
  |__ theme.less   # stylesheets
  |__ partials     # optional partial templates
  |__ helpers      # optional JS helpers
```

It can be loaded using:

```
--theme-path file://path/to/theme
```

Note that loading a theme from disk will not download any extra code or install dependencies for you.
All dependencies should already have been setup separately if needed (e.g. `npm install`).

To submit a theme to be built-in, please [raise an issue on Github here](https://github.com/thumbsup/thumbsup).

### album.hbs

This template will be called for every album in the gallery, including the root album.
It should typically render thumbnails for every entry in the album, as well as links to nested albums if applicable.

```hbs
{% raw %}{{#with album}}
  <h1>{{title}}</h1>

  <h2>Nested albums</h2>
  {{#each albums}}
    <a href="{{relative url}}">{{title}}</a>
  {{/each}}

  <h2>Photos and videos</h2>
  {{#each files}}
    <a href="{{relative urls.large}}">{{filename}}</a>
  {{/each}}

{{#endwith}}{% endraw %}
```

The data available to render is described on the [data-model page](../data-model/).
It's also a good idea to read the [thumbsup source-code](https://github.com/thumbsup/thumbsup) to get familiar with any subtleties.

### theme.less

This is the entry point for all your theme's styles.

```less
h1 {
  color: #2070ee;
}
```

Some notes:

- You can split your styles into multiple files using `@import "other.less";`
- The generated CSS file is placed in the `public` folder (important for relative paths)

To make your theme configurable, you should use LESS variables for key elements like colors or sizes.
For example:

```less
@highlight: #17baef;

h1 {
  color: @highlight;
}
```

This will allow users to specify their own highlight color using:

```bash
thumbsup --theme-path ./your-theme --theme-style custom.less
```

```less
// custom.less
@highlight: #ed124d;
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
{% raw %}<!-- caption.hbs -->
<div>Photo caption</div>
```

```hbs
<!-- album.hbs -->
{{> caption}}{% endraw %}
```

### helpers

Thumbsup automatically loads JavaScript helpers from the `helpers` folder.
Each helper is available in the views using `{% raw %}{{name}}{% endraw %}`
for inline helpers, or `{% raw %}{{#name}}{% endraw %}` for block helpers.
You can pass data to a helper using the `{% raw %}{{name arg1, arg2}}{% endraw %}` syntax.

```bash
theme/helpers
  |__ hello.js
```

```js
// hello.js
module.exports = handlebars => {
  handlebars.registerHelper('hello', name => {
    return `hello ${name}`
  })
}
```

```hbs
{% raw %}<!-- album.hbs -->
<div>
  {{hello world}}
</div>{% endraw %}
```

### public

Every theme typically depends on extra static assets such as JavaScript files or images. The content of the `public` folder is copied as-is to the final gallery, on top of defaults assets bundled by thumbsup.

```bash
myTheme
  |__ album.hbs
  |__ public
     |__ cool.js
     |__ dragon.jpg
```
