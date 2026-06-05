---
title: Pretty Heckin' Private
description: BYU CTF 2026
author: Zinko
date: 2025-12-05
categories: [Web]
media_subpath: '/assets/img/posts/PrettyHeckinPrivate'
---

This was a quest of many mistakes being made...

## Problems

I start off by going to the website that we were provided. I click all the buttons on the page but none of the buttons go anywhere. I scroll and down at the bottom there's an info tab that gets my attention.

![System Information](System-Information.png)

Luckily we have the code for the main page. I check the index.php file for anything suspicious and this code catches my eye

```php
<span class="info-value">PHP <?php echo phpversion(); ?></span>
<span class="info-value"><?php echo isset($_SERVER['PATH_INFO']) ? htmlspecialchars($_SERVER['PATH_INFO']) : '/'; ?></span>
```

These lines catch my eye as they're the only ones with php in them.

I start wondeirng where the PATH_INFO variable is coming from as that's the only dynamically generated thing on this page.

Luckily in our nginx.conf we have the answer!

```nginx
location ~ [^/]\.php(/|$) {
  fastcgi_split_path_info ^(.+?\.php)(/.*)$;
```

This leads me to believe that it's something to do with path traversal. htmlspecialchars normally prvents path traversal but there's ways around that.

I start messing around and doing some research (like 3 hours of testing) and came accross some interesting results from my testing.

1. This version of php is vulnerable to encoding a null byte `%0A` in the url. This leads to some interesting interactions...
2. If I make my url `(url)/index.php/a%0Aaa/.php` the webapp with display PATH_INFO.

![](Path-Info.png)

I thought that this was fascinating, we'll have to experiment with it more later.

3. Whenever you use the null character it consumes the 8 characters immediately following it.

![/index.php/a%0Aaaaaaaaahello.php](Url-Poc.png)

![The resulting path of hello.php](Path-Poc.png)

Talking advantage of this it allows you to bypass the htmlfilterchars to get ../ into the url address.

![/index.php/%0Aaaaaaaaaa%2E%2E/url](Url-Poc2.png)

![The resulting path of ../url](Path-Poc2.png)

I messed around with it for a bit but was ultimately unsuccessful in traversing any paths. 

I feel like there's something here though... It seems like it could be used with a bit more research on how it actually works and proccesses things.

## Solution

So as it turns out all of this was for not. I looked up PHP 7.3.9 (the version the site uses) CVE and found CVE-2019-11043.

Some more research brought me upon this POC exploit for it: https://github.com/neex/phuip-fpizdam.

I run the command with ./phuip-fpizdam https://php.csapi.dev/index.php.

This gives a result of that says to append to the url `?a=/bin/sh+-c+'which+which'&`.

Doing so doesn't appear to do anything but now the request path section doesn't show anything.

However, if we refresh the page a few times we get something interesting...

![/usr/bin/which appears!](ExploitStarted.png)

It works! We are able to run commands through the url!

We then use `a=ls /` to see the root directory.

![Listing root directory](lsresults.png)

We then put in our final url of `/index.php?a=cat /flag.txt`

![](flag.png)

Flag: byuctf{it's_a11_pwn?_alway5_ha5_b33n} 
