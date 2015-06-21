---
layout: post
title: Time inputs with Ionic
date: 2015-06-22
categories: Tips
---

This is a guest post by [Justin Noel @candelee](https://calendee.com/) sharing insights into using the time input field with Ionic and how it behaves differently on iOS and Android devices with a nice fix.

<!--more-->

I recently needed to include a time field in an app I'm working on. By default, the `<input type="time">` field displays seconds and milliseconds in Chrome. Of course this is completely useless to the average mobile user.

When you put a time input in an Ionic Framework app, you get to discover one of the joys of cross platform mobile app development.  iOS displays the time correctly as `HH:MM`. Great! Unfortunately, Android will display the full time including seconds and milliseconds just like Chrome.

While trying to fix this, I discovered a post from [Mark & Ruth](http://mark.zealey.org/2015/01/08/formatting-time-inputs-nicely-with-angularjs) that showed how to use a directive to correct the display. Their sample didn't quite work for me as my times did not end in 00 seconds and 000 ms.

Fortunately, the fix just required a bit of regex changes.

```
.directive('formattedTime', function ($filter) {

  return {
    require: '?ngModel',
    link: function(scope, elem, attr, ngModel) {
        if( !ngModel )
            return;
        if( attr.type !== 'time' )
            return;

        ngModel.$formatters.unshift(function(value) {
        	// Replace the seconds & ms like :23.298 with nothing
            return value.replace(/:[0-9]+.[0-9]+$/, '');
        });
    }
  };

});
```

The `formattedTime` directive simply kills the seconds and milliseconds so they don't show up in the view. This solves the display problem in Chrome. Again, Android has to be different. It will no longer show the milliseconds, but insists on showing the seconds.

Here's a [working example](http://play.ionic.io/app/f9c3230ab47b) showing the difference between displaying a regular time input and a formatted one.

#### iOS Screenshot

![iOS Time Formatting]({{ site.baseurl }}/images/formatted-time-ios.png)

#### Android Screenshot

![Android Time Formatting]({{ site.baseurl }}/images/formatted-time-android.png)
