---
layout: post
title: Livereload your Ionic app inside of your emulator or device
date: 2014-10-03
categories: Tutorial
tags: [tips]
---
The Ionic CLI tool is quite powerful and is able to do some very neat things that will make development easier. One of my favorite gems is the ability to use livereload inside of an emulator or device so you can develop and preview without rebuilding your app!

If you aren't familiar with livereload, the concept is to automatically reload the app anytime you save a file in your editor so you can preview everything instantly. No more having to rebuild, reload, or wait.

To use this amazing feature, you just have to emulate or run your app with the -l flag. The -c flag is used to send the data you normally see in the browser console into the command line. The last flag -s allows any server logs to be sent to the command line as well, which is helpful when you are noticing server errors.

    ionic emulate ios -l -c
    ionic run android -l -c

This handy tip can speed up your testing and development without having to wait for the project to build and reload inside of the emulator or device.
