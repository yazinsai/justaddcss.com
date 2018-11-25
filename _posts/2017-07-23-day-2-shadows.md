---
title: Day 2 Shadows
date: 2017-07-23 00:00:00 +03:00
layout: single
excerpt: 'Today, we look at shadows and page lighting. You know how some shadows look
  amazing and others just look forced. Hopefully, we''ll figure out how to make the
  former.

'
---

Ok, so first let's talk about the CSS `box-shadow` property that we'll be using:

```css
box-shadow: none|h-shadow v-shadow blur spread color |inset|initial|inherit;
```

- `h-shadow` and `v-shadow` are the positions of the horizontal and vertical shadows, respectively. They are in distance units (e.g. `px`).
- `blur` is the blur distance. Larger values mean the shadow is more, well, blurred.
- `spread` is the size of the shadow (with negative values allowed). It's like the thickness of the shadow outline of the object. A negative value would mean that the shadow is *smaller* than the object.
- No points for guessing what `color` is.
- `inset` changes the shadow from an outer shadow (outset) to an inner shadow, if set.

As far as color goes, using a semi-transparent option seems to be the popular option &mdash; and most readily simulates real shadows: `rgba(0, 0, 0, 0.4)`.

Let's mess around with it abit:

```html
<div style="
  box-shadow: 10px 5px 2px 3px rgba(0, 0, 0, .4); 
  width: 100px; height: 100px;"></div>
```
<div style="box-shadow: 10px 5px 2px 3px rgba(0, 0, 0, .4); width: 100px; height: 100px; margin-bottom: 20px;"></div>

Ok, so if I wanted to create an effect like the one in the image below:

<img src="/assets/shadow-recess-middle.png">

&hellip; I know that:

- The shadow has to be smaller than the object &hellip; so `spread < 0`
- The shadow is centered, so the horizontal distance from the center of the object `h_distance = 0px`
- Since the negative `spread` will cause the vertical distance to reduce to the center, we'll need to offset it by the same amount or slightly more (so it pokes out). That means `v_distance >= spread`

Which makes:

```html
<div style="
  box-shadow: 0px 7px 5px -5px rgba(0,0,0,.4);
  width: 100px; height: 100px; background: #f7f7ca;"></div>
```
<div style="
  box-shadow: 0px 7px 5px -5px rgba(0,0,0,.4);
  width: 100px; height: 100px; background: #f7f7ca; margin-bottom: 20px;"></div>

Not bad for such an early try!

Turns out, you can also set the `box-shadow` property multiple times to the same element (e.g. adding an `inset` shadow, and a regular one).

{% comment %}
See also:
https://codepen.io/haibnu/pen/FxGsI
{% endcomment %}

## Back to buttons

In [the previous post]({% post_url 2017-07-19-day-1-gradients %}), we ended up with a button:

<button style="
  background: linear-gradient(to bottom right, #f7b733, #fc4a1a);
  border: 1px solid #f7b733;
  border-radius: 3px;
  color: #fff;
  padding: 10px 20px;">Hi there!</button>

&hellip; and wanted to add a shadow to it so it looks more realistic. We spoke briefly about lighting and how having a fixed light point on the page can help you decide how the gradients and shadows should look like.

Now, we'll try and put that to practice.

If we assume that the light source is in the top-left corner of the page, what should the shadow look like? My intuition is:

- It'll be below the button (as opposed to above it 😅)
- and slightly to the right so `h_position > 0`
- with the shadow slightly larger than the button itself so `spread > 0`
- no idea what blur should look like, so i'll try a bunch of stuff here

### First attempt

```html
<button style="
	box-shadow: 3px 2px 3px 2px rgba(0,0,0,.4);
	...
```

<button style="
	box-shadow: 3px 2px 3px 2px rgba(0,0,0,.4);
  background: linear-gradient(to bottom right, #f7b733, #fc4a1a);
  border: 1px solid #f7b733;
  border-radius: 3px;
  color: #fff;
  padding: 10px 20px;">Hi there!</button>

That looks way too forced. It's screaming newbie! Let's

- soften the shadow (more blur, lower spread)
- change the border to be slightly darker than the button

### Second attempt

```html
<button style="
	box-shadow: 2px 2px 4px 1px rgba(0,0,0,.4);
	...
```

<button style="
	box-shadow: 2px 2px 4px 1px rgba(0,0,0,.4);
  background: linear-gradient(to bottom right, #f7b733, #fc4a1a);
  border: 1px solid #fc4a1a;
  border-radius: 3px;
  color: #fff;
  padding: 10px 20px;">Hi there!</button>

Better, but still looks &hellip; off.

I did some searching and [found](https://www.smashingmagazine.com/2017/02/shadows-blur-effects-user-interface-design/) this excellent image that sums up how elevation affects the shadow of an object (in terms of size and blur):

![Shadows](/assets/object-elevation-shadow-opt.gif)


