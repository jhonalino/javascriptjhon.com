---
title: Build Your Own Record Player Vanilla JS
description: Build your own Vanilla JS record player
date: 2020-05-15
tags:
  - vanilla js
layout: layouts/post.njk
---

Listening to music is always fun, but you know whats more fun than listening ? Thats right! Building your own Vanilla JS record player that plays that exact same music! [Here's](/demo/record-player-js/) what were gonna build. All you're gonna need to follow along is an html file and an mp3 on the same folder! lets get started!

## 1. HTML
For our HTML all we need is a container `<div>` for our record and a little hole `<div>` in the middle:

```html/11-13/
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>record-player-js</title>
        <style>
            /* //your styles here */
        </style>
    </head>
    <body>
        <div class="record-player-disc">
            <div class="hole"></div>
        </div>
        <script>
            //your JS here
        </script>
    </body>
    </html>
```

## 2. CSS
For styles we want to center everything from the body:
```css
    body {
        height: 100vh;
        display: flex;
        flex-flow: column nowrap;
        justify-content: center;
        align-items: center;
        background: #15202b
    }
```
Make a our disc rounded, optionally set an img as a background, and add a grayscale filter which can we toggle off when its playing:
```css
    .record-player-disc {
        width: 550px;
        height: 550px;
        border-radius: 50%;
        background-position: center;
        background-size: contain;
        background-repeat: no-repeat;
        border: 1px solid #000000;
        background-image: url('./img.jpg');
        position: relative;
        animation: rotate 20s infinite linear;
        animation-play-state: paused;
        filter: grayscale(1);
    }
```
We will then infinitely rotate it and remove the grayscale filter when 'playing' class is added:
```css
    .record-player-disc.playing {
        animation: rotate 20s infinite linear;
        filter: grayscale(0);
    }

    @keyframes rotate {
        100% {
            transform: rotateZ(360deg);
        }
    }
```

## 3. JS

To play our audio, we're going to create an `<audio>` element and reference our mp3 file:
```js
    const audio = new Audio("./music.mp3");
```
Get a reference to our record div when DOM is ready, and listen for the click event:
```js
    let disc, img;

    document.addEventListener("DOMContentLoaded", initialize);

    function initialize() {
        disc = document.querySelector(".record-player-disc ");
        disc.addEventListener("click", togglePlayback);
    }
```
We handle that click just by toggling play and pause of our audio element and adding or removing "playing" class for our CSS
```js
    function togglePlayback() {
        if (audio.paused) {
            disc.classList.add("playing");
            audio.play();
        } else {
            disc.classList.remove("playing");
            audio.pause();
        }
    }
```

## 4. THATS IT!
Have fun and enjoy your Vanilla JS Record Player. I encourage your to spice it up, change the music, colors, animation, etc.


here is the full source and the [demo](/demo/record-player-js/)
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>record-player-js</title>
  <style>
    body {
      height: 100vh;
      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;
      background: #15202b
    }

    .record-player-disc:hover {
      cursor: pointer;
    }

    .record-player-disc {
      width: 550px;
      height: 550px;
      border-radius: 50%;
      background-position: center;
      background-size: contain;
      background-repeat: no-repeat;
      border: 1px solid #000000;
      background-image: url('./img.jpg');
      position: relative;
      animation: rotate 20s infinite linear;
      animation-play-state: paused;
      filter: grayscale(1);
    }

    .record-player-disc.playing {
      animation: rotate 20s infinite linear;
      filter: grayscale(0);
    }

    @keyframes rotate {
      100% {
        transform: rotateZ(360deg);
      }
    }

    .record-player-disc .hole {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background-color: #15202b;
      border: 1px solid black;
      box-shadow: inset 1px 1px 6px #000000;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

  </style>
</head>

<body>

  <div class="record-player-disc">
    <div class="hole"></div>
  </div>

  <script>
    const audio = new Audio("./music.mp3");

    let disc, img;

    document.addEventListener("DOMContentLoaded", initialize);

    function initialize() {
      disc = document.querySelector(".record-player-disc ");
      disc.addEventListener("click", togglePlayback);
    }

    function addEventHandlers() {

    }

    function togglePlayback() {
      if (audio.paused) {
        disc.classList.add("playing");
        audio.play();
      } else {
        disc.classList.remove("playing");
        audio.pause();
      }
    }

  </script>
</body>

</html>

```