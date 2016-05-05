---
title: How Chartholdr Works
date: 2015-07-12
tags: rails, web dev
category: web dev
---


![Chartholdr pie graph](http://chartholdr.io/pie/200)

I remember the first time I stumbled across Placehold.it, a simple image placeholder serving plain images with text indicating the width and height. Immediately, I wondered how the site was able to deliver images with the illusion they always existed on the server.

A basic image placeholder could be made by generating the images once and leaving them on the server at the appropriate URL.

For instance, you could write a script that generates images between 1x1 and 1000x1000 and save them to the server's www/ folder. This would require no serverside logic, but it would be a huge waste of disk space, since there's a high chance most of the images will never be needed.

I can't attest to Placehold.it's serverside logic, but I can give a technical overview of how the image placeholder I built handles dynamic image rendering and serverside caching.
READMORE

## Routes
Taking advantage of the Ruby on Rails router, I grab the graph type, width, height (optional), and color (optional) all from one URL comprised of the following syntax.

```
http://chartholdr.io/bar/1000/500/c=9d5ddd
```
The routes.rb calls the Application Controller which initializes the generator object and sends the inline png file. 

The generator's constructor takes in the chart object so it knows which templates to use when rendering. If the image isn't already cached in the  public folder, the generator's get method initializes PhantomJS, renders the JS chart, saves the image to the public folder and then returns the file location.

Originally, I put most of the logic in the application controller. When I realized I wanted to generate multiple chart types, however, I decided to make the process modular. As you can tell, I took advantage of abstraction whenever I could.

```Router ---> Application Controller ---> Generator ---> Chart```

## Rendering

I used Zurb's Pizza Amore pie library to generate the charts. While there are more sophisticated libraries out there such d3, I chose Pizza.js because it is lightweight and its simple charts are perfect for placeholder lorem ipsum.

I knew I needed a headless browser to generate the charts. PhantomJS was the obvious choice since it has built-in svg support as well as the ability to take screenshots.

## Caching

I first thought about setting up an E3 database to go with my Elastic Beanstalk instance. But why use a database when I could just place the images in the public folder? So that's what I did.

Let's say I went to the url ```localhost:3000/pie/300```

If this image has not been generated before, the url is converted to a path and passed into PhantomJS where it will be saved to the public folder. If the image already exists, the application controller calls the send_data method and sends the image located at the converted url path, in this case, ```public/pie/300/300```.

## The Source

I had a blast working on this project, and I do have plans to continue working on it. If you'd like to contribute, the project is open source on [github](https://github.com/NoahHines/Chartholdr).

[1]:https://twitter.com/NoahTrust