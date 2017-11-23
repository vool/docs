---
title: Output settings
category: Configuration
order: 2
---

#### \-\-thumb-size

Size of the square thumbnails in pixels. Defaults to `120`.

#### \-\-large-size

Height of the fullscreen photos in pixels. Defaults to `1000`.

#### \-\-download-photos / \-\-download-videos

These settings control the download behaviour, and whether the original photos/videos are copied to the output folder.

| Value	| Behaviour |
|-------|-------------------------|
| `large`	| Download points to the web-friendly large version, which is already generated in the gallery's media folder |
| `copy`  |	Copies all original files into the output media folder, and points the downloads to them. This significantly increases the size of the gallery, but allows the gallery to be self-contained |
| `symlink`	| Creates symlinks to the originals in the output folder. This can be useful for galleries made for local browsing |
| `link`  |	Points the downloads to another (existing) location, which can be local or remote. Use the `--download-link-prefix` option to configure the links, e.g. `../..` or [https://myfiles.com/originals](#) |

For example, given a photo called `MyAlbum/IMG_0001.jpg`:

```bash
--download-photos large
# points download link to "large/MyAlbum/IMG_0001.jpg"

--download-photos copy
# points download link to "originals/MyAlbum/IMG_0001.jpg" (which is created as part of the build)

--download-photos symlink
# points download link to "originals/MyAlbum/IMG_0001.jpg" (which is a symlink to the input photo)

--download-photos link
# by default, will use a relative link to the input folder, relative to the output folder
# the path prefix also be overridden using the --download-link-prefix option
```

#### \-\-download-link-prefix

This settings controls the download links when `--download-*` is set to `link`.
The default value is the relative path from the output folder to the input folder.
For example:

```bash
thumbsup --input /docs/photos --output /docs/website --download-photos link
# given a photo called holidays/IMG_0001.jpg
# the download link will points to ../photos/holidays/IMG_0001.jpg
```

This can be overridden with any relative or absolute path, or a URL. For example:

```bash
--download-photos link --download-link-prefix "../../"
# points download link to "../../holidays/IMG_0001.jpg" (which is assumed to already exist)

--download-photos link --download-link-prefix "https://static.mygallery.com/originals/"
# points download link to "https://static.mygallery.com/originals/holidays/IMG_0001.jpg" (which is assumed to already exist)
```

#### \-\-cleanup

When enabled (`--cleanup true`) this will generate the website as usual,
but also delete any **output** media files that are no longer referenced.

For example if you delete a photo from the **input** folder,
it will automatically delete the corresponding thumbnail since no album refers to it anymore.

*Note:* this never deletes any files from the input folder itself.
