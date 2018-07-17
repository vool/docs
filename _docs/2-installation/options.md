---
title: Options
category: Installation
order: 1
---

### Choosing the right installation

There are 2 main ways to run Thumbsup.
They each have pros and cons, which one you choose depends on your requirements.

**As an npm package**

<table class="comparison">
  <tr>
    <td>Dependencies</td>
    <td>Need to install manually (e.g. exiftool, ffmpeg).</td>
  </tr>
  <tr>
    <td>Codecs</td>
    <td>Uses what's available. Can install extra specific codecs if you need to.</td>
  </tr>
  <tr>
    <td>Performance</td>
    <td>As fast as your computer.</td>
  </tr>
</table>

See the <a href="../../2-installation/npm">npm page</a> for more detail.

**As a Docker container**

<table class="comparison">
  <tr>
    <td>Dependencies</td>
    <td>Everything provided out of the box.</td>
  </tr>
  <tr>
    <td>Codecs</td>
    <td>Most common codecs built-in. <br />You can create a derived image if you want to include new ones.</td>
  </tr>
  <tr>
    <td>Performance</td>
    <td>Up to 50% slower than the npm version.</td>
  </tr>
</table>

See the <a href="../../2-installation/docker">Docker page</a> for more detail.

### Checking your installation

Once installed, you can run thumbsup on a small folder and should expect and output similar to:

```
$ thumbsup --input ./photos --output ./website

✔ Indexing folder
✔ Processing media
✔ Creating website

Gallery generated successfully
3 albums, 70 photos, 5 videos
```

If you receive any errors please use the `--log` argument to troubleshot the issue, as shown in the [troubleshooting](../../3-configuration/troubleshooting) page.
