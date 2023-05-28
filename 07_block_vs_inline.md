## Block vs Inline

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Block vs Inline</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <p>I'm a paragraph!</p>
    <p>I'm <em>another</em> paragraph!</p>
  </body>
</html>
```

```css
p {
  border: 2px solid black;
}

em {
  border: 2px solid blue;
}
```

So we have two different paragraphs but the latter has an emphasis tag. And in the CSS we are just giving the black border to `p` tags and a blue border to `em` tags.

What you might notice about the output is that the `p` tag, regardless of how much text, that border is taking up the entire width of the body. Why is that happening? That is because the `p` tag defaults to what we call a __block level element__. 

__Block level elements__
- default to taking up the width of their parent
- start on a new line

So regardless of how big these paragraphs are, they start on a new line. We can test this by changing the width to `30vw`.

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  border: 2px solid blue;
}
```

Now the width gets much smaller and we could fit these paragraphs on one line but they still end up going onto a new line.

The `em` tag is an __inline element__.

__Inline elements__
- only take up the width of their parent
- don't start on new lines

I can change the width of `em` to `100vw` and nothing is going to change. Why does nothing change? Because it's an inline element, it's just looking at the width of its content. The same thing is true of height. I could set `100vh` for height too and nothing will change..

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  width: 100vw;
  height: 100vh;
  border: 2px solid blue;
}
```

### `display` property

That being said, we can change the `display` property of any element if we want to. We usually don't want to, but we can.

All of the tags that contain small pieces of text like `em` and `strong` will usually be inline to default. And usually the large containers will default to block. And this is what we want. If I change `em` to have `display: block;`, then we see it is taking `100vw` and `100vh`.

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  display: block;
  width: 100vw;
  height: 100vh;
  border: 2px solid blue;
}
```

And if we erase the width and height from `em`, you can see the `em` tag is like acting the `p` tag and getting its own line. The reason its sort of squished against the other things is the paragraph tag has some default tags.

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  display: block;
  border: 2px solid blue;
}
```

Let's get of rid this now.

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  border: 2px solid blue;
}
```

### `display: inline-block`

What if we did want the paragraphs to be on the same line as each other? I guess there's a few ways. We could set a `display: inline` and now we see they end up on the same line. But now this `30vw` isn't making any effect anymore and that's because this is an inline element, and inline elements can't have a width and a height.

So what we can do is set `display` to `inline-block`. This is sort of a middle ground where it doesn't go to a new line but you can still create custom widths and heights.

```css
p {
  width: 30vw;
  border: 2px solid black;
}

em {
  border: 2px solid blue;
}
```

Now we see our paragraphs get this `30vw` width but also are on the same line.

There are plenty of other ways to get elements on the same line but this is one of those ways. We don't use this a ton but it is nice to know that exists.

By default, the vast majority of container style elements we see will be `display: block`. The vast majority of the small pieces of the content will be `display: inline`. Really the only tag we tend to see with `display: inline-block` are images. And this is useful because we want to resize images but don't want them taking up their own line.
