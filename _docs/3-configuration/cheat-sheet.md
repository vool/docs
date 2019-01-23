---
title: Cheat sheet
category: Configuration
order: 2
---

Here are all the CLI arguments currently supported by thumbsup:

```
Input options:
  --include             Glob pattern of files to include  [array]
  --exclude             Glob pattern of files to exclude  [array]
  --include-photos      Include photos in the gallery  [boolean] [default: true]
  --include-videos      Include videos in the gallery  [boolean] [default: true]
  --include-raw-photos  Include raw photos in the gallery  [boolean] [default: false]

Output options:
  --thumb-size            Pixel size of the square thumbnails  [number] [default: 120]
  --large-size            Pixel height of the fullscreen photos  [number] [default: 1000]
  --photo-quality         Quality of the resized/converted photos  [number] [default: 90]
  --video-quality         Quality of the converted video (percent)  [number] [default: 75]
  --video-bitrate         Bitrate of the converted videos (e.g. 120k)  [string] [default: null]
  --video-format          Video output format  [choices: "mp4", "webm"] [default: "mp4"]
  --download-photos       Target of the photo download links  [choices: "large", "copy", "symlink", "link"] [default: "large"]
  --download-videos       Target of the video download links  [choices: "large", "copy", "symlink", "link"] [default: "large"]
  --download-link-prefix  Path or URL prefix for linked downloads  [string]
  --cleanup               Remove any output file that's no longer needed  [boolean] [default: false]
  --concurrency           Number of parallel parsing/processing operations  [number] [default: 4]
  --gm-args               Custom image processing arguments for GraphicsMagick  [array]
  --watermark             Path to a transparent PNG to be overlaid on all images  [string]
  --watermark-position    Position of the watermark  [choices: "Repeat", "Center", "NorthWest", "North", "NorthEast", "West", "East", "SouthWest", "South", "SouthEast"]

Album options:
  --albums-from            How files are grouped into albums  [array] [default: ["%path"]]
  --sort-albums-by         How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]
  --sort-albums-direction  Album sorting direction  [choices: "asc", "desc"] [default: "asc"]
  --sort-media-by          How to sort photos and videos  [choices: "filename", "date"] [default: "date"]
  --sort-media-direction   Media sorting direction  [choices: "asc", "desc"] [default: "asc"]

Website options:
  --index                 Filename of the home page  [default: "index.html"]
  --albums-output-folder  Output subfolder for HTML albums (default: website root)  [default: "."]
  --theme                 Name of a built-in gallery theme  [choices: "classic", "cards", "mosaic"] [default: "classic"]
  --theme-path            Path to a custom theme  [string]
  --theme-style           Path to a custom LESS/CSS file for additional styles  [string]
  --title                 Website title  [default: "Photo album"]
  --footer                Text or HTML footer  [default: null]
  --google-analytics      Code for Google Analytics tracking  [string]
  --embed-exif            Embed the exif metadata for each image into the gallery page  [boolean] [default: false]

Misc options:
  --config       JSON config file (one key per argument)  [string]
  --log          Print a detailed text log  [choices: null, "info", "debug", "trace"] [default: null]
  --usage-stats  Enable anonymous usage statistics  [boolean] [default: true]
  --dry-run      Update the index, but don't create the media files / website  [boolean] [default: false]

Deprecated:
  --original-photos     Copy and allow download of full-size photos  [boolean] [default: false]
  --original-videos     Copy and allow download of full-size videos  [boolean] [default: false]
  --albums-date-format  How albums are named in <date> mode [moment.js pattern]  [default: "YYYY-MM"]
  --css                 Path to a custom provided CSS/LESS file for styling  [string]

Options:
  --version  Show version number  [boolean]
  --help     Show help  [boolean]
```
{: .nowrap }
