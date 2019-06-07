---
title: Basic usage
category: Configuration
order: 1
---

All `thumbsup` configuration is done passing command-line arguments, or a [JSON config file](../misc-settings).
This can be as simple as:

```bash
thumbsup --input "/media/photos" --output "./website"
```

or as complex as

```bash
thumbsup --input "/media/photos" --output "./website" --title "My holidays" --thumb-size 200 --large-size 1500 --original-photos true --original-videos false --albums-from "{YYYY/MM}" --sort-albums-by date --theme cards --theme-style "./custom.less" --google-analytics "UA-999999-9"
```

See the [cheat sheet](../cheat-sheet) for a list of all possible settings, or dive into these sections for details about every single option:
- [Input settings](../input-settings)
- [Output settings](../output-settings)
- [Album settings](../album-settings)
- [Website settings](../website-settings)
- [Misc settings](../misc-settings)

*Note:* all relative paths are relative to the current working directory.
