---
title: Get Your Javascript Web App Started Without React
description: How to Write a Javascript Web App Without React
date: 2020-05-09
tags:
  - vanilla js
layout: layouts/post.njk
---

If you're used to writing javascript with frameworks, writing with vanilla javascript can be intimidating. But it doesn't have to be that way! it can be a lot quicker to get started especially without all the tooling and configuration bloat that usually comes with a framework. All you need is an HTML file, a script tag and 5 simple steps

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .is-red {
            color: red
        }
    </style>
</head>
<body>
    <p class="sample-paragraph">hello you</p>
    <button id="sampleButton">sample button></button>
   <script>
    //your JS here
   </script>
</body>
</html>
```

### 1. Wait for the DOM to be ready with DOMContentLoaded

Most scripts interact with a DOM one way or another. For example changing some text when the user clicks a button or attaching click handlers. But before we can interact with the DOM, it first has to be loaded.

```javascript
    document.addEventListener("DOMContentLoaded", function () {
        //your code here when dom is loaded
    });
```


### 2. Referencing a specific HTML element

There are a couple ways of referencing an element, one of which is `document.querySelector()` which accepts a CSS selector as a parameter.

```javascript/1/
    document.addEventListener("DOMContentLoaded", function () {
        document.querySelector('#button');
    });
```

This selects the first element that has an id of 'button'. Referencing an element allows you to script the element within JS such as listening for events.

### 3. Attaching an event listener

For the elements that you have references, you can attach an event listener and a handler using `element.addEventListener(eventName, callback)`

```javascript/2,4/
    document.addEventListener("DOMContentLoaded", function () {
        document.querySelector('#button')
        .addEventListener('click', function() {
            //handle click here
        })
    });
```

### 4. Changing an elements HTML

You can also change the text or HTML of an element with `element.innerHTML`

```javascript/3/
    document.addEventListener("DOMContentLoaded", function () {
        document.querySelector('#button')
        .addEventListener('click', function() {
            document.querySelector('.sample-paragraph').innerHTML = "not so sample now";
        })
    });
```


### 5. adding/removing a class

use `element.classList.add()` and `element.classList.remove()` to add or remove classes respectively

```javascript/4/
    document.addEventListener("DOMContentLoaded", function () {
        document.querySelector('#button')
        .addEventListener('click', function() {
            document.querySelector('.sample-paragraph').innerHTML = "not so sample now";
            document.querySelector('.sample-paragraph').classList.add('is-red');
        })
    });
```


## That's it!
there's a lot more to vanilla JS but these 5 steps will get you started with your interactive web app without react.
