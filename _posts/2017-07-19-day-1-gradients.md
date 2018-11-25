---
title: Day 1 Gradients
date: 2017-07-19 00:00:00 +03:00
layout: single
excerpt: 'Today, I practice gradients and try to figure out what makes a good gradient
  from an unsightly one!

'
---

Ok, so I'm pretty familiar with how to make a button:

```html
<button style="background: #cfcfcf;">Hi there!</button>
```
Preview:
<button style="background: #cfcfcf;">Hi there!</button>

Ok, but that's plain boring. Let's add some juicy gradient goodness to the mix!

## Gradient backgrounds

Gradients are most often used with the `background` CSS property, and there are two types:

- Linear Gradient
- Radial Gradient (I'll cover this later)

Linear gradient is the popular kid on the block, and it's defined like so:

```css
background: linear-gradient(direction, color-stop1, color-stop2, ...);
```

Ok, let's try that on our button:

```html
<button style="background: linear-gradient(to bottom, red, blue);">Hi there!</button>
```
<button style="background: linear-gradient(to bottom, red, blue);">Hi there!</button>

Ah, that's looking better. 

I mean, sorta. It still looks horrendous (when you consider the actual colors). I think having subtle gradients would work better, I found a website that showcases some good looking gradients [here](https://uigradients.com/). 

Let's take one example &hellip; [OrangeFun](https://uigradients.com/#OrangeFun): 

```html
<button style="
  background: linear-gradient(to bottom, #fc4a1a, #f7b733);">Hi there!</button>
```
<button style="background: linear-gradient(to bottom, #fc4a1a, #f7b733);">Hi there!</button>

Oh, that looks sweet &mdash; but *why*? What's the right amount of "distance" between colors so it turns out OK? I plugged the two colors into Photoshop to see how they differed:

![Picking a gradient](/assets/gradient-picking-one.png)

Hmm, it seems that the primary difference is in that H value ("Hue"), with a difference of about ~30&deg;. Nice. That's probably a good benchmark to consider when picking colors for a gradient combo.

> Lesson: Vary Hue (up to 30&deg;) to get a good color combo for a gradient.

Finally, let's add abit more CSS to make the thing look nice and polished:

```html
<button style="
  background: linear-gradient(to bottom right, #f7b733, #fc4a1a);
  border: 1px solid #f7b733;
  border-radius: 3px;
  color: #fff;
  padding: 10px 20px;">Hi there!</button>
```
<button style="
  background: linear-gradient(to bottom right, #f7b733, #fc4a1a);
  border: 1px solid #f7b733;
  border-radius: 3px;
  color: #fff;
  padding: 10px 20px;">Hi there!</button>

Ah, that looks lovely! Giving it a bit of breathing space (using `padding`) and a border with the lighter of the two shades looks great.

> When using a gradient, use the lighter shade as the border

Also, I changed the direction of the gradient so it looks like the light is coming from the top left. I remember reading something about that somewhere, and will make tomorrow's post about diving into lighting and shadows and all that goodness!

Stay tuned.

Next&hellip;
- Radial gradients
- Lighting, shadows
