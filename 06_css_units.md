## CSS Units

### Lengths

- `px`: Pixels, absolute length
- `em`: Relative to font size
- `rem`: Relative to root element font size
- `vw`: 1% of viewport width
- `vh`: 1% of viewport height
- `ch`: Width of "0" character
- `%`: Percentage, usually relative to parent value

These could be used for properties such as width, height, font size, margin, etc. The most basic is pixels. Most important point is that pixels are absolute so they don't scale as the user of resizes. Variety of absolute units as inches and centimeters but don't get used as much so we won't focus on them.

On the other hand, relative units make our lengths relative to something else. And there are a variety of useful units to choose what that something else is.

`em` it will be relative to the font size. If you are using `em` to set a font size, it will be relative to a parent's font size. `rem` is very similar to `em` but it's relative to the `<html>` tag. The root font size defaults to 16 px but we can always change that by changing the font size on the `<html>` tag. Moreover, often overridden by browser font size settings.

`vw` and `vh` stand for viewport height and viewport width. `1vw` is 1% of the width of the viewpoint. `50vw` is 50% of the width of the veiwpoint.

`ch` is relative to the width of the 0 character in the current font, which allows us to make width based on number of characters in a paragraph.

`%` represent a percentage value relative to something else, usually the parent's value for that same property but sometimes it can act differently depending on the property.

---

So that's great and all, but how do we choose a unit? There are no hard set rules, but there are general guidelines.

If you're coming into a project that is already in-progress, being consistent with the existing code is oftentimes your best bet.

## Width and Height

- `%` to be relative to parent
- `vw/vh` to be relative to viewport
- `ch` for paragraph widths
- `rem` for closer to absolute values
  - `px` as a last resort for true absolutes`

Oftentimes `%` unit so sizes relative of parent. Oftentimes want to take half width of parent. Occasionally we use `vw/vh` to be relative to entire viewpoint. `ch` is for a specific use case, and that is choosing the width of a paragraph. Once paragraphs exceed 70 characters per line they become hard to read. So setting `ch` to 50-70 is a way to get a good readable paragraph. For an absolute value, I would recommend `rem`. Still relative but it is the closest relative unit to being absolute. For most users, it would be relative to 16px but not related to anything in the page. But for users who have chosen to change default font sizes, this will still scale. And finally as a last resort, if you need height and width to never change, you can use `px` but it is detrimental to accessibility.

### Margin and Padding

- `rem` for closer to absolute values
- `em` to scale with font size
- `px` for small values, last resort

### Borders and Shadows

- `px` for small values
- `rem/em` okay here too
  - scaling doesn't always look great

`px` is usually fine because we often don't want borders and shadows to scale and it will become too big for users. `rem/em` is fine but it just depends on what you want to happen when a user has a larger front size.

### Font Size

`rem` is usually best
`em` is to scale to parent size
`px` as a last resort

I prefer using `rem`. These scale with user preferences while being easy to work with. `em` can be good if you want values to scale with parent size but I tend to find this to be confusing in large projects if there's a large chain of parents. `px` is a last resort as they will often prevent fonts from scaling with user preferences and we don't want to prevent user preferences fro mworking.

### Colors

- Keywords: red, blue, etc.
- Hex RGB: `#4B7DAF`
- RGB: `rgb(75, 125, 75)`
  - RGBA: `rgb(75, 125, 75, .5)`
- HSL: `hsl(210, 40%, 49%)`
  - HSLA: `hsl(210, 40%, 49%, .5)`

So these all really mean the same thing. I often find that people use hexadecimal but I find that hard to read compared to the RGB or HSL.

### Code Demo

Now let's move onto the code.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Units</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div id="parent">
      <div id="red">Red</div>
      <div id="blue">Blue</div>
      <div id="green">Green</div>
    </div>
    <p>
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
      I am a very long paragraph.
    </p>
  </body>
</html>
```

```css
#parent {
  width: 75%;
  border: 2px solid black;
}

#red {
  width: 50%;
  background-color: red;
}

#green {
  width: 50vw;
  background-color: green;
}

#blue {
  width: 10rem;
  background-color: blue;
}

div {
  margin: 10px;
  color: white;
}
```

So first let's at the widths. The `parent` has a width of 75%. So it's taking up 75% of its parent, the body, which is the entire page. And `red` takes a width of 50%, and 50% refers to 50% of its parent which is `parent`. And `red` is 50% of 75% if we wanted to get its entire percentage of the body. And then we get to `blue` which is `50vw`, which is 50 viewport width which is half the size of the browser window. Finally we have `green` which is `10rem` which is essentially using an absolute width because we haven't changed the `html` element. So the width of will be `16 x 10` pixels, or 160 pixels.

Now let's change the width of `parent` to be 50%. Now we can see that `red` changes in response because it's scaling in response, and blue is overflowing because `50vw` is larger than the space of `parent`. `green` is now about half the width of `parent` but it hasn't changed at all.

If we change the width of `parent` to be 25%. `red` is still scaling but now `blue` and `green` are both overflowing. This shows why in general I recommend using percentages for width so they don't start overflowing and they scale with their parents.

---

Next let's look at this paragraph and it's super long and hard to read. But with a bigger browser window it would  be harder to read.

We want the `ch` unit here.

```css
p {
  width: 60ch;
}
```

Now what's nice is the width is based on the font sie and the font family. And this isn't based on the screen size the user is using.

---

Next let's take a look at the font sizes. It's all defaulting to 16px because that's what the root element is set to. Let's change it.


```css
p {
  width: 60ch;
}

#parent {
  width: 75%;
  border: 2px solid black;
}

#red {
  font-size: 1em;
  width: 50%;
  background-color: red;
}

#green {
  font-size: 1rem;
  width: 50vw;
  background-color: green;
}

#blue {
  font-size: 16px;
  width: 10rem;
  background-color: blue;
}

div {
  margin: 10px;
  color: white;
}
```

You can save this and nothing changes. `green` is 16px which was the default. `blue` is looking at root element which we haven't changed which is defaulting to 16px. `red` is looking at its parent which also hasn't been changed which is also defaulting to the root element which is 16px. But if we change the `font-size` of `parent` to 1.5em, we'll see `red` gets a little bit bigger because `red` is looking at `parent`.

Now let's change the font size of the root element.

```css
html {
  font-size: 24px;
}

#parent {
  font-size: 1em;
  width: 75%;
  border: 2px solid black;
}
```

So now what happened is that the font size of `parent` is 1.5em, which is 1.5 times its parent and its parent is the body so it'll be `1.5 * 24` or 36px. And then `red` is 1em so it's the same as its parent so it's also 36 pixels. `blue` has a font size of `1rem` and `rem` is going to `html` font size, so it's 24px. And the green font is still set to the absolute value of `px`. And this why we don't recommend using `px` because it won't scale if the user has changed the value of the root element in their browser.

```css
#blue {
  background-color: rgb(75, 125, 175);
}
```

So this is mostly a blue and greenish color with a little bit of red. We can add an alpha value. If the alpha value is .5, it's transparent. At 1 it's opaque. And at 0 it disappears.

```css
#blue {
  background-color: rgba(75, 125, 175, .5);
}
```

```css
#blue {
  background-color: rgba(75, 125, 175, 1);
}
```

```css
#blue {
  background-color: rgba(75, 125, 175, 0);
}
```

We can also use HSL as well, and also play with the alpha values.

```css
#blue {
  background-color: hsl(210, 40%, 49%, .5);
}
```

And as we can see the colors look exactly the same. It just depends on which style you prefer.
