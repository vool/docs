---
title: Choosing a theme
category: Themes
order: 1
---

Themes change the final style and layout of the galleries.
They don't impact thumbnail generation, so you can change theme as often as you want within seconds!

```bash
# load one of the built-in themes
--theme <name>

# load an external theme
—-theme-path path/to/theme

# add additional styles
--theme-style custom.less
```

You can look at [built-in themes](../built-in/) or maybe [create your own](../create/).

### Customising themes

Themes often expose configuration options such as the background color.
These options should be documented in the theme's documentation.
Simply use `--theme-style <path>` to override any variable, and make the theme your own!

```less
// Overriding theme variables is an easy way to customize a theme.
// Theme variables are well supported and should be stable within a theme.
@theme-variable: 'new value';

// You can also override any other elements.
// Your styles will be applied on top of the existing theme styles.
// However the name of CSS classes or IDs might change with new theme versions.
.other-custom-item {
  color: red;
}
```
