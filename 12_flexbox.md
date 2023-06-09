## Flexbox 

Flexbox is a layout system for building responsive websites. What we mean by this is it will allow us to build websites that resize themselves based on the size of the window, creating a great user experience regardless of screen size.

### Flexbox Overview

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Flexbox</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div class="red">Red</div>
    <div class="blue">Blue</div>
    <div class="green">Green</div>
  </body>
</html>
```

```css
section {
  height: 90vh;
  border: 2px dotted black;
}

.red {
  height: 75px;
  background-color: red;
}

.green {
  height: 125px;
  background-color: green;
}

.blue {
  height: 100px;
  background-color: blue;
}

div {
  border: 5px solid black;
  padding: 0.5rem;
  color: white;
  font-size: 2rem;
  font-weight: bold;
}
```

In the HTML, we have 3 `divs`: red, green and blue.

And then in the CSS, the `section` has a height of `90vh`, 90% of the viewport. And a dotted black border. Each of red, green and blue have a different height and the colors for their background color that correspond to their class name

And the `div` has some generic styling for all 3 `divs`. A border of `5px`, padding of `0.5rem`, font stuff, etc.

Flexbox allows us to define a __flex container__ and then __flex items__.

A container will be whatever is surrounding the flex items. To create a flexbox container, we set something to `display: flex`. We set this property on whatever is around the flex items, whatever we want to layout. So I'll do this on the `section`.

```css
section {
  display: flex;
  height: 90vh;
  border: 2px dotted black;
}
```

Because we set `display: flex` on the `section`, it says now all these 3 `divs` are flex items which essentially changes the way all these 3 `divs` will be laid out on the page. It is worth noting here that __this only affects direct children__, if these 3 `divs` had more children, only these 3 `divs` would be made flex items whereas the nested elements are just nested inside that flex item, but they are not necessarily flex items themselves.

So direct children of an element with `display: flex` are flex items and whatever we set `display: flex` to is a flex container. 

So now let's look what happened when I set it to `display: flex`. All of these `divs` are now on one line, and they are no longer stretching the full width of the page and stretching the width of their content and this is sort of the default behavior of flexbox.

But we can go through the different options how we can get different layouts with this, and layout in different places all over the page.

### `flex-direction` property

First, let's look at the direction we are _flexing_ in, as we say.

There is a property `flex-direction` and it defaults to `row`.

So if I save it to this, nothing will change.

```css
section {
  display: flex;
  flex-direction: row;
  height: 90vh;
  border: 2px dotted black;
}
```

`row` says put all the flex items horizontally in a row. However we could change it to `column`.

```css
section {
  display: flex;
  flex-direction: column;
  height: 90vh;
  border: 2px dotted black;
}
```

This says to stack vertically on top of each other. Since this is a `column` layout and only one element per row, these elements have the space to horizontally stretch out to fill up the container.

We could do something like `column-reverse` instead of `column` but it will change the order as well as throwing everything at the bottom. We can do the same thing with `row-reverse` instead of `row` with everything on far right with the `divs` in backwards order.

And the way we refer to this is the __main axis__. So `flex-direction: row` is going to say the main axis is horizontal, which means the main flexing that is happening is horizontal. But if we change this to `flex-direction: column`, we are saying the main axis is the vertical axis. We are flexing vertically. And then we call the other axis that's not the main axis the __cross axis__.

### `justify-content` Property

We can use this property `justfy-content` to say how we want the elements in the axis to be laid out. It starts with `flex-start`.

```css
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  height: 90vh;
  border: 2px dotted black;
}
```

This won't do anything because `flex-start` is the default value. And this says put everything at the beginning of the main axis.

But we could change this to `flex-end` and it will push everything to the right side.

We could also do `space-around` and what this does is evenly space out the elements.

We could also do `space-between` which is similar to `space-around` but it doesn't put any space around the outside elements and they get pushed to the edge of the flex container.

Additionally, we can combine with different flex directions, like `row-reverse`. But we hadn't specified `justify-content`, everything got put to right and maybe we don't want that. So we can change it to `flex-end`. And since we are in `row-reverse`, `flex-end` is now the left side and `flex-start` becomes the right side. And same thing with `column` and `column-reverse`.

```css
section {
  display: flex;
  flex-direction: row-reverse;
  justify-content: flex-end;
  height: 90vh;
  border: 2px dotted black;
}
```

So let's change it to `column`.

```css
section {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  height: 90vh;
  border: 2px dotted black;
}
```

Now with `flex-end`, all of our values end up at the end. All of the values end up at the bottom because `column` is now the main axis, so `justify-content` is controlling how these elements are laid out vertically and we said `flex-end` which is going to be at the bottom.

We could also change this to `column-reverse` and now we're in the reverse and `flex-end` is at the top because we're in reverse order. 

Now let's change it back to row.

```css
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  height: 90vh;
  border: 2px dotted black;
}
```

### `align-items` property

And next, we may want to change this how things are aligned on the cross axis. And we can do this with a property called `align-items`. So `align-items` takes the same values as `justify-content` and also defaults to `flex-start`. So we could say `flex-end`.

```css
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: flex-end;
  height: 90vh;
  border: 2px dotted black;
}
```

And you'll see all the items moved down to the bottom of the flex container because we are now on the cross axis going all the way to the end. We could also use `center` for both `align-items` and `justify-content`. So this is a really way to center things. Centering things in a CSS can be a pain and an easy way is to just set `display: flex` and `justify-content: center` and `align-items: center`. And that will immediatelly center all the flex items of that flex container.

```css
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: flex-end;
  height: 90vh;
  border: 2px dotted black;
}
```

### `gap` Property

You might notice there's no space between these properties and we wanted them all centered but we might want some space between them. And there's a property for that called `gap`. And `gap` is just that, the space between items. It's almost the same thing as `margin`. It's just that it's specific to flexbox, and it's the gap between flex items rather than setting it on single flex item. It's a little bit more automatic. If we want the same spacing between flex items, `gap` is the easier way to go for that.

```css
section {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: flex-end;
  gap: 10px;
  height: 90vh;
  border: 2px dotted black;
}
```

### `flex-wrap` Property

And next, what I want to look at it if we have more items flexing than 3.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Flexbox</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div class="red">Red</div>
    <div class="blue">Blue</div>
    <div class="green">Green</div>
    <div class="red">Red</div>
    <div class="blue">Blue</div>
    <div class="green">Green</div>
    <div class="red">Red</div>
    <div class="blue">Blue</div>
    <div class="green">Green</div>
  </body>
</html>
```

