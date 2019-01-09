---
title: Password protection
category: Deployment
order: 3
---

If you want to protect your galleries, you can

- deploy your website behind a web server like `Nginx` or `Apache` and configure basic authentication.
- deploy the galleries behind hard-to-guess URLs, like Dropbox shared galleries. The main upside / downside is that anyone with the link can access the gallery.
- deploy to AWS S3 and add an authentication layer, as below.

### Private galleries on AWS

AWS S3 itself does not support authentication.
However, you can build a fully self-hosted private gallery using [S3](https://aws.amazon.com/s3/) + [CloudFront](https://aws.amazon.com/cloudfront/) + [Cognito](https://aws.amazon.com/cognito/) + [Lambda](https://aws.amazon.com/lambda/).

The main benefits of this setup are:

- cheaper and faster than a public S3 bucket, as all photos are cached and served at the edge
- scales to very large number of users, who can sign-up and reset their own passwords
- easily configurable to support Google/Facebook single-sign-on

A full walk-through is available at [github.com/thumbsup/aws-private-gallery](https://github.com/thumbsup/aws-private-gallery).
This should only take about 1 hour to setup, given you have some AWS knowledge and are comfortable with the command-line.
