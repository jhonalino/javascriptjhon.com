---
title: 7 Ways to Make a Cake With Arrow Functions and Why It Can Have a Bitter Aftertaste
description: Learn different ways to write arrow functions and how it could hurt readability of your code
date: 2020-05-13
tags:
  - vanilla js
layout: layouts/post.njk
---

I love the fat arrow function! It's elegant, modern and with its ability to be written in many variations, can be done in significantly fewer keystrokes. But at what cost ?

Let's make a cake to find out!

Here we have a function called makeCake:

```js
  function makeCake() { }
```

The function written in standard ES5 is equivalent to the following fat arrow function :

```js
  const makeCake = () => { }
```

Like regular functions, the fat arrow function parameters are placed between the parentheses.

```js
  const makeCake = (flour) => { }
```

In addition, you would also use the return keyword to return a value.

```js
  const makeCake = (flour) => { return flour }
```

However, if you only have one parameter, you can omit its surrounding parentheses altogether.

```js
  const makeCake = flour => { return flour }
```

An expression immediately to the right of the arrow is implicitly evaluated and returned,

so we can omit the surrounding curly block, as well as the return keyword, leaving the expression we want to return.

In this example the snippet above is equivalent to:

```js
  const makeCake = flour => flour;
```

Our makeCake is going to require more than 1 ingredient, so we need to list the parameters between the parenthesis:

```js
  const makeCake = (flour, eggs, sugar) => flour + eggs + sugar;
```

In addition, if we want to return an object literal implicitly, we need to wrap it in parentheses so JavaScript doesn't mistake it for the function's curly braces.

```js
  const makeCake = (flour, eggs, sugar) => ({ cake: flour + eggs + sugar});
```

As you can see, our arrow function is written more concisely, but it doesn't necessarily make it easier to read.

When looking at the variations in which fat arrow functions can be written individually it is not quite as difficult to process. But imagine hundreds of lines of code and the difference in variation would be much more challenging.

In development we spend a lot of our time debugging, so wouldn't it make sense to explicitly state our intent while writing code even if it means more keystrokes?

```js
  function makeCake(flour, eggs, sugar) {
    return {
      cake: flour + eggs + sugar
    }
  }
```

By reading the snippet above, one can see immediately that it is a named function because of the function keyword. The parentheses and the return statement are in plain view thus it is clear what the function returns.

I hope you enjoyed making a cake with this article! Fat arrow functions have many use cases; however in the end it requires practice to be well versed in the many variances of fat arrow functions. I'm going to end this article with a tweet from Bram Cohen that I think some of us can relate to

<blockquote class="twitter-tweet" data-theme="light"><p lang="en" dir="ltr">&quot;90% of coding is debugging. The other 10% is writing bugs&quot;</p>&mdash; Bram Cohen (@bramcohen) <a href="https://twitter.com/bramcohen/status/51714087842877440?ref_src=twsrc%5Etfw">March 26, 2011</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>





Special thanks to [Daniel Parker](https://www.linkedin.com/in/daniel-parker-15887a91/) and [Patricia Burns](https://www.linkedin.com/in/patricia-burns-aa62b616/) for editing this article!
