---
title: npm package
category: Installation
order: 2
---

Simply install [thumbsup](https://www.npmjs.com/package/thumbsup) globally from the registry:

```bash
npm install -g thumbsup
```

The following tools also need to be installed, with binaries in your system path:

- [Node.js](http://nodejs.org/)
- [Exiftool](http://www.sno.phy.queensu.ca/~phil/exiftool/)
- [GraphicsMagick](http://www.graphicsmagick.org/)

And optionally:

- [FFmpeg](http://www.ffmpeg.org/) to process videos
- [Gifsicle](http://www.lcdf.org/gifsicle/) to process animated GIFs

You can verify that `thumbsup` was installed correctly by running:

```bash
thumbsup --help
```

For more details about all the arguments and options available, see the [configuration](../../3-configuration/usage) page.

### Installation notes

Installing `thumbsup` should be straightfoward.
Here are some notes and workarounds that have been reported by users.

#### MacOS

You can install all the extra dependencies using [Homebrew](https://brew.sh/):

```bash
brew install node
brew install exiftool
brew install graphicsmagick
brew install ffmpeg
brew install gifsicle
```

#### Ubuntu

There currently is <a href="https://github.com/thumbsup/thumbsup/issues/27">an issue with Ubuntu 14.04</a>
if you build <code>ffmpeg</code> from source. Please upgrade to 14.10 and install it with <code>apt-get</code>.

#### Debian

You might have to manually install `cmake` and `g++` to compile the thumbup's binary dependencies.

You could also run into issues because the available version of Node.js is too old.
You can install Node 10 using:

```bash
sudo apt install curl software-properties-common
curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
sudo apt install nodejs
```

If you had already installed thumbsup, you might need to rebuild its binary components:

```bash
cd /usr/lib/node_modules/thumbsup && npm rebuild --unsafe-perm
```

#### Raspberry PI

If installing thumbsup on a Raspberry Pi, you must provide an extra environment variable:

```bash
LZZ_COMPAT=1 npm install -g thumbsup
```
