---
layout: post
title: "Hacking iFrames for Fun & Proper Image Orientation"
modified:
categories: 
excerpt:
tags: []
image:
  feature:
date: 2014-11-05T19:55:21-08:00
---

#####Why do things the right way, when you can do them the wrong way and put them in an iFrame?)***

At [Sqor Sports](https://sqor.com/), we handle a lot of user and athlete created content. One of the challenges faced when accepting this content is honoring EXIF orientation data. Ever since the iPhone 6 Plus came out, we started seeing photos from users that couldn't reach the camera button when in landscape mode. They looked like this:


<figure class="half">
	<a href="https://d262ilb51hltx0.cloudfront.net/max/1200/0*XWHSHBaBFWRodlLs."><img src="https://d262ilb51hltx0.cloudfront.net/max/1200/0*XWHSHBaBFWRodlLs."></a>
</figure>


Clearly, that’s bad.

We wondered if it would be possible to handle EXIF data on the front end and save us some server cycles.

Disclaimer: This is a hack, not a sustainable solution - it doesn’t even work on IE. We share it because we thought it was a pretty neat trick.

When dealing with user submitted content, we were surprised at how bad the state of detecting EXIF data was. Gmail ignored the problem for a long time, and other big sites [like DERPDERP] still don’t handle it. Only a few sites like Facebook do a perfect job handling EXIF rotation data. Solving the problem - especially just on the front end - seemed difficult.

*Reference: www.daveperrett.com/articles/2012/07/28/exif-orientation-handling-is-a-ghetto/*



#####The Solution for Chrome & Safari (Desktop):

Notice first that if an image is opened from the desktop with Chrome (Open With), it is displayed with the expected orientation:

The next step was to see if somehow putting the image in an iFrame inside 

<figure class="half">
	<a href="https://d262ilb51hltx0.cloudfront.net/max/1085/0*Mr5hW82d61aGOERI."><img src="https://d262ilb51hltx0.cloudfront.net/max/1085/0*Mr5hW82d61aGOERI."></a>
</figure>

It worked! Success!  Well... not exactly.


######Setbacks:

When testing our solution, we quickly ran into a problem. Since the images were saved without file extensions, when we pointed the iframe at them, the browser would think they were file downloads and show a download prompt. That was unacceptable.
 
We solved this problem like we solved every problem - with more hacks:

1. Point the iFrame to an image that would work, i.e. pixel.jpg
2. Use javascript to load the iFrame, look for the “img” tag inside the iFrame, and replace that “img” tag with the target image (that has no extension). 

<figure class="half">
	<a href="https://d262ilb51hltx0.cloudfront.net/max/805/0*a7vQtdIgLn42mQHS."><img src="https://d262ilb51hltx0.cloudfront.net/max/805/0*a7vQtdIgLn42mQHS."></a>
</figure>

Now we have success - and no download prompts.

<figure class="half">
	<a href="https://d262ilb51hltx0.cloudfront.net/max/700/0*yZVrAVfMfWCV-_Jn."><img src="https://d262ilb51hltx0.cloudfront.net/max/700/0*yZVrAVfMfWCV-_Jn."></a>
</figure>


Eventually, everything was switched and implemented on the server but it was fun while it lasted.

#####Check out the Sqor Open Source Github [Repo](https://github.com/sqor/)
