---
layout: post
title: Ionic is designed for mobile apps, not the desktop
date: 2015-05-16
categories: Tips
---

Ionic is designed for mobile devices, but since it is still technically a web application it could be used for desktop applications as well. While you can use Ionic to build desktop apps, I want to point out a number of hurdles that will stand in your way to building a successful web application for desktop environments.

<!--more-->

It needs to be clear that Ionic is designed for mobile devices for touch experiences. If you are aware of these types of issues and can navigate around them, then Ionic is certainly capable of providing you with a desktop web application as well.

### Ionic styles are optimized for iOS/Android browsers, not desktop or older browsers

The first, and most important thing is that the styling is designed to work in the iOS Safari browser and the Android browser/Chrome. The styling is not actively tested on other browsers or platforms, so you may run into issues where styling doesn't work correctly in some browsers, such as Firefox or Internet Explorer. This is especially true as you consider older versions of these browsers.

For example, in the [chapter 6 demo, settings view](http://dev.modern.ie/tools/screenshots/#https://ionic-in-action-chapter6.herokuapp.com/#/settings) of [Ionic in Action](/about), you can see that in the IE screenshot the range component is not properly styled.

### Many components are designed for touch, and are clunky with a mouse

The mouse can be used to click and drag to approximate touch events like swipes or drags, but this is clunky and not intuitive. This may cause components to be nearly useless on a desktop, because the UI components may not respond to traditional desktop environments with a mouse.

For example, in the [chapter 5 example](https://ionic-in-action-chapter5.herokuapp.com/#/tabs/rates) for **[Ionic in Action](/about)**, there is a list of current rates for Bitcoin in currencies. This list can be refreshed by pulling down to refresh, but on a desktop the user cannot use the mouse scroll wheel or trackpad to pull down. They must actually **click and drag** down to activate the pull to refresh. Not very intuitive for desktop use cases.

### Missing features that desktop apps might use

When you compare Ionic to another UI toolkit designed for the browser, such as [Twitter Bootstrap](http://getbootstrap.com), you will realize that some desktop features don't exist. When using a mouse, web applications have traditionally been able to use the position of the mouse to provide extra context (UX designers might fight over the usability of such features).

For example, this includes things like tooltips and dropdown menus, which don't have a place in a mobile/touch environment.

### The desktop doesn't have mobile platform features, or they are different

Mobile apps often use the device in some way, such as to track geolocation or to send push notifications. Currently, if these features exist on the desktop environment they are likely to require a different implementation than on mobile. Cordova, which is the platform Ionic uses to access the native device, [does provide some level of support](http://www.raymondcamden.com/2014/09/24/Browser-as-a-platform-for-your-PhoneGapCordova-apps) for the desktop browser, but features are limited.

For example, [some browsers are starting to support push messaging](http://updates.html5rocks.com/2015/03/push-notificatons-on-the-open-web), a similar concept to push notifications, but they are not the same and requires additional work to implement for both mobile and desktops.

Do you have any additional tips or warnings for using Ionic in a desktop environment? Share them in the comments!
