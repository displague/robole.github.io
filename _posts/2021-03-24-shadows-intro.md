---
layout: post
title: "Shadows - A practical guide for front-end devs"
description: "Shadows add physical realism to user interfaces. When used well, they can help create interfaces that pop. This article is a short visual guide. It shows you some practical applications of shadows, and how you can use different properties to achieve different effects. It will teach the syntax without lengthy descriptions."
image: /assets/img/blog/2021-03-24-shadows-intro/nes-controller.apng
tags: [css]
published: true
---

<img src="/assets/img/blog/2021-03-24-shadows-intro/sufis.jpg" alt="whirling dervishes" style="display:block;width:100%;max-width:1200px;margin:0 auto;">

Shadows add physical realism. When used well, they can help create interfaces that _pop_. 🍾

To demonstrate this, I recreated a Nintendo (NES) controller in HTML and CSS. Below is a GIF of the controller, toggling all of the shadows on and off to highlight the differences.

<img src="/assets/img/blog/2021-03-24-shadows-intro/nes-controller.apng" alt="whirling dervishes" style="display:block;width:100%;max-width:600px;margin:0 auto;">

Without shadows, the controller has a cartoony, graphic look. With shadows, the controller looks more realistic and tactile. You can play with the example in [this codepen](https://codepen.io/robjoeol/full/ZELzVPV).

This article will show you how you can use different properties to achieve different effects. It teaches the syntax without lengthy descriptions. It shows practical applications of shadows.

## Syntax

When learning new CSS properties, I prefer to try out some code while I read through a description. This helps to verify my understanding as I go. A live playground can be very helpful if you like to learn in a similar way. The codepen below allows you to play with the `box-shadow` property using the control panel.

<p class="codepen" data-height="650" data-theme-id="light" data-default-tab="result" data-user="robjoeol" data-slug-hash="jOVjdeW" style="height: 650px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="box-shadow playground">
  <span>See the Pen <a href="https://codepen.io/robjoeol/pen/jOVjdeW">
  box-shadow playground</a> by Rob (<a href="https://codepen.io/robjoeol">@robjoeol</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

The summary below outlines the different methods for creating shadows. There are 3 CSS properties and 1 SVG element. The syntax is pretty consistent across them. Shout-out to the W3C! 🙌

<img src="/assets/img/blog/2021-03-24-shadows-intro/shadow-summary.png" alt="syntax summary" style="display:block;width:100%;max-width:1200px;margin:0 auto;" loading="lazy">

You may be wondering why I am including a SVG element in here. Well, I am covering shadows on the web. SVGs are a web technology, so why not leverage the knowledge while you're at it?

Let’s look at the parameters in more detail.

## Offsets (`x-offset`, `dx` , `y-offset`, and `dy`)

Offsets are used to nudge a shadow away from the element it targets. The `x-offset` sets the horizontal position, and the `y-offset` sets vertical position of the shadow _relative_ to the target element.

<img src="/assets/img/blog/2021-03-24-shadows-intro/offsets.png" alt="Offset illustration" style="display:block;width:100%;max-width:600px;margin:0 auto;" loading="lazy">

It is analogous to using `position: relative` along with the properties `top`, `left`, `right`, and `bottom`.

<img src="/assets/img/blog/2021-03-24-shadows-intro/offsets.gif" alt="demo of offset parameters" style="display:block;width:100%;max-width:550px;margin:0 auto;" loading="lazy">

If the `x-offset` and `y-offset` are both zero, you may not see a shadow. This is because the shadow is obscured by the target element (same position). A shadow is the exact same size as the target element, and it lies below it (it's like it has a lower z-index).

The properties take any [length value](https://developer.mozilla.org/en-US/docs/Web/CSS/length) (`em`, `px`, `vh`..etc), but not percentages.

The offset properties are required for parameters for `box-shadow`, `text-shadow`, and `drop-shadow()`.

The `dx` and `dy` attributes are optional for `<feDropShadow>`. They have a default value of 2.

### Blur Radius (`blur-radius` and `stdDeviation`)

The blur radius controls the amount of blur applied to a shadow. Blur makes the shadow become fainter and bigger.

A value of zero is no blur (duh). The larger this value is, the bigger the blur. You can’t have a negative value.

<img src="/assets/img/blog/2021-03-24-shadows-intro/blur-radius.png" alt="blur radius examples" style="display:block;width:100%;max-width:291px;margin:0 auto;" loading="lazy">

If you want to dig into more details on what a blur radius really is, David Baron elaborates in his article - [What does a blur radius mean?](https://dbaron.org/log/20110225-blur-radius).

The calculation of blur in `box-shadow` and in filters (`filter:drop-shadow()`, `<feDropShadow>`) is different. So applying a blur of 2 pixels will not look the same when applied to each of these properties. You would only notice this if you use them in the same place.

### Spread Radius (`spread-radius`)

The spread radius resizes a shadow. Positive values expands the shadow, negative values shrink the shadow.

<img src="/assets/img/blog/2021-03-24-shadows-intro/spread-radius.gif" alt="spread radius demonstration" style="display:block;width:100%;max-width:596px;margin:0 auto;" loading="lazy">

A spread radius of 2px adds 2px to each side, this increases the width and height of the shadow by 4px.

**This parameter is only available to `box-shadow`**.

### Color (`color` and `flood-color`)

You can set the color of the shadow. The default value is [currentColor](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentcolor_keyword) (the value of `color` that is inherited from an ancestor).

The `flood-color` attribute for `<feDropShadow>` is equivalent to `color`. It has a default value of black.

### The `inset` **keyword**

The `box-shadow` property is the only one that can create inner shadows (that are drawn inside an element). The presence of the `inset` keyword makes a shadow an inner shadow.

<img src="/assets/img/blog/2021-03-24-shadows-intro/inset-shadow.png" alt="Inner shadow example using inset keyword" style="display:block;width:100%;max-width:619px;margin:0 auto;" loading="lazy">

The shadow is drawn inside the border, above the background, but below the content.

You can fake an inner shadow for text with an [unusual hack](https://codepen.io/robjoeol/pen/LYRXdjG).

### Multiple Shadows

To specify multiple shadows, you provide a list of shadows to the property.

The list syntax differs:

- `box-shadow` and `text-shadow` have comma-separated lists,
- `drop-shadow()` has space-separated lists.

```css
.myBoxShadow {
  box-shadow: 20px 20px 0 0 grey,
              40px 0 0 0 red;
}

.myTextShadow {
  text-shadow: 20px 20px 0 0 grey,
               40px 0 0 0 red;
}

.myDropShadow {
  filter: drop-shadow(20px 20px 0 grey)
          drop-shadow(40px 0 0 red);
}
```

The z-ordering of multiple shadows follows the order in which they are specified (the first specified shadow is on top).

#### Unexpected behaviour with multiple `drop-shadow()` instances

One unusual thing with `drop-shadow()` is that you get more shadows than you specify! If you specify 3 instances of `drop-shadow()`, you get 7 shadows. Why is that?

<img src="/assets/img/blog/2021-03-24-shadows-intro/drop-shadow-multiple.png" alt="multiple drop-shadow()" style="display:block;width:100%;max-width:623px;margin:0 auto;" loading="lazy">

This is because a filter behaves like an image transformation pipeline. It uses the outputs of one transformation as the input for the next transformation.

For this example, the output of the first invocation of the function is one shadow plus the original element. These are the inputs for the second invocation. The filter creates 2 new shadows as it processes the 2 inputs. The figure below gives an outline of what the algorithm looks like at each invocation.

<img src="/assets/img/blog/2021-03-24-shadows-intro/multiple-shadow-explanation.svg" alt="Multiple shadows using filter:drop-shadow()" style="display:block;width:100%;max-width:600px;margin:0 auto;" loading="lazy">

## SVG

As we discussed already, `<feDropShadow>` creates a drop shadow for SVG elements. It must be used inside a `<filter>` element. It is applied to an element using the `filter` attribute.

```html
<svg viewBox="0 0 30 10" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="shadow">
      <feDropShadow dx="0.2" dy="0.4" stdDeviation="0.2" />
    </filter>
  </defs>

  <circle cx="5" cy="50%" r="4" filter="url(#shadow)" fill="red" />
</svg>
```

This produces this:

<img src="/assets/img/blog/2021-03-24-shadows-intro/fedropshadow.png" alt="fedropshadow example" style="display:block;width:100%;max-width:300px;margin:0 auto;border:1px solid darkgrey;" loading="lazy">

## Characteristics of shadows on the web

- Shadows don’t influence the document layout.
- A shadow is the same size as the element it targets. You can modify the size of a `box-shadow` (through the spread radius parameter), but other properties cannot modify the shadow size.
- A shadow implicitly has a lower Z-index than elements, so a shadow will sit below other elements.
- If an element with a `box-shadow` is clipped (with `clip-path`) or uses a mask ( with `mask`), a shadow is never shown. Whereas if an element with `text-shadow` or `filter: drop-shadow()` is clipped, a shadow will be shown (if it is within the clip region).
- You can't create shadows that have diagonal sides with any of the shadow properties.

## Practical usage

You will reach for different properties depending on what type of element you are targeting, and what it is you want to do.

Generally, you will use:

- [`box-shadow`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) for drop shadows for elements (regular shapes);
- [`text-shadow`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-shadow) for applying shadows to text and adding some stylish flourishes to text;
- [`filter: drop-shadow()`](<https://developer.mozilla.org/en-US/docs/Web/CSS/filter-function/drop-shadow()>) for drop shadows for irregular shapes such as transparent images, clipped elements, and for grouped elements;
- [`<feDropShadow>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feDropShadow) for drop shadows for SVG elements.

The `box-shadow` property adds a shadow to the element’s box (defined by the [box model)](https://www.w3schools.com/Css/css_boxmodel.asp). If you use `border-radius` to add rounded corners, the shadow will also has rounded corners. The shadow mirrors the shape of the box. When I refer to a regular shape, I mean the box shape.

On the other hand, the `drop-shadow()` filter will add a drop shadow based on the visible content of an element. Take an image with transparency such as the PNG of a bicycle below. When we apply a `drop-shadow()` to it, it produces a shadow based on the outline of the bicycle.

<p class="codepen" data-height="548" data-theme-id="light" data-default-tab="result" data-user="robjoeol" data-slug-hash="xxRovrb" style="height: 548px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Adding filter:drop-shadow() to a PNG">
  <span>See the Pen <a href="https://codepen.io/robjoeol/pen/xxRovrb">
  Adding filter:drop-shadow() to a PNG</a> by Rob (<a href="https://codepen.io/robjoeol">@robjoeol</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

The shadow properties are most often used for drop shadows, but there are many other applications. Floating buttons and sunken combo-boxes use shadows to create the perception of depth. Beyond that there are many creative uses of the properties to achieve a wide range of visual effects. The codepen below demonstrates a wide range of applications with code.

<p class="codepen" data-height="554" data-theme-id="light" data-default-tab="result" data-user="robjoeol" data-slug-hash="qBaMQEN" style="height: 554px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Shadow Showcase">
  <span>See the Pen <a href="https://codepen.io/robjoeol/pen/qBaMQEN">
  Shadow Showcase</a> by Rob (<a href="https://codepen.io/robjoeol">@robjoeol</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

Te `text-shadow` property can be used for adding drop shadows to text, but often it is used a lot to dress-up text in creative ways. You can see a wide range of examples below.

<p class="codepen" data-height="714" data-theme-id="light" data-default-tab="result" data-user="boltaway" data-slug-hash="iIwqu" data-preview="true" style="height: 714px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Text Shadow Compilation">
  <span>See the Pen <a href="https://codepen.io/boltaway/pen/iIwqu">
  Text Shadow Compilation</a> by emma (<a href="https://codepen.io/boltaway">@boltaway</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### Creating more realistic shadows by using multiple shadows

If you use a single shadow, you can't express some of the complexities and nuances of shadows in real life. Shadows generally aren't uniform in color, size, and shape. Using multiple, layered shadows can overcome some of these limitations. You can see an example of this below.

<img src="/assets/img/blog/2021-03-24-shadows-intro/layered-shadows.png" alt="layered shadows" style="display:block;width:100%;max-width:560px;margin:0 auto;" loading="lazy">

Tobias Bjerrome gets into this topic in more detail in his article - [Smoother & sharper shadows with layered box-shadows](https://tobiasahlin.com/blog/layered-smooth-box-shadows/).

Phillp Brumm wrote a [WYSIWYG tool to help create layered shadows](https://shadows.brumm.af/).

## What about pseudo-elements?

You can apply shadow properties to the `::before` and `::after` pseudo-elements.

- A `box-shadow` can be applied to the the `::first-letter` pseudo-element.
- A `text-shadow` can be applied to the `::first-letter` and `::first-line` pseudo-elements.

## Browser support

- `box-shadow` [support is virtually universal](https://caniuse.com/?search=box-shadow) (97.8 global usage including IE9+).
- `text-shadow` [support is virtually universal](https://caniuse.com/css-textshadow) (98.93% global usage including IE10+).
- `drop-shadow()` [support is excellent](https://caniuse.com/css-filters) (95% global usage).
- `<feDropShadow>` [support could be better](https://caniuse.com/mdn-svg_elements_fedropshadow) (64.45% global usage). Safari does not support the element at all.

For the CSS properties, you can use them freely. It is only an issue if you need to support IE11 and you want to use `drop-shadow()`.

Using `<feDropShadow>` is a bit more fraught considering Safari does not support it! The alternative is to draw your own shadow with a shape or `<path>` to maximize cross-browser compatibility.

## Conclusion

Shadows are a vital part of creating realistic interfaces. Learning the syntax is straightforward, but mastering the application of shadows takes practice. To learn more, you can check out a companion article I wrote - [Getting Deep into Shadows](https://css-tricks.com/getting-deep-into-shadows/).
