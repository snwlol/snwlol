---
layout: post
title: "Razer Cloud Bucket Takeover"
author: "ron"
tags: ["web"]
---

## Summary
There was potential for some Razer product collateral to be leaked, so Razer secured this bucket out of caution.

## Proof of Concept
### Google Dorks
[Google Dorking](https://en.wikipedia.org/wiki/Google_hacking), also known as Google Hacking, was used to reveal insecure permissions on the S3 bucket.

I used the following payload:

{% highlight markdown %}
site:s3.amazonaws.com <target>

{% endhighlight %}


![](https://i.imgur.com/eN3wyTW.png)


S3 bucket URL: https://razer-assets2.s3.amazonaws.com

Bucket name found, **razer-assets2**

### Listing content
Let's see the content using `ls` command.

{% highlight markdown %}
~ > aws s3 ls s3://razer-assets2
                           PRE _ui/
                           PRE archives/
                           PRE css/
                           PRE eedownloads/
                           PRE html/
                           PRE images/
                           PRE js/
                           PRE json/
                           PRE mockups/
                           PRE p.templates/
                           PRE pages/
                           PRE products/
                           PRE videos/
2016-03-29 14:29:08          0 1.txt
2016-03-29 14:31:12          6 common.js
2016-03-29 14:29:56          0 common2.js
2016-03-29 08:45:10          8 lol.txt

{% endhighlight %}

## Report ID
https://hackerone.com/reports/710319
