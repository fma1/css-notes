## Position

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Box Sizing</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <p>I am a paragraph</p>
    <section>
      <div id="box">Box</div>
      <p id="long">
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
        This is a very long paragraph with a lot of text.
      </p>
    </section>
  </body>
</html>
```

```css
p {
  font-size: 1.75rem;
  margin: 1.5rem;
  padding: 1rem;
  border: 2px solid black;
}

body > p {
  background-color: lightblue;
}

#box {
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}

#long {
  background-color: lightyellow;
}
```

So first on the paragraphs we're just making things easier to see and making font sizes bigger. We give the first `p` a light blue background. We give the `#box` a light green background. And then we give `#long` a light yellow background.

By default we say all the elements on the page are what we call static positioned and this is just the positioning we've been used to. And if we scroll everything scrolls like we expect it to. But we can change the way this works by using the `position` property.

### `position: fixed`

```css
#box {
  position: fixed;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}
```

So what `fixed` says is this will be removed from the normal flow of the document. So you'll see this pushes it on top of other elements. And we can use the `top` property to move the box. So `top: 10px` will set it `10px` from the top of the browser window.

```css
#box {
  position: fixed;
  top: 10px;
  left: 200px;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}
```

And now when I scroll, you'll see the box stays there because it is __fixed__ to the viewport. So it'll always be `10px` from the top of the window. You could remove the `top` property and add `bottom: 10px` and it becomes fixed `10px` from the bottom of the viewport.

I would usually avoid `position: fixed` because it can cover up other items on the page which is a bad user experience. But it's good to know we have that option.

### `position: relative`

```css
#box {
  position: fixed;
  bottom: 10px;
  left: 200px;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}
```

`position: relative` is fairly simple. It sticks the element where it would normally be. Then it uses the `bottom` and `left` or the `top` and `right` properties to add an offset based on that natural position.

So if I comment `bottom` and `left` you'll see this is it's normal position. And when we add these back in it goes `10px` up from the bottom and `200px` over from the left. Same thing if we used `top: 20px;` and `left: 100px`. Keep in mind you can use negative values here. But most of the time you would use `right` and the other value.

Now with `position: relative`, it will stay where we put it. So when we scroll it is going to scroll with the page. It's not going to be removed from the flow of the document.

### `position: sticky`

```css
#box {
  position: sticky;
  bottom: 10px;
  left: 200px;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}
```

`position: sticky` is a mixture of `fixed` and `relative`. When I scroll down, the element will stay where it is. So it will hit the top of `20px` and the left of `100px`. And then it won't go away. And this is actually great for things like navigation bars. If I had a `top: 0;` when I scroll down it's going to just stay there as the window hits the top. So you can imagine if we had some navigation bar we could use `position: sticky;` so as the user scrolls they always have access to that nav bar. But you must be careful not to cover up elements that you don't want to be covering up.

This will act very similar to `position: fixed` once you start scrolling. Once you start scrolling it is essentially a `fixed` element.

We do want to be cognizant of accessibility. Older browsers did not have support for `position: sticky` and you would want to test output on them.

### `position: absolute`

So `position: absolute` has sort of two purposes. Most of the time this is going to act very similar to `position: fixed`. The difference being, that when I scroll, it's actually going to stay where it was on the page.

So rather than being absolutely positioned with respect to the browser window, it is in respect to where it is on the page in the actual document.

However, this isn't always the case. If the parent of a `position: absolute;` element is `position: relative`, or rather anything above it as an ancestor is a `position: relative;`, it will instead position absolute to that `relative` item.

I'll show you what I mean. We remember this `#box` was within this `section`.

So I can do this.

```css
section {
  position: relative;
}

#box {
  position: sticky;
  top: 0;
  left: 100px;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}
```

And now the `#box` will be positioned absolutely to that section. But it is still is absolutely positioned. It's still on the top of the items and still following these `top` and `left` values. Now it's `0px` from the top of the `p`.

### `z-index` Property

Now the next question you might have, what if I want it to not be on top of these other elements?

And the way we can solve this is with __a z-index__.

So I'm going down to `#long` and add a `z-index` property and it says "I want this element to be at some height." So by default, everything's at the same level, at a zero height.

```css
p {
  font-size: 1.75rem;
  margin: 1.5rem;
  padding: 1rem;
  border: 2px solid black;
}

body > p {
  background-color: lightblue;
}

section {
  position: relative;
}

#box {
  position: sticky;
  top: 0;
  left: 100px;
  width: 15rem;
  height: 10rem;
  border: 2px solid black;
  background-color: lightgreen;
}

#long {
  z-index: 2;
  background-color: lightyellow;
}
```

And when I save, you'll notice nothing actually happens. The reason is related to something called stacking contexts. But for now, just know we have to be creating a new stacking context whenever we use `z-index`, and this doesn't happen by default with `position: static` elements so we need to change it.

For now, just know for `position: static` elements, we won't be able to use `z-index` immediately and we'll need to change the position or another property that will create that stacking context for us.

```css
#long {
  position: relative;
  z-index: 2;
  background-color: lightyellow;
}
```

And now you'll see the `p` is on top of `#box`. So I'll add `-20px` to the `#box`.

```css
#box {
  position: relative;
  top: -20px;
  ...
}
```

And you can see the `#box` now peeking out from behind the `p`.

But we can add `z-index` to other elements.

```css
#box {
  position: relative;
  top: -20px;
  ...
  z-index: 3;
  border: 2px solid black;
  ...
}
```

So the `#box` is back on top. But if I change `z-index` of `#long` to be 4, then `#long` is back on top.

### `float` Property

We're going to try something called `float`. The `float` property is very similar to `position` in that it does remove elements from the normal flow. But it allows us to take elements and have them sort of flow around other elements.

Let's come over to `#box` and I'm going to say `float: left;`.

```css
#box {
  float: left;
  top: -20px;
  ...
}
```

Now we see the `p` is wrapping around the `#box`. So what `float` does is it just says __"take this element to push it to one side of its container, in this case the left side, and then allow the elements below it to just wrap around wherever there is empty space on the other side."__ And this is a very powerful tool, especially if you're doing a blog post and you want to have an image in it, but you don't want to image to take up the whole width and you want to float text around the image. And we can do this with multiple items. We can change the first `p` that says "I am a paragraph!" to float right.

```css
body > p {
  float: right;
  background-color: lightblue;
}
```

And now you can see the text is wrapping around both the `#box` and first `p`. And `p` is on the right side because it is floating right. And `#box` is on the left side because it is floating left.


Finally, sometimes you need elements to not be paying attention to `float`. So we can add this property `clear`.

And `clear` allows an element to say __"actually I want to go below whatever is floating".__

`clear: both` says both the elements floated left and right, make sure I am still below them.

```css
#long {
  clear: both;
  background-color: lightyellow;
}
```

`clear: right;` says go below the element that is floating right and if there is something floating left that is bigger we can allow it to float.

`clear: left;` says go below the element that is floating left and if there is something floating right that is bigger we can allow it to float.

However, here `clear: left;` won't do anything because the element on the left is taller than the element on the right. So if we clear the left one we have to clear the right one.

---  

As a closing thought, try to use position sparingly. We don't want to be setting lots of elements to `position: fixed;` and `position: absolute;`
