---
title: AWS
category: Deployment
order: 2
---

The simplest way to deploy a `thumbsup` gallery on the internet is to sync
the output folder to Amazon S3 using the [AWS CLI](http://aws.amazon.com/cli/).

```bash
aws s3 sync ./generated/website s3://my.website.bucket --delete
```

You can also use [s3cmd](http://s3tools.org/) which offer a few more options.

```bash
s3cmd sync --config=<credentials> --delete-removed --exclude-from <exclude-file> ./generated/website/ s3://my.website.bucket/
```

Simply enable *website hosting* on S3, and point your user-facing domain to S3 website URL. For example:

```
CNAME mybucket.s3-website-us-east-1.amazonaws.com
```
