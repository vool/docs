---
title: Basic usage
category: Configuration
order: 1
---

All `thumbsup` configuration is done passing command-line arguments.

### Command line arguments

The following arguments are required:

```bash
--input <path>   # Path to the folder with all photos/videos  [string] [required]
--output <path>  # Output path for the static website  [string] [required]
```
{: .nowrap }

And you can optionally specify:

```bash
Output options:
  --thumb-size            # Pixel size of the square thumbnails  [number] [default: 120]
  --large-size            # Pixel height of the fullscreen photos  [number] [default: 1000]
  --download-photos       # What the download link points to for photos  [large,copy,symlink,link] [default: large]
  --download-videos       # What the download link points to for videos  [large,copy,symlink,link] [default: large]
  --download-link-prefix  # Relative or absolute prefix if downloads are set to "link"  [string]
  --cleanup               # Remove any output file that's no longer needed  [boolean] [default: false]

Album options:
  --albums-from            # How to group media into albums  [choices: "folders", "date"] [default: "folders"]
  --albums-date-format     # How albums are named in <date> mode [moment.js pattern]  [default: "YYYY-MM"]
  --sort-albums-by         # How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]
  --sort-albums-direction  # Album sorting direction  [choices: "asc", "desc"] [default: "asc"]
  --sort-media-by          # How to sort photos and videos  [choices: "filename", "date"] [default: "date"]
  --sort-media-direction   # Media sorting direction  [choices: "asc", "desc"] [default: "asc"]

Website options:
  --index                 # Filename of the home page  [default: "index.html"]
  --albums-output-folder  # Output subfolder for HTML albums (default: website root)  [default: "."]
  --theme                 # Name of the gallery theme to apply  [choices: "classic", "cards", "mosaic"] [default: "classic"]
  --title                 # Website title  [default: "Photo album"]
  --footer                # Text or HTML footer  [default: null]
  --css                   # Path to a custom provided CSS/LESS file for styling  [string]
  --google-analytics      # Code for Google Analytics tracking  [string]

Misc
  --config                # Load the configuration from a JSON file
  --log                   # Configure the logging verbosity
  --usage-stats           # Enable or disable anonymous usage stats
```
{: .nowrap }

For example it can be as simple as

```bash
thumbsup --input "/media/photos" --output "./website"
```

or as complex as

```bash
thumbsup --input "/media/photos" --output "./website" --title "My holidays" --thumb-size 200 --large-size 1500 --original-photos true --original-videos false --albums-from date --albums-date-format 'YYYY/MMM' --sort-albums-by date --theme cards --css "./custom.css" --google-analytics "UA-999999-9"
```

All relative paths are relative to the current working directory.

### JSON configuration

Maintaining many arguments can become tedious.
You might also want to save them somewhere and re-use them easily.
To help with this `thumbsup` also supports passing arguments as a `JSON` file:

```bash
thumbsup --config config.json
```

Simply specify all arguments as an object, without the `--` prefix:

```json
{
  "input": "/media/output",
  "output": "./website",
  "title": "My holiday",
  "thumb-size": 200,
  "large-size": 1500,
  "download-photos": "copy",
  "download-videos": "large",
  "sort-albums-by": "date",
  "theme": "cards",
  "css": "./custom.css",
  "google-analytics": "UA-999999-9"
}
```

### Usage statistics

By default, thumbsup reports anonymous usage stats such as the OS and the gallery size.
This is used to understand usage patterns and guide development effort, for example
"should we focus on Windows support" or "should we make optimizations for galleries of 10,000+ photos".

You can disable usage reporting by specifying `--no-usage-stats`.
When using a JSON config file you can set

```json
{
  "usage-stats": false
}
```

Rest assured that thumbsup will never report any personal data such as filenames,
album names or EXIF metadata. You can of course check the source code at
[https://github.com/thumbsup/thumbsup](https://github.com/thumbsup/thumbsup).

---
