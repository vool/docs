---
title: Album settings
category: Configuration
order: 3
---

> \-\-albums-from

If you choose `folders`, the album structure will exactly mirror the folder structure on disk.
If you choose `date`, files will be grouped into albums based on their date - regardless of where they are on disk.

> \-\-albums-date-format

This is only relevant if you chose `--album-from date`, and determines how albums are named.
It can be any valid [moment.js](http://momentjs.com/) date format. The format can contain
the `/` character to create nested albums. Some valid examples are:

- `YYYY MMMM` for a top-level `2016 October` album
- `YYYY/MM` for a top-level `2016` album, with a nested album called `10`
- `YYYY/YYYY MMMM` for a top-level `2016` album, with a nested album called `2016 October`

<div class="warning">
The date of a file is always the date is was taken, if available in the <code>EXIF</code> data.
If there is no EXIF data, it defaults to the file's <code>mtime</code>,
which you can change with many tools - including Unix's <code>touch</code> command.
</div><br />

> \-\-sort-albums-by

How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]

> \-\-sort-albums-direction

Album sorting direction  [choices: "asc", "desc"] [default: "asc"]

> \-\-sort-media-by

How to sort photos and videos  [choices: "filename", "date"] [default: "date"]

> \-\-sort-media-direction

Media sorting direction  [choices: "asc", "desc"] [default: "asc"]
