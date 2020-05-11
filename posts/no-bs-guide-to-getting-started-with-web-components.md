---
title: No BS Guide to Getting Started With Web Components
description: No BS Guide to Getting Started With Web Components
date: 2020-05-10
tags:
  - vanilla js
  - web components
layout: layouts/post.njk
---

Here is the Web Component that we're going to make, a product component that has a photo, a title, a price and a "buy now" button
<iframe
     src="https://codesandbox.io/embed/no-bs-web-components-cwkly?fontsize=14&hidenavigation=1&theme=dark&view=preview"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="no-bs-web-components"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts">
</iframe>

To get started all you're gonna need is an HTML file

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>WebComponents</title>
  </head>
  <body>
  </body>
</html>
```

## 1. HTML Templates
Templates will hold any html without rendering it to the page for example:

```html
 <template>
   <p>this html won't be rendered to the page </p>
  </template>
```

We can use this to create a reusable template for our product component. Lets create our product html inside a `<template>`
```html
<!DOCTYPE html>
<html lang="en">
  ...
  <body>
    <template id="product-card-template">
      <style>
        :host {
          --primary: #ffc107;
          --secondary: #000;
          font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto,
            Oxygen-Sans, Ubuntu, Cantarell, Helvetica Neue, sans-serif;
        }

        .product-container {
          padding: 1.25em;
          display: inline-block;
          background: var(--primary);
        }

        .thumb-cover {
          width: 100%;
          height: 100%;
          background-size: cover;
          background-position: center;
          border-radius: 20px;
        }

        .thumb {
          position: relative;
          width: 200px;
          height: 300px;
          border-radius: 20px;
          box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16),
            0 3px 6px rgba(0, 0, 0, 0.23);
        }

        .info {
          display: flex;
          justify-content: space-between;
          color: var(--secondary);
          text-transform: uppercase;
          margin-bottom: 1em;
          margin-top: 1em;
        }

        .info p {
          margin: 0;
        }

        .buy-now {
          width: 100%;
          padding: 0.8em 3em;
          box-sizing: border-box;
          text-transform: uppercase;
          font-size: 1em;
          background: var(--secondary);
          font-weight: lighter;
          color: var(--primary);
          outline: none;
          border: 1px solid var(--secondary);
        }

        .buy-now:hover {
          background: var(--primary);
          color: var(--secondary);
          border: 1px solid var(--secondary);
          cursor: pointer;
        }
      </style>

      <div class="product-container">
        <div class="thumb">
          <div
            class="thumb-cover"
            style="background-image: url(https://i.picsum.photos/id/25/300/300.jpg);"
          ></div>
        </div>
        <div class="info">
          <p>age of ultron</p>
          <span>$49</span>
        </div>
        <button class="buy-now">buy now</button>
      </div>
    </template>
  </body>
</html>
```

## 2. Custom Elements
custom elements allows you to defined your own Custom HTML Elements

so instead of a regular div you can define something complete arbitrary like:

```html
  <product-card></product-card>
```

which can also have its custom attributes like:

```html
  <product-card
    img="https://i.picsum.photos/id/25/300/300.jpg"
    title="some trees"
    price="$49"
  ></product-card>
```

to define one, you would need a class that inherits from HTMLElement and define its custom name with `customElements.define()`

```html
<!DOCTYPE html>
<html lang="en">
...
  </template>
    <script>
      class ProductCard extends HTMLElement {
        constructor() {
          super();
        }

        // gets called when this element has been mounted to DOM
        connectedCallback(e) {}
      }

      customElements.define("product-card", ProductCard);
    </script>
    </body>
</html>

```


## 3. Shadow DOM
Shadow DOM allows you to encapsulate your custom Elements so any css it have can't affect any HTML outside, preventing you from polluting the global CSS
```html
  <script>
      class ProductCard extends HTMLElement {
        constructor() {
          super();

          //"this" refers to your Custom Element in this context

          //this.attachShadow will create a shadow dom for your custom element
          //which you can then assign to an arbitrary instance var called "shadow"
          //any descendant of shadow DOM will be encapsulated so it's CSS can't affect anything outside
          this.shadow = this.attachShadow({
            mode: "open"
          });

          //get template reference for the reusable Template you've made in (1. HTML Templates)
          var template = document.getElementById("product-card-template");

          //get template content
          var templateContent = template.content;


          //clone template content and append it to your shadow DOM
          this.shadow.appendChild(templateContent.cloneNode(true));
        }

        // gets called when this element has been mounted to DOM
        connectedCallback(e) {
          //you can do normal DOM operations on your Custom element as well as its shadow DOM

          //gets the attribute of your custom element
          var img = this.getAttribute("img");
          var title = this.getAttribute("title");
          var price = this.getAttribute("price");
          var primary = this.getAttribute("primary");
          var secondary = this.getAttribute("secondary");

          this.shadow.querySelector(".info p").innerHTML = title;
          this.shadow.querySelector(".info span").innerHTML = price;
          this.shadow.querySelector(
            ".thumb-cover"
          ).style.backgroundImage = `url(${img})`;
          this.style.setProperty("--primary", primary);
          this.style.setProperty("--secondary", secondary);
        }
      }

      customElements.define("product-card", ProductCard);
    </script>
```

and there you go, you've just made a fully functional web component using the 3 web technologies:

1. HTML Templates - create reusable `HTML Template` without being rendered on the page
2. Custom Elements  - define `custom HTML Element` with arbitrary names `<custom-element/>`
3. Shadow DOM - a shadow of an Element which encapsulates all the styles of its descendants from Global CSS and outside HTML

used together, these tech allows you to build a component for the web such as the `<product-card></product-card>` component, thus called Web Components.

I encourage you to play around with the source code, make your own components and get wild with your ideas to make awesome new components

#### `full sourcode`
<iframe
     src="https://codesandbox.io/embed/no-bs-web-components-cwkly?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="no-bs-web-components"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>