So now we have 9 flex items. And you can see we're out of space and we have a scrollbar on our website but we probably don't want this. It's overflowing from our flex container.

And the way we can control this is with `flex-wrap`. `flex-wrap` defaults to `nowrap` which is what we are seeing right now which is overflowing. 

```css
section {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  align-items: flex-end;
  gap: 10px;
  height: 90vh;
  border: 2px dotted black;
}
```

But we can change this to `wrap` and this will instead go to a new line when it runs out of space. We can also do `wrap-reverse` which works very similar to `row-reverse` in that we get the wrap effect but we will get in reverse order. So every new line we go to will happens in backwards order.

Now let's go back to `flex-wrap: wrap` and you can see it's just going to a new line when it runs out of space.

### `flex-flow` Property

We can specify `flex-direction` and `flex-wrap` with one property and that is `flex-flow`. It's just a shorter syntax.

```css
section {
  display: flex;
  flex-flow: row wrap;
  justify-content: flex-end;
  align-items: flex-end;
  gap: 10px;
  height: 90vh;
  border: 2px dotted black;
}
```

### `align-content` Property

Now that we have multiple rows, we need a way to determine how close the rows are together. We initially used align-items for this purpose but as you can see when we have a `flex-wrap`, `align-items` will only align items within their individual row.

And if we change `align-items` from `center` to `flex-start`, everything gets pushed to the top of the rows, but it doesn't change how rows are aligned to each other.

The way we can change this is `align-content`. It could be `center` and this will be put the rows all the way in the center. We could say `space-between`, and will add some space between them. `space-around` willadd space around them, etc.

