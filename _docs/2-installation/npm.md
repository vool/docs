---
title: npm package
category: Installation
order: 2
---

Simply install [thumbsup](https://www.npmjs.com/package/thumbsup) globally from the registry:

```bash
npm install -g thumbsup
```

### Additional requirements

The following tools need to be installed, with binaries in your system path:

- [Node.js](http://nodejs.org/)
- [Exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)
- [GraphicsMagick](http://www.graphicsmagick.org/)
- [FFmpeg](http://www.ffmpeg.org/)

On macOS:

```bash
brew install node
brew install exiftool
brew install graphicsmagick
brew install ffmpeg
```

<div class="warning">
  Note: there currently is <a href="https://github.com/thumbsup/thumbsup/issues/27">an issue with Ubuntu 14.04</a>
  if you build <code>ffmpeg</code> from source. Please upgrade to 14.10 and install it with <code>apt-get</code>.
</div>

### Creating a basic gallery

```bash
thumbsup --input ~/photos --output ~/gallery
```

For more details about all the arguments and options available, see the [configuration](../../3-configuration/usage) page.
