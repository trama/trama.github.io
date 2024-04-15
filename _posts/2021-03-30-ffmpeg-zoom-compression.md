---
layout: post
title: Zoom-like compression for lectures, using ffmpeg
date: 2021-03-30
description: How to use ffmpeg to provide a high compression level (like in Zoom) for lectures
---

In this last year, we have been accustomed to teach via conferencing tools.
We have several options (Meet, Teams, Zoom, BBB, etc) but Zoom provides, in my opinion, the best compromise between quality and compression level on recorded videos.

Indeed, if you have to record the lecture (maybe a 2 hours lecture) you have to use either the built-in functions of the software, or something made available by the OS.

And you may end up with a huge video file.
Who have tried to record the screen through the built-in functions of Win10 or Mac, just to make an example, should already know that the final file maybe in the order of GBs :sweat:
That is not the best way to record a lecture, I agree!
However, take into account that sometimes software functions may just be unavailable. Example: use Zoom on an iPad...if you have a valid account you may record on the cloud, otherwise, it simply does not provide a _local_ recording function. The only solution is to record your screen with the iPadOS function.

Conversely, if you are able to use the Zoom record functionality, you will end up with a really small file, more or less 100MB per hour, that however retains a rather good quality, especially if you use slides.

So, how can I try to reproduce the same compression scheme (end efficiency) for a large video?

The point is that, in that specific case, you are actually realizing a video with a really low motion level, for seconds you may be watching at the same slide...and honestly if I don't see PowerPoint animations at 60FPS, my eyes won't be hurted very much :rofl:.
Techincally speaking, you can decimate frames

<!-- 
{% raw  %}
{% highlight c++ linenos %}  <br/> code code code <br/> {% endhighlight %}
{% endraw %}

The keyword `linenos` triggers display of line numbers.
Produces something like this: -->

{% highlight bash linenos %}

    ffmpeg -i input.mp4 -vcodec "libx264" 
        -crf 36 -vf mpdecimate -vsync vfr -c:a aac -b:a 128k 
        -preset veryslow -profile:v high -tune stillimage 
        -max_muxing_queue_size 2048 -f output.mp4

{% endhighlight %}
