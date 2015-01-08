---
layout: post
title: Techniques for styling Ionic apps
date: 2014-11-25
categories: [Tips]
tags: [styling]
---
There are many ways that you can manage the CSS for your Ionic app, and I'd like to share a few tips how I prefer to keep my CSS clean.

Disclaimer. I'm not as concerned about CSS optimization in a hybrid app when the CSS is bundled with the app itself. There are two primary reason to optimize CSS, to speed up the delivery of the file over HTTP and to minimize the number of CSS rules the browser has to track. When the file is bundled in the app, there is almost no latency to load the file and that takes care of the first reason. I still attempt to keep my CSS as lean as possible and avoid unnecessary rules for the browser, and you could run it through [Uncss](https://github.com/giakki/uncss) to clean out unused selectors.

## Tip 1 - Use SASS and change defaults

I think you get a lot of value from building the CSS using SASS. Ionic builds their CSS bundle using SASS, so you can modify the variables that are global values. All apps should consider changing the default colors for their app, and you can do that by modifying SASS variables.

First, you'll need to setup Gulp and your app. The Ionic CLI prepares the environment for Gulp, but you have to install it yourself. Install the node modules needed in your app for this task.

    npm install
    gulp

This will build the CSS file into the www/css/ionic.app.css file, which you then need to use instead of the ionic.bundle.css file used by default.

To use some variables, open the scss/ionic.app.scss file and add this line before the @import at the bottom. This sets the default color used for the primary CSS class, and when the CSS is built it will override the default.

{% highlight sass %}
$positive: #53922B !default;
{% endhighlight %}

There are other variables, which you can find a complete list in the [source code here](https://github.com/driftyco/ionic/blob/master/scss/_variables.scss). You may need to modify the gulp build job if you move the location of the SCSS files.

If you are making a lot of changes, use the watch task to rebuild automatically on file changes.

    $ gulp watch

## Tip 2 - Prefix CSS selectors by view or component

CSS cascades, so writing CSS can accidentally collide with other views if you aren't careful. My preferred technique is to use a class on the root of every view template and then prefix all of my CSS rules for that view with that class. Assume this is the view template HTML. I just add a class to the root of the view template HTML.

{% highlight html %}
<ion-view title="My View" class="my-view">
  <ion-header-bar class="bar-stable">
    <h1 class="title">Ionic View</h1>
  </ion-header-bar>
  <ion-content>
    <ion-list>
      <ion-item>Item</ion-item>
    </ion-list>
  </ion-content>
</ion-view>
{% endhighlight %}

Now this is how I would write my SCSS for this view. This only applies to CSS rules that are for this view. This will center the text of an item in a list and change the list to white text on black, but only for this view. Essentially I just wrap the entire set of rules with the view class, since SASS will compile each rule down to valid CSS for me.

{% highlight scss %}
.my-view {
  ion-list {
    background: #000;
    color: #fff;
  }
  ion-item {
     text-align: center;
  }
}

/* SASS converts above to
.my-view ion-list { background: #000; color: #fff; }
.my-view ion-item { text-align: center; }
*/
{% endhighlight %}

This has helped prevent unintended CSS collisions and allows me to use the same CSS class names in different views without fear.

## Tip 3 - Organize SCSS/CSS with HTML files

I prefer to use a folder structure for my views that contains the JavaScript, CSS, and HTML for each view in one place. Some people like to use another method, but this makes the most sense to me. Instead of writing one large CSS file or placing them in different places, I put them side by side and only write CSS specific to that HTML template.

I find the most time I waste writing CSS is trying to locate where a given CSS rule was declared, and this has helped to minimize that problem.

## Tip 4 - Target platforms with CSS

There is a handy class added to the body of the document that tells you what platform is currently being used. That allows you to write CSS specifically for Android or iOS, and you should when you can make something look more like the native platform design guidelines. Here is what the body class might look like for an iPhone.

{% highlight html %}
<body class="grade-a platform-ios platform-ios7 platform-ios7_0 platform-ready" />
{% endhighlight %}

## Share your tips

If you have some other great CSS tips for Ionic, leave them in the comments! I'll happily update the article with more tips.
