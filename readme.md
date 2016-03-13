knockout.animate
================

*Animate.css custom binding for Knockout.js*

[animate.css](https://github.com/daneden/animate.css) is a bunch of cool, fun, and cross-browser animations for you to use in your projects `now with support of Knockout.js`. Great for emphasis, home pages, sliders, and general just-add-water-awesomeness.

Installing
----------

Download `knockout.animate.min.js` and all dependencies (`animate.css`, `knockout.js`) or use `Bower` command:

```
bower install knockout.animate
```

Usage
-----

To use `knockout.animate` in your website, simply drop the `animate.css`, `knockout.js` and `knockout.animate.js` into your document's <head>:

```html
<head>
  <link rel="stylesheet" href="animate.min.css">
  <script type="text/javascript" src="knockout.min.js"></script>
  <script type="text/javascript" src="knockout.animate.min.js"></script>
</head>

```


Then add next data-binding to an element:

```html
<div data-bind="animate:{ animation: 'zoomIn', state: true"></div>
```

That's it! You've got a CSS animated element. Super!

Use observable to control animation
-----------------------------------

You can control when animation is going to happen by assigning `Knockout Observable` to `state` field:

```html
<div data-bind="animate:{ animation: 'zoomIn', state: state"></div>
```

```js
function Viewmodel(){
  this.state = ko.observable(true);
}

ko.applyBindings(new Viewmodel());
```

Animation will be played when observable become `true`.

Assign `in` and `out` states and toggle between them
----------------------------------------------------

You can add `in` and `out` animation this way:

```html
<div data-bind="animate:{ animation: ['zoomIn', 'zoomOut'], state: state"></div>
```

First animation will be played when `state` field become `true` and second when `false`.

Assign custom handlers on state change
--------------------------------------
The `before` and `after`

```html
<div data-bind="animate:{ animation: 'zoomIn', state: state, before: beforeAnimate, after: afterAnimate }, text: message">
  Hello World!
</div>
```

```js
function Viewmodel(){
  this.state = ko.observable(true);
  this.message = ko.observable('Hello World!');
  
  this.afterAnimate = function(event, state){
    this.message = ko.observable('Goodbye World!');
  }
}

ko.applyBindings(new Viewmodel());
```

removeClass and animation-fill-mode: forwards
---------------------------------------------
In some cases you may not want to remove the animation class (`bounceInRight`...)
after the animation has finished.

This can be the case when using the CSS property `animation-fill-mode: forwards`.

In that case you can set the option `removeClass` to `false`:

```html
<div data-bind="animate:{ animation: 'zoomIn', state: state, removeClass: false }">
  Hello World!
</div>
```

The class will then only be removed when `state` is toggled again.

Reference: <https://developer.mozilla.org/en/docs/Web/CSS/animation-fill-mode>