---
title: Input settings
category: Configuration
order: 2
---

The following flag determines whether certain types of files are indexed by thumbsup, and added to the gallery.

> \-\-include-photos

Boolean, whether to include standard photo files (jpg, png...).

> \-\-include-videos

Boolean, whether to include standard video files (mp4, mov...).

> \-\-include-raw-photos

Boolean, whether to include camera RAW files (Nikon NEF, Canon CR2...).
Just like other photos, RAW files are processed to generate thumbnails and a web-friendly preview.
Processing RAW files requires [dcraw](https://www.cybercom.net/~dcoffin/dcraw/) to be installed.
