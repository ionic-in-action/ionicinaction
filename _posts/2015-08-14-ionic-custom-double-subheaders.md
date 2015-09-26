---
layout: post
title: Custom Double Subheaders
date: 2015-09-24
categories: Tips
---

Have you ever tried to put custom content inside an Ionic Framework subheader or maybe needed two subheaders? In most cases, this is no big deal.  However, your content can't exceed the height of the subheader (44px) or your app's content inside `ion-content` will be partially hidden behind your thicker subheader.

<!--more-->

> This is a guest post by Justin Noel,the developer of [Kids in Touch](https://kidsintouch.com) - a safe messaging app for kids.

### Custom Header Bar
Here's an example of a custom header that contains a very large button.  As you can see, the content section is obscured by the button.  The button even overflows outside of the subheader.  Scroll down in the content section to see the hidden paragraphs.

<img src="{{ site.baseurl }}/images/big-buttons-problem.png" alt="Big Buttons Problem" style="height: 500px" />

[See it in action](http://play.ionic.io/app/9ddfabd1d6b6)

### Double Header Bar
Here's an example of trying to use 2 subheaders.  As you can see, the second subheader completely overlaps the first subheader.

<img src="{{ site.baseurl }}/images/second-subheader-problem.png" alt="Second Subheader Problem" style="height: 500px" />

[See it in action](http://play.ionic.io/app/f03bfd2b1498)

Initially, this seems like a pretty easy obstacle to overcome.  You just do a bit of custom CSS to set the height of the header and all is well ... until it isn't.  You did all your custom CSS based on your app running in the browser.  Then, when you ran on iOS it all broke because of the iOS status bar.  So, back to the drawing board.  If you really want this to work properly in all platforms, you'll need to spend a lot of time understanding the contents of Ionic Framework's `_platform.scss` file.

So, you finally get it all working great and your customer/boss says, "Make the buttons bigger.  Oh, we also need a special subheader on Page X and another on  Page Y."

Argh!  Have fun keeping all this custom CSS organized and working properly across a wide variety of platforms/releases.

Fortunately, there is an easier way.  You just need to take advantage of the power of AngularJS's custom directives.

We'll create special directive called `positionBarsAndContent ` that will solve all of these troubles.

<script src="https://gist.github.com/calendee/e189e5ac267107aa1039.js"></script>

Now, let's see how those 2 examples work with this new directive.

### Custom Header Bar Corrected

Notice how the subheader is correctly sized now and the content is not obscured.

<img src="{{ site.baseurl }}/images/big-buttons-fixed.png" alt="Big Buttons Fixed" style="height: 500px" />

[See it in action](http://play.ionic.io/app/59aee016c90c)

FYI: This particular sample has some custom CSS to make the bar the right size:

{% highlight css linenos %}
.bar .button{
  height: auto;
  padding: 20px;
}

.bar.bar-subheader {
  height: auto; // Override Ionic's 44px bar height and let it size itself automatically based on the content.
}
{% endhighlight %}

### Double Header Bar Corrected

You can see that the second subheader no longer sits on top of the first subheader.  Additionally, the content area is properly position below all the subheaders.

<img src="{{ site.baseurl }}/images/second-subheader-fixed.png" alt="Second Subheader Fixed" style="height: 500px" />

[See it in action](http://play.ionic.io/app/c142f56b167f)

As you can see, this single directive can solve just about any special requirement you throw at it. If you need 1, 2, or even 3 or more subheaders, the directive can handle it.  If you need a single custom height subheader, you're covered!
