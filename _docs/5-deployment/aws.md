---
title: AWS
category: Deployment
order: 2
---

The simplest way to deploy a `thumbsup` gallery on the internet is to sync
the output folder to Amazon S3 using the [AWS CLI](http://aws.amazon.com/cli/).

```bash
aws s3 sync ./generated/website s3://mybucket --delete
```

You can also use [s3cmd](http://s3tools.org/) which offer a few more options.

```bash
s3cmd sync --config=<credentials> --delete-removed --exclude-from <exclude-file> ./generated/website/ s3://mybucket/
```

Simply enable *website hosting* on S3, and navigate to https://mybucket.s3-website-us-east-1.amazonaws.com.
You can also use a custom domain name, as long as your bucket name matches your domain exactly, e.g. `s3://website.com`.
Then create a `CNAME` record pointing to the S3 website domain:

```
CNAME website.com.s3-website-us-east-1.amazonaws.com
```
