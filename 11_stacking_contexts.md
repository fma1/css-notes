## Stacking Contexts 

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Stacking Context</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <section>
      <div id="red">Red</div>
      <div id="blue">Blue</div>
    </section>
    <div id="green">Green</div>
  </body>
</html>
```

```css
#red {
  z-index: 1;
  background-color: red;
}

#blue {
  z-index: 2;
  top: 100px;
  left: 150px;
  background-color: blue;
}

#green {
  z-index: 3;
  top: 200px;
  left: 40px;
  background-color: green;
}

div {
  position: fixed;
  width: 200px;
  height: 200px;
  border: 5px solid black;
  padding: 0.5rem;
  color: white;
  font-size: 2rem;
  font-weight: bold;
}
```

So we're going into how `z-index` is actually working. Here we first have a section that contains two divs, red and blue, and then outside the `section` we have the green `div`.

So let's take at the CSS. So each of these `divs` is set to `position: fixed`. And each one we are setting some properties. In `#green`, we give it the background color of green, we set its top and left values, and works because it is `position: fixed` and then we set the `z-index`. So right now red has a `z-index` of 1, blue has a `z-index` of 2 and green has a `z-index` of 3.

And looking at the output, this makes sense. `#green` is on top of `#blue`, and `#blue` is on top of `#red`, and `#green` is also on top of `#red`. If I change the `z-index` of `#red` to 4 then it's on top of both of the other two. But now let's change it back.

Now let's look what is happening when we set these `z-index` values and we use `position: fixed`. Anytime we add `position: fixed`, we create what is called a stacking context. Now this isn't the only way. There's `position: sticky`, `position: relative` with a stacking context, `transform`, etc.

So a stacking context is __a grouping of elements on the z-axes__.

In this case, each one of these is acting as its own stacking context. Because each one of these values, `#red`, `#green`, `#blue` are all `position: fixed` which creates a stacking context for each one. And the `z-index` says how high in the z-axis is the stacking context. So now the `#green` stacking context has a value of 3, the `#blue` stacking context has a value of 2, and the `#red` stacking context has a value of 1.

But what would happen if we went to `section` and created a stacking context here as well? And let's give it a `z-index` of 4, saying this `section` on top.

```css
section {
  position: fixed;
  z-index: 4;
}
```

But now we see `#green` has been pushed all the way to the bottom, even though it has a `z-index` of 3. Shouldn't it be on top of `#red` and `#blue`? Why is `#green` below?

If we go back to the HTML, we have this `section` here and then the `#green` is outside of it. So this entire `section` is a stacking context due to `position: fixed` and `#green` is also a stacking context. And we call these sibling stacking contexts because they are at the same level, not necessarily in the DOM tree, but they are at the same level within stacking contexts, because they are both at the root level, they are the highest level stacking context we have other than the base document stacking context.

And this `section` has a `z-index` of 4. Whereas the `div` of `#green` has a `z-index` of , which means `#green` is below the `section`, because everything inside of the `section`.

The `z-index` of `#red` of `#blue` is only being used to compare them within their stacking context _parent_. And from that, we see `#blue` is on top of red. We can change that, and give `#blue` a `z-index` of -1, and `#red` is now on top of `#blue`. But even with a negative `z-index`, `#blue` is still on top of `#green`, because `#blue`'s parent `section` is a sibling stacking context to the `#green` stacking context and `section` has a higher `z-index` than `#green`. But if we changed `#green`'s `z-index` to 5 then `#green` would be ahead of `#red` of `#blue` even if I gave `#red` a `z-index` of 1000. And the reason is because `#red` is inside of the `section` with the `z-index` of 4, which is lower than green. So the only way `#red` could be ever on top of `#green` is if its parent stacking context had a higher `z-index` than `#green`.  

Now, there are a ton of actual ways to create a stacking context. So if you're running into any bugs related to `z-index`, most likely it's related to the fact that you having more stacking contexts then you think you have or you have less than you think you have.
