---
title: Input settings
category: Configuration
order: 3
---

> \-\-include &lt;glob&gt;

By default, all files in the `--input` folder are added to the gallery.
This optional pattern controls which files to include instead.

- It must be a valid *glob* pattern such as `**/IMG_*`
- When targeting a folder name, make sure it's followed by stars, such as `holidays/**`
- If specified multiple times, files matching **any** of the patterns will be included
- This does not change the kind of extensions that are supported (`**/*.doc` will not include Word documents)

When using a JSON config file, make sure that this value is an array, such as

```json
{
  "include": ["**/IMG_*"]
}
```

> \-\-exclude &lt;glob&gt;

This optional pattern controls which files to exclude from the input folder.
Exclusions are applied after inclusions.

- It must be a valid *glob* pattern such as `**/IMG_*` or `**/work/**`
- When excluding a directory, make sure to use `folder/` or `folder/**` (not just the name)
- Some folders are always excluded by default, such as
  - any folder starting with a dot
  - Synology vendor folders (thumbnails, recycle bin)

When using a JSON config file, make sure that this value is an array, such as

```json
{
  "exclude": ["**/IMG_*"]
}
```

> \-\-include-photos &lt;boolean&gt;

Whether to index / process / display standard photo files (jpg, png...).
Notes:
- if set to `false`, the corresponding file types will be ignored regardless of any `--include` patterns
- if set to `true`, it doesn't bring back any files that were ignored using `--include/exclude`

> \-\-include-videos &lt;boolean&gt;

Whether to index / process / display standard video files (mp4, mov...).

> \-\-include-raw-photos &lt;boolean&gt;

Whether to index / process / display camera RAW files (Nikon NEF, Canon CR2...).
Just like other photos, RAW files are processed to generate thumbnails and a web-friendly preview.
Processing RAW files requires [dcraw](https://www.cybercom.net/~dcoffin/dcraw/) to be installed.


> \-\-scan-mode &lt;full,partial,incremental&gt;

These 3 modes control what happens between multiple runs of Thumbsup, specifically:
- when a file has been deleted since the last run
- when a file is not part of the latest scan because of changing `--include` or `--exclude` patterns

|  | Full | Partial | Incremental |
|--|------|---------|-------------|
| File outside the include pattern | Remove | Keep | Keep |
| File deleted from disk (inside the pattern) | Remove | Remove | Keep |

A common use-case for `partial` is to avoid re-scanning folders that never change, but keeping their content in the gallery.
A common use-case for `incremental` is to always *append* content to an existing gallery, even when the source data no longer exists.

Consider this folder structure:

```bash
2022/IMG_001.jpg
2023/IMG_002.jpg
2023/IMG_003.jpg
```

```bash
# Index all photos
thumbsup --input /photos

# Delete a file
rm 2023/IMG_002.jpg

# Rerun scoping to 2023
thumbsup --input /photos --include '2023/**' --scan-mode 'SEE BELOW'
```

|  | Full | Partial | Incremental |
|--|---------|---------|---------|
| IMG_001 | removed because it's outside the include pattern | kept because it's outside the include pattern | kept |
| IMG_002 | removed because it was deleted on disk | removed because it was deleted on disk | kept |
| IMG_003 | kept | kept | kept |

**Careful!**

The flags `--include-photos / videos / raw-photos` are applied regardless of the scan mode.
For example if your gallery has existing videos and you set `--include-videos false`:

- In `full` mode: all videos will be removed from the gallery.
- In `partial` any video matching the include pattern will be removed from the gallery.
- In `incremental` mode: all videos will be kept in the gallery, since this mode never removes content.
