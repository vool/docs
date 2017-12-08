---
title: Password protection
category: Deployment
order: 3
---

If you want to protect your galleries, you can

- deploy your website behind a web server like `Nginx` or `Apache` and configure basic authentication
- deploy the galleries to UUID-based locations, like Dropbox shared galleries
- deploy to S3 with [CloudFront with signed cookies](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html)

### CloudFront signed cookies

AWS S3 does not support authentication itself. However you can front S3 with the CloudFront CDN,
which supports authentication through cookies. The two main steps are

**Step 1: serve your gallery through CloudFront**

- configure CloudFront, preferably using HTTPS, using an origin of `mybucket.s3.amazonaws.com`
- you can disable website hosting on the bucket, which is not needed anymore
- repoint your user-facing domain to the CloudFront endpoint instead of S3, e.g. [https://00000000.cloudfront.net](#)
- remove public access from the Bucket in the "permissions" section
- grant CloudFront access using the following *Bucket Policy*

```json
{
  "Version":"2012-10-17",
  "Id":"PolicyForCloudFrontPrivateContent",
  "Statement":[
    {
      "Sid":" Grant CloudFront access to all objects",
      "Effect":"Allow",
      "Principal":{
        "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity 0000000000000"
      },
      "Action":"s3:GetObject",
      "Resource":"arn:aws:s3:::website.com/*"
    },
    {
      "Sid": "Grant access to list objects, so S3 can return 404 instead of 403",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity 0000000000000"
      },
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::website.com"
    }
  ]
}
```

At this point you should have a working gallery going through CloudFront, with the added benefit of caching! Serving the gallery from CloudFront is both much faster and less expensive than serving it from S3 (e.g. data transfer costs).

**Step 2: adding authentication**

- setup a new Lambda function using [lambda-cloudfront-cookies](https://github.com/thumbsup/lambda-cloudfront-cookies). Its job is to create authentication cookies when presented with valid credentials
- add a login page to the S3 bucket that contains your galleries, e.g. `s3://website.com/login.html`. You can find a nice-looking template at [thumbsup/html-pages](https://github.com/thumbsup/html-pages)
- setup CloudFront to require auth cookies for all pages
- setup CloudFront to render the login page on `403` errors. This is why the `s3:ListBucket` permission is important, otherwise CloudFront will render the login page for broken links too
- update the login page `<form action="....">` to point to the Lambda API endpoint
