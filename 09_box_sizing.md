## Box Sizing

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Box Sizing</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div id="container">
      <h1>Container</h1>
      <div id="child">
        <h2>Child</h2>
      </div>
    </div>
  </body>
</html>
```

```css
#container {
  width: 300px;
  background-color: lightblue;
}

#child {
  width: 100%;
  border: 10px solid black;
  padding: 12px;
  background-color: orange;
}
```

so we see the html and the css. pretty simple stuff. container has a `width` of `300px` and child has a `width` of `100%`.

But when we look at the output we see the child is overflowing from the container. So what's happening here? We set the `width` to `100%` which should say `100%` of the size of the container.

The problem is setting the `width` to `100%` sets the `width` of the content, but in addition to the content, we have `10px` of border and `12px` of padding. And because this is on each side, we have `20px` total of border on the left and right, and `24px` of padding on the left and right. So this is causing our child to overflow becaues this isn't being accounted for in the `width`.

So we could solve this with `calc()`.

```css
#child {
  width: calc(100% - 20px - 24px);
}
```

This would work but this isn't very clean code. Now we have these values hardcoded to these other values. We will see in the CSS variables how we can avoid hardcoding all the values but it's still not very clean code. So how else could we solve this?

And the solution is the `box-sizing` property. What the `box-sizing` property does is __it says should we use the width and height of the content or all the way out to the edge of the border?__

If we set `box-sizing: content-box`, it's not going to change anything, because that's the default and `context-box` says the size of the box, the size of width is affected by the width of just the content. However, we can change this to `border-box`.

```css
#child {
  width: 100%;
  box-sizing: content-box;
}
```

Now this `width: 100%` is the equivalent of what we did before with `calc()`. So it's no longer `300px` but `300px - 20px - 24px`.

Now some people love `border-box` and think it's a much cleaner box sizing and some people like `content-box` and switch to `border-box` only when needed.

But a very common CSS ruleset you will see to be have the universal selector and set the entire page to use `box-sizing: border-box`, and when you need `content-box` you could switch it back.

```css
* {
  box-sizing: border-box;
}
```

If you're coming into a project I would recommend check to see what their `box-sizing` property is set to so you know how `width` and `height` are calculated for elements in the project.
