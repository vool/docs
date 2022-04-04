---
title: Cheat sheet
category: Configuration
order: 2
---

Here are all the CLI arguments currently supported by thumbsup:

<!-- embedme ../../usage.txt -->
```txt


 Usages:
   thumbsup [required] [options]
   thumbsup --config config.json


Required:
  --input   Path to the folder with all photos/videos  [string] [required]
  --output  Output path for the static website  [string] [required]

Input options:
  --include-photos      Include photos in the gallery  [boolean] [default: true]
  --include-videos      Include videos in the gallery  [boolean] [default: true]
  --include-raw-photos  Include raw photos in the gallery  [boolean] [default: false]
  --include             Glob pattern of files to include  [array]
  --exclude             Glob pattern of files to exclude  [array]

Output options:
  --thumb-size          Pixel size of the square thumbnails  [number] [default: 120]
  --small-size          Pixel height of the small photos  [number] [default: 300]
  --large-size          Pixel height of the fullscreen photos  [number] [default: 1000]
  --photo-quality       Quality of the resized/converted photos  [number] [default: 90]
  --video-quality       Quality of the converted video (percent)  [number] [default: 75]
  --video-bitrate       Bitrate of the converted videos (e.g. 120k)  [string] [default: null]
  --video-format        Video output format  [choices: "mp4", "webm"] [default: "mp4"]
  --video-stills        Where the video still frame is taken  [choices: "seek", "middle"] [default: "seek"]
  --video-stills-seek   Number of seconds where the still frame is taken  [number] [default: 1]
  --photo-preview       How lightbox photos are generated  [choices: "resize", "copy", "symlink", "link"] [default: "resize"]
  --video-preview       How lightbox videos are generated  [choices: "resize", "copy", "symlink", "link"] [default: "resize"]
  --photo-download      How downloadable photos are generated  [choices: "resize", "copy", "symlink", "link"] [default: "resize"]
  --video-download      How downloadable videos are generated  [choices: "resize", "copy", "symlink", "link"] [default: "resize"]
  --link-prefix         Path or URL prefix for "linked" photos and videos  [string]
  --cleanup             Remove any output file that's no longer needed  [boolean] [default: false]
  --concurrency         Number of parallel parsing/processing operations  [number] [default: 4]
  --output-structure    File and folder structure for output media  [choices: "folders", "suffix"] [default: "folders"]
  --gm-args             Custom image processing arguments for GraphicsMagick  [array]
  --watermark           Path to a transparent PNG to be overlaid on all images  [string]
  --watermark-position  Position of the watermark  [choices: "Repeat", "Center", "NorthWest", "North", "NorthEast", "West", "East", "SouthWest", "South", "SouthEast"]

Album options:
  --albums-from            How files are grouped into albums  [array] [default: ["%path"]]
  --sort-albums-by         How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]
  --sort-albums-direction  Album sorting direction  [choices: "asc", "desc"] [default: "asc"]
  --sort-media-by          How to sort photos and videos  [choices: "filename", "date"] [default: "date"]
  --sort-media-direction   Media sorting direction  [choices: "asc", "desc"] [default: "asc"]
  --home-album-name        Name of the top-level album  [string] [default: "Home"]
  --album-page-size        Max number of files displayed on a page  [number] [default: null]
  --album-zip-files        Create a ZIP file per album  [boolean] [default: false]
  --include-keywords       Keywords to include in %keywords  [array]
  --exclude-keywords       Keywords to exclude from %keywords  [array]
  --include-people         Names to include in %people  [array]
  --exclude-people         Names to exclude from %people  [array]
  --album-previews         How previews are selected  [choices: "first", "spread", "random"] [default: "first"]

Website options:
  --index                 Filename of the home page  [string] [default: "index.html"]
  --albums-output-folder  Output subfolder for HTML albums (default: website root)  [string] [default: "."]
  --theme                 Name of a built-in gallery theme  [choices: "classic", "cards", "mosaic", "flow"] [default: "classic"]
  --theme-path            Path to a custom theme  [string]
  --theme-style           Path to a custom LESS/CSS file for additional styles  [string]
  --theme-settings        Path to a JSON file with theme settings  [string]
  --title                 Website title  [string] [default: "Photo album"]
  --footer                Text or HTML footer  [string] [default: null]
  --google-analytics      Code for Google Analytics tracking  [string]
  --embed-exif            Embed the exif metadata for each image into the gallery page  [boolean] [default: false]
  --locale                Locale for regional settings like dates  [string] [default: "en"]
  --seo-location          Location where the site will be hosted. If provided, sitemap.xml and robots.txt will be created.  [string] [default: null]

Misc options:
  --config         JSON config file (one key per argument)  [string]
  --database-file  Path to the database file  [string]
  --log-file       Path to the log file  [string]
  --log            Print a detailed text log  [choices: "default", "info", "debug", "trace"] [default: "default"]
  --usage-stats    Enable anonymous usage statistics  [boolean] [default: true]
  --dry-run        Update the index, but don't create the media files / website  [boolean] [default: false]

Deprecated:
  --original-photos       Copy and allow download of full-size photos  [boolean]
  --original-videos       Copy and allow download of full-size videos  [boolean]
  --albums-date-format    How albums are named in <date> mode [moment.js pattern]
  --css                   Path to a custom provided CSS/LESS file for styling  [string]
  --download-photos       Target of the photo download links  [choices: "large", "copy", "symlink", "link"]
  --download-videos       Target of the video download links  [choices: "large", "copy", "symlink", "link"]
  --download-link-prefix  Path or URL prefix for linked downloads  [string]

Options:
  --version  Show version number  [boolean]
  --help     Show help  [boolean]


 The optional JSON config should contain a single object with one key
 per argument, not including the leading "--". For example:
 { "sort-albums-by": "start-date" }

```
{: .nowrap }
