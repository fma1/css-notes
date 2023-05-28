## Box Model

Today we're going to be talking about the Box Model, which explains how elements are displayed on the page, specifically using `margin`, `border` and `padding` and the content of those elements.

So let's take a look at the HTML and CSS.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Box Model</title>
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
  margin: 24px;
  padding: 10px;
  border: 2px solid black;
  background-color: light-blue;
}
```

So what's actually happening here? We can see in the Inspector we have our two paragraphs and we can hover over them and see the values. And we can see all the different values we've set.

So in the middle here we see the __actual content__ and just wraps the content of the paragraph and goes all the way to the end of the element because it's a block parent.

And then directly outside of the element we have __the padding__, and that's `10px` because that's what we set. And this is space in-between the content and the edge, or the border. So this is sort of space is like inside of the content in the sense the background is still there so it still gets the blue background color but it's outside of the content, as it's just before the border.  

And then we have the __border__, which is that `2px solid black`.

And then we have the __margin__, which says this is the minimum space that I want between me and other elements. I say minimum before even though both of these paragraphs have `24px` margin, they are only `24px` away from each other. Those margins aren't adding together. And the way this works is called collapsing margins. So with vertical alignment, the margins will collapse, so we will just use whatever margin is bigger. However, with horizontal margins that actually doesn't happen and the margins will add up together.

### Margins

One of the first things you might notice is we've set the margin to be `24px` and this is affecting every direction. And we can hit this little arrow to see all the individual values, `margin-top`, `margin-right`, `margin-bottom`, `margin-left`.

So I'll disable the `margin` and the paragraphs get a little bit closer but still a little bit of margin coming from the user stylesheet which is `1em`.

Perhaps we can say `margin-bottom: 48px`. Now you'll see this is pushing the 2nd paragraph down. Or we can say `margin: 48px 24px 0 10px`. The order is top right bottom left. This is clockwise, starting from 12 o'clock. 

We could also define margins as just vertical and horizontal and say `margin: 48px 24px`. What this says is `24px` of right and left and `48px` of top and bottom. 

Finally we can also say `margin: auto`. Just allows the browser to make a decision and will often default to 0. And now you can see the paragraphs are touching each other.

But what we can also do with `margin: auto` is use it to _center elements_ by adding a `width: 30%` but if we remove the `margin: auto` the element will not be centered.

```css
p {
  margin: auto;
  padding: 10px;
  border: 2px solid black;
  background-color: light-blue;
  width: 30%;
}
```
So often you'll see `margin: 24px auto;` to say we want `24px` of margin and then we want to center the element. And that's a good way to get an easy simple layout that works with.

And there's one trick with margin. And that is to set a __negative margin__.

```css
p {
  margin-left: -10px;
  padding: 10px;
  border: 2px solid black;
  background-color: light-blue;
  width: 30%;
}
```

This is going to shift the element `10px` to the left. So while positive margin generally pushes elements away, negative margin pulls it closer to the elements on the side of it. And when I disable this it moves it to the right.

We usually want to avoid using negative margins too much because it can create some weird effects in our layout but they can be nice occasionally.

Finally, let's take a look at this inline emphasis tag. And let's set a margin of `24px`. Now you'll see the horizontal margin is working and pushing the text away and the word paragraph moved to a new line. But it's not pushing anything the vertical. And when I highlight the `em` you don't even see the vertical margins. The reason is because vertical margins have no effect on inline elements. And this is true of padding as well.

### Padding

Let's go back to `p` and talk about padding. Padding works very similar to margin but the primary difference is the space goes inside the border rather than the outside of the border. So padding's purpose is to push the element away from other elements. Its purpose to push the border farther away or closer to the other.

Padding works similarly with `padding-top`, `padding-right`, `padding-bottom` and `padding-left`.

It's worth pointing out that not everything works the same.

Padding can not take a negative value. If I say `padding: -10px`, it's just going to give this yellow warning to tell me this is an invalid property.

### Borders

Finally let's take a look at how we can edit the border. If we disable the border, the black border goes away. There's not much to the border. 

You can set one direction, with padding and margin. So I could say `border-top: 2px solid red`. And we could set different borders on different sides. So I could say `border-bottom: 2px solid black`. And now we have the black border on the bottom and the red border on the top.

We also have `border-radius`, which allows us to add curvature to the outside element. I can say `border-radius: 10px`, and we get a niced curved edge to these paragraphs instead of the sharp corners. And we can also set it to a percentage. Since the radius is half the diameter in a circle, setting `border-radius: 50%`, this says we want a circular shape. And if this was a square, it would be a circle. So if I gave this a width and height of `300px`, you'll see that now we have actually have an exact circle. Again, the radius is half the diameter.

```css
p {
  border-top: 2px solid black;
  border-bottom: 2px solid black;
  border-radius: 50%;
  padding: 10px;
  background-color: light-blue;
  width: 300px;
  height: 300px;
}
```


Now you'll notice the text is actually no longer inside of the circle. And the reason is we still use the box model. This is still a box even though it looks like a circle. If I hover over the paragraph, you'll see the shape of the content is rectangular but the border is a circular shape.

For now, I will get rid of `border-radius`.

```css
p {
  margin: 24px;
  padding: 10px;
  border: 2px solid black;
  background-color: light-blue;
}
```

So to recap, let's take one last look at the last model. Inside the middle, we have the content. And then outside the content, we have the padding. Space between element and border, and background colors will affect this because the background color affects things inside the border. And then we have the border, which is the edges. We can set the top and right differently and set the radius. And finally we have the margin, which defines the space between two different elements. With vertical spacing, this is going to be collapsed, whereas with horizontal spacing it will add the margin values together.

And that's all there is to the box model. Very straightforward but a powerful way to layout our elements.
