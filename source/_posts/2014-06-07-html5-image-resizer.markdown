---
layout: post
title: "HTML5 Image Resizer"
date: 2014-06-07 00:08:49 +0200
comments: true
categories: ["javascript","html5", "canvas", "apps", "opensource"]
description: Resizing images in the browser with HTML5 new features
---

Many have already experimented with resizing images in the browser using the canvas element, but all 
I saw were just experiments for resizing one image that’s understandable as many of it were relatively 
old “2-3 years ago”, browsers were slower also many people are still considering browsers not good enough 
for such computationally intensive tasks. But now as browsers are becoming more and more efficient at doing this 
tasks even performing quite as good as ImageMagick! "see results below". So I decided to make an app to resize 
images in the browser & generate zip file. 
[Here it is](http://dbasem.com/my-apps/html5-img-resizer/) and [Github repo](https://github.com/Basemm/html5-img-resizer)

{% img center https://raw.githubusercontent.com/Basemm/html5-img-resizer/master/screenshot.png 'HTML5 Image Resize App Screenshot' 'HTML5 Image Resize App Screenshot' %}


Features:
----------

- Quick way to resize images, no need to download & install a dedicated app also you won’t 
need to upload your files to any of online image resizing websites. Resize the image directly in your browser!

- Fast “tested in Chrome, quite as fast as ImageMagik convert!”

- Accept png and jpeg

- Set jpeg quality

- Resize to fixed dimensions “preserve aspect ratio” or use percentages

Caveats:
----------

- Unlike ImageMagick, browsers can’t directly persist each resized image
on disk so the whole process run in memory & generate zip file for all of
them at the end. Obviously it won’t scale when used with hundreds of large
images.

- Repeatedly resizing lots of images without page refresh will slow down the browser due to a memory leak,
it need further checks.

Benchmark in Chrome vs ImageMagick convert:
----------

**Scaling 100 PNG images "424 MB" down by 50%**

- Chrome: 1 minute, 12 seconds "72851 millisecond"

- ImageMagick convert: 1 minute, 10 seconds

**Test run in**

- Chrome version: 35.0.1916.153

- OS: ubuntu 14.04LTS, 64bit

- Processor: Intel® Pentium(R) CPU G630 @ 2.70GHz × 2

- Memory: 8 GB


Notes:
----------

- Chrome numbers cover also generating & saving the zip file, so it
could actually perform better if there’s a way to provide the images to user
directly in a friendly way without zip compression.

- The 100 images in above test is not a limit by any means, it depends on your machine and you can go beyond this number!
