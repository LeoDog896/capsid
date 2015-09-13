# class-component.js v5.0.0

> Framework to define reusable HTML class component

***note*** This library depends on jQuery and is jQuery plugin


## How to use

Through npm

```js
global.jQuery = require('jquery');
require('class-component');
```

Through bower

```html
<script src="path/to/jquery.js"></script>
<script src="path/to/class-component.js"></script>
```


## Class Component

What is a class component?

A class component is a HTML element which has the special functionality (called coelement) according to its `class` attribute.

### Background

It's been a common technique in frontend development to bind some handlers to the specific HTML classes like the following.

```js
$('.foo').on('click', someProcess);
```

In the above, `.foo` class has the special functionality of peforming `someProcess` on click on it. What `class component` does is very similar as the above but it cares a bit more about the timing of initialization or the prevention of the double initialization.

It may be similar to [Custom Element](http://www.html5rocks.com/en/tutorials/webcomponents/customelements/) in the basic idea but `class component` is based on html class and doesn't require any new API.


## Interfaces

```js
/**
 * @param {String} name The name
 * @param {Function} definingFunction The defining function
 */
$.cc.register(name, definingFunction);
```

This registers a "class component" of the given name using the given defining function.
The given defining function is called only once on an element of the given class name at `$(document).ready` timing.
The defining function takes one arugment which is jquery object of the element. This function is called only once for each class component element.

If you want to add class component elements after `$(document).ready` timing, you can initialize them by calling `$.cc.init('class-name')`, which initializes all class components on the page. The double initialization is automatically prevented by the framework.

See the [DEMO](http://kt3k.github.io/class-component/test.html).


---

```js
/**
 * @param {String} name The name of the class component
 * @param {HTMLElement|null} elem The element in which the class components are initialized
 */
$.cc.init(name, elem);
```

`$.cc.init` initializes the class components `name` in `elem`. If `elem` is omitted, then the elements in the whole page are initialized. If `name` is omitted, then all registered class components are initialized.


## Examples

Download button

js

```js
$.cc.register('download', function (elem) {

    elem.click(function () {

        window.open(elem.attr('url'), '_blank');

    });

});
```

html
```html
<button class="download" url="http://url/to/dl-target">DL</button>
```

When you click the above button, new window opens and starts downloading it.

---

Hover element

js

```js
$.cc.register('my-anchor', function (elem) {

    elem.on('click', function () {

        location.href = elem.attr('href');

    });

    elem.on('mouseover', function () {

        elem.addClass('hover');

    });

    elem.on('mouseout', function () {

        elem.removeClass('hover');

    });

});
```

html
```html
<div class="my-anchor" href="https://www.google.com/">...</div>
```

When you click the above div, the page goes to href's url (https://www.google.com/ in this case) and when you mouse over it, it gets `.hover` class.

## See also

- [actor-system](https://github.com/kt3k/actor-system)
  - The utility to define more complex class components easily

## Example components

- [event-hub](https://github.com/kt3k/event-hub)
- [event-twister](https://github.com/kt3k/event-twister)

## License

MIT
