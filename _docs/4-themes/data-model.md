---
title: Data model
category: Themes
order: 4
---

The [templating engine](https://handlebarsjs.com) is called for each album in the gallery, with the following data:

```js
{
  album: Album,
  gallery: Gallery,
  breadcrumbs: [String]
}
```

Here are the main classes used in the model.

#### Gallery

```js
{
  home: Album,
  title: String,
  footer: String,
  thumbSize: Number,
  largeSize: Number,
  googleAnalytics: String
}
```

#### Album

```js
{
  title: String,
  home: Boolean,
  depth: Number,
  zip: String,
  albums: [Album],
  files: [File],
  stats: {
    albums: Number,
    photos: Number,
    videos: Number,
    fromDate: Date,
    toDate: Date
  }
}
```

#### File

```js
{
  id: Number,
  path: String,
  filename: String,
  date: Date,
  type: 'Video|Image',
  isVideo: Boolean,
  meta: Metadata,
  urls: {
    thumbnail: String,
    small: String,
    large: String,
    video: String,
    download: String
  }
}
```

#### Metadata

```js
{
  date: Date,
  caption: String,
  keywords: [String],
  video: Boolean,
  animated: Boolean,
  rating: Number,
  favourite: Boolean,
  width: Number,
  height: Number,
  exif: Object
}
```
