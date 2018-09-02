---
title: Output settings
category: Configuration
order: 2
---

> \-\-thumb-size

Size of the square thumbnails in pixels. Defaults to `120`.

> \-\-large-size

Height of the fullscreen photos in pixels. Defaults to `1000`.

> \-\-photo-quality

Quality of the resized images, from `0` to `100`.

> \-\-download-photos / \-\-download-videos

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

> \-\-download-link-prefix

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

> \-\-cleanup

When enabled (`--cleanup true`) this will generate the website as usual,
but also delete any **output** media files that are no longer referenced.

For example if you delete a photo from the **input** folder,
it will automatically delete the corresponding thumbnail since no album refers to it anymore.

*Note:* this never deletes any files from the input folder itself.

> \-\-concurrency

This controls the number of photos and videos processed in parallel.
The default value is the number of CPU cores on the current machine.
It might make the machine / server less responsive, in which case you can specify a fixed number:

```bash
--concurrency 2
# process a maximum of 2 photos/videos in parallel
```

*Note:* This corresponds to the maximum number of `exiftool`, `ffmpeg` and `graphicsmagick`
processes that are run at the same time, in addition to the main `Node` process.
There are other limiting factors in terms of performance, such as disk I/O,
so using more cores does not always increase performance.

> \-\-gm-args

Extra command-line arguments to pass to [GraphicsMagick](http://www.graphicsmagick.org/) when processing images.

- `--gm-args` must be specified once per _logical_ option
- each option should be specified as a string, including all relevant arguments

For example:

```bash
# Equalise the image
thumbsup --gm-args 'equalize'

# Add a border around the image
thumbsup --gm-args 'border 5x5'

# Sharpen the image
thumbsup --gm-args 'unsharp 2 0.5 0.7 0'

# Sharpen and add brightness
thumbsup --gm-args 'unsharp 2 0.5 0.7 0' --gm-args 'modulate 120'
```

Note that post-processing will only apply to new images.
As with other options, thumbsups will not regenerate existing images because of a change of flags.

> \-\-watermark

Overlays a watermark on all the resized images. The provided image should be a PNG with transparency.
The watermark does not affect downloadable images if `--download-photos` is set to `copy`, `link` or `symlink`.

```bash
thumbsup --watermark copyright.png
```

> \-\-watermark-position

Defines where the watermark is placed on the image. The possible values are:

- `Repeat`: the watermark is tiled across the entire image
- `Center`: the watermark is placed in the center of the image
- `NorthWest`,`North`,`NorthEast`,`West`,`East`,`SouthWest`,`South`,`SouthEast`: the watermark is positioned along the edges

```bash
thumbsup --watermark copyright.png --watermark-position Repeat
```

![watermark](../../images/watermark.jpg) ![tiled](../../images/watermark-repeat.jpg)
