---
title: Album settings
category: Configuration
order: 3
---

> \-\-albums-from

As detailed in the [intro section](../../1-introduction/concepts), albums are a virtual concept in thumbsup.
Files can belong to arbitrary albums regardless of where they are on disk.
This setting determines how the photos and videos are grouped into albums.

The simplest value is a raw string where `/` denotes a hierarchy of albums. For example,
`--albums-from "Holidays/Tokyo"` specifies that all files should go in an album called `Tokyo`,
inside an album called `Holidays`.
A more typical use case is to use keywords to generate albums on the fly based on the photos being processed.

##### Folders

The value `%path` automatically expands to the nested folder structure, relative to the input folder.
For example:

| File path | Pattern | Value |
|-----------|---------|-------|
| `Holidays/Tokyo/IMG_0001.jpg` | `%path` | `Holidays/Tokyo` |
| `Tokyo/IMG_0001.jpg` | `Holidays/%path` | `Holidays/Tokyo` |

##### Date

The value `{format}` automatically expands to the date the photo/video was taken.
The format must be a valid [moment.js format](https://momentjs.com/docs/#/displaying/format/).

| File date | Pattern | Value |
|-----------|---------|-------|
| `2017-10-21` | `{YYYY}` | `2017` |
| `2017-10-21` | `{YYYY/MM}` | `2017/10` |
| `2017-10-21` | `{YYYY}/{MM - MMM}` | `2017/10 - October` |
| `2017-10-21` | `Years/{YYYY}/{MM}` | `Years/2017/10` |

This always uses the creation date if available in the <code>EXIF</code> data.
If there is no EXIF data, it defaults to the file's <code>mtime</code>.
You can change `mtime` with many tools such as Unix's <code>touch</code> command.

##### Keywords

The value `%keywords` expands to every ITPC keyword present in the photo.
For example, if a photo is tagged with `sunset` and `beach`:

| Keywords | Pattern | Albums |
|-----------|---------|-------|
| `sunset`, `beach` | `%keywords` | `sunset`, `beach` |
| `sunset`, `beach` | `Tags/%keywords` | `Tags/sunset`, `Tags/beach` |


##### Multiple albums

A file can belong to zero, one or many albums.
One the command line, simply specify the flag multiple times:

```bash
thumbsup --albums-from "Folders/%path" --albums-from "Years/{YYYY}"
```

If using a config file, specify the patterns as an array:

```json
{
  "albums-from": ["Folders/%path", "Years/{YYYY}"]
}
```


> \-\-sort-albums-by

How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]

> \-\-sort-albums-direction

Album sorting direction  [choices: "asc", "desc"] [default: "asc"]

> \-\-sort-media-by

How to sort photos and videos  [choices: "filename", "date"] [default: "date"]

> \-\-sort-media-direction

Media sorting direction  [choices: "asc", "desc"] [default: "asc"]