```css
section {
  display: flex;
  flex-flow: row wrap;
  justify-content: flex-end;
  align-items: flex-end;
  align-content: space-around;
  gap: 10px;
  height: 90vh;
  border: 2px dotted black;
}
```

### `order` Property

Now that's pretty much everything to flex containers. Sometimes we need to change how a single flex item is aligning in the group. Maybe we want one of them to do something different from something else. And there's something we can set on the flex items themselves.

And the first property we can look at is `order`. And it says where in the order do we want this to be. By default this is the order in the DOM. I could make this -1 when 0 is the default.

```css
.red {
  order: -1;
  height: 75px;
  background-color: red;
```

And when I save this, all the red ones get pushed to the beginning because they have a value of -1 which is less than the value of everything else.

We could set this to `1` and red is going to end up all at the end because the default value of `order` is 0 for all flex items.

### `flex-grow` Property

`flex-grow` says is if there's extra space, how much of it should this element take up? This defaults to 0, meaning nothing will take up extra space, which is why we saw initially everything was condensed to size of its content.

When I set this to `flex-grow: 1`, when there is extra space, the red elements will take up that space.

```css
.red {
  order: 0;
  flex-grow: 1;
  height: 75px;
  background-color: red;
```

So on the first line there is no extra space for the red elements to take up so they're not changing. But on the second line there's lots of whitespace. `flex-grow` said I have `flex-grow: 1` but the others don't have any `flex-grow` so just let red take up all the space. You'll notice `flex-grow` has no unit because these are just proportions. Because if I said green was also `flex-grow: 1`, then red and green will take up equally the extra space. But if I said green was `flex-grow: 2`, then red is going to take up of the extra space that green is taking up because of that proportion of 1:2.

### `flex-shrink` Property

`flex-shrink` says whether or not this element is able to shrink. It defaults to 1, which says it's able to shrink. I'm going to give green a `width`.

```css
.green {
  width: 100vw;
  height: 125px;
  background-color: green;
}
```

Now you'll see green isn't taking up `100vw`. It's just taking up the size of the parent. But if we change the `flex-shrink` value to 0, we'll see it goes back to `100vw` and overflowing from the flex container.

```css
.green {
  width: 100vw;
  flex-shrink: 0;
  height: 125px;
  background-color: green;
}
```

### `flex-basis` Property

Finally, we have this property `flex-basis`. I'm going to change the `width` to `flex-basis`. It means the same thing as `width` when we have `flex-direction: row`. This is how much I want space to take up in whatever the main axis direction is.

```css
.green {
  flex-basis: 100vw;
  flex-shrink: 0;
  height: 125px;
  background-color: green;
}
```

So if this was changed from `flex-direction: row` to `flex-direction: column`, then the green elements would get `100vw` in height. But if we go back to `row`, it's `100vw` in `width`.

### `flex` Property

There's a shorthand for these properties, in the order of `grow`, `shrink` and then `basis`.

For example, we can say this is going to have a `flex-grow` of 1, a `flex-shrink` of 0 and a `flex-basis` of `200px`.

```css
.green {
  flex: 1 0 200px;
  height: 125px;
  background-color: green;
}
```

So now we can see these properties interacting with each other. `flex-grow` of 1 means allow the green elements to grow if there's available space. `flex-shrink` of 0 says they cannot shrink down to a smaller size than their `flex-basis` of `200px`. And since there's more there `200px` in each of our rows, this is our allowing our green element to grow beyond `200px` in each row. 

However, we change the `flex-basis` to 2000px, I can grow if there's even more space even more that, and I am not allowed to shrink. Because there's no room to grow and not allowed to shrink, the green elements will show up as `2000px` and be overflowing from our flex container. But if we change `flex-shrink` to 1, it shrinks down back to the size of the flex container. But let's move it back to `200px`.

That's really it. That's really all of the Flexbox properties. It's a bit of a learning curve of thinking in Flexbox and thinking of what elements need to be flex containers and which elements need to be flex items, and then which flex properties do we need to set to get elements to layout exactly how we want them to. However, it's a super intuitive way to layout pages and it's a great way to get responsive websites because things are just going to flow and flex and sizes will change based on space on screen. So everything tends to work really well.
