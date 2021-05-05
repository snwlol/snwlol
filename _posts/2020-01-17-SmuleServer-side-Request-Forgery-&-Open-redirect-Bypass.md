---
layout: post
title: "Smule SSRF + Open Redirect bypass"
author: "ron"
tags: ["web"]
---

## Summary

`redirection_url=` parameter at `https://www.smule.com/user/login?redirection_url=` was vulnerable to Open redirect & SSRF attacks.

## Proof of Concept

### Open redirect

The usual method `?redirect=http://evil.com` didn't work so I found an another bypass. This bypass payload worked: **///google.com**

{% highlight markdown %}
https://www.smule.com/user/login?redirection_url=////google.com

{% endhighlight %}

### SSRF

Now, I started a listener at port 1337 and inserted payload at the vulnerable parameter:

{% highlight markdown %}
https://www.smule.com/user/login?redirection_url=////127.0.0.1:1337

{% endhighlight %}

## Report ID
https://hackerone.com/reports/771465
