---
title: Concepts
category: Introduction
order: 1
---

Thumbsup generates HTML galleries for existing photos and videos.

**What it does**

- Thumbsup groups photos into albums, based on criteria you define (e.g. per folder)
- It creates HTML pages for every album.
- It generates thumbnails & multiple resolutions for internet-friendly browsing.
- It only rebuilds thumbnails if the source files have changed: it's fast!
- It generates a fully self-contained website, which can be copied onto a USB stick or deployed on a static web server.

**What it doesn't do**

- Thumbsup never changes your input folder. In fact, it doesn't need write access at all.
- It's not a full application / web server, and doesn't have "server side" logic.
- It doesn't have the concept of users, logging-in, etc.

### Albums

Albums are a central concept in Thumbsup.
They are a collection of photos and videos, regardless of where the files are on disk.
When generating the gallery you can specify how albums are created, e.g.

- 1 album per folder and sub-folder
- 1 album per date, e.g. `YYYY` or `YYYY/MM`

For now files can only belong to one album, but in the future a file could
easily be added to several albums.

### Performance

Thumbsup uses a few tricks to generate galleries as quickly as possible:

- it caches all metadata into a local database (`thumbsup.db`) to avoid re-parsing the input files every time
- when reading metadata, it runs several `exiftool` instances in batch mode to process up to 300 photos/sec
- it check file modification dates to only build thumbnails when necessary
- it runs thumbnail generation in parallel to make use of all CPUs

### Standing on the shoulder...

There is no need to re-invent the wheel when dealing with photo and video-processing.
Thumbsup uses well known tools under the hood, like `exiftool`, `graphicsmagick` and `ffmpeg`.
These tools each have more than 13 years of development and troubleshooting, and provide all the capabilities we need.

_Fun fact:_ ImageMagick will soon be 30 years old!
