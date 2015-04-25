---
layout: post
title: How to fix CORS problems and No Access-Control-Allow-Origin header errors with Ionic
date: 2014-11-20
categories: Tutorial
---
A new solution has been built into the Ionic CLI, [read about it here]({% post_url 2015-01-14-how-to-fix-cors-issues-revisited %}).

When building a hybrid app with Ionic, you will often need to load data from some API. When you are running your Ionic app in the browser using `ionic serve`, it usually runs on `localhost:8100`. However if you have to load data from another domain or port you might get this type of error.

<!--more-->

    No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:8100' is therefore not allowed access.

This happens due to the browser's security policies, which essentially a way to block access to data from other domains. This applies to XMLHttpRequests (XHR) requests, which are also known as AJAX requests made with JavaScript to load data. When using Ionic and Angular, any requests made to another domain fall into this category and are subject to this security policy.

This is of course a problem for developers who need to load data from other domains. So browsers came up with the concept of [Cross origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Essentially before a browser will make a cross domain XHR request (which is usually a [GET or POST](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post) request), it first makes an ORIGIN request. This is often called the preflight request, and you can think of it like checking that a phone number is in service before being allowed to actually connect. This ORIGIN request is simple, it just asks the server a simple question, 'Hey can I load this data?'. The server then decides if the requesting domain is allowed and says 'Yes' or 'No'.

The good news is if you have control over the data server, you can configure it to properly respond when an ORIGIN request is made. Unfortunately if you do not have control, you are limited and will have to setup a CORS proxy service.

### Setup a CORS Proxy

You can create a proxy service, which means you will make an API that handles CORS but underneath makes requests to the real API. For quick development, there is a handy NodeJS module](https://www.npmjs.org/package/corsproxy) that will help you out. You can install it like using npm and start the proxy server.

    npm install -g corsproxy
    corsproxy

The server will start up and you'll be able to then make requests using the following syntax.

    http://localhost:9292/mydomain.com/api/endpoint

This works because CORS only applies to requests made by the browser, and the localhost:9292 server (which is the corsproxy server) can make that request to the real API without the OPTIONS preflight request.

If you wanted to setup a full time server, you can dig into it more with the great resource [Enable CORS](http://enable-cors.org).

### Have other issues or solutions?

I'd be happy to expand this resource with more information or solutions, just let me know in the comments!
