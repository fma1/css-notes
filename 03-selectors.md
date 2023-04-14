## Selectors  

### Selector Overview

So here we have a HTML file and it's pretty simple. At the top we have a top-level heading. We have a section with a section heading a section paragraph. And then we have a footer also with an h2 and a paragraph.

Finally we linked a CSS stylesheet.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Selectors</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Top Level Heading</h1>

    <section>
      <h2>Section Heading</h2>
      <p>Section paragraph</p>
    </section>

    <footer>
      <h2>Footer Heading</h2>
      <p>Footer paragraph</p>
    </footer>
  </body>
</html>
```

Let's open that CSS file.

### Type Selectors

So first of all, the most basic selector is a type selector, what tag you want to select.

```css
h1 {
  color: red;
}
```

Now you'll see the top-level heading becomes red. Additionally we can select multiple elements this way.

```css
h1, h2 {
  color: red;
}
```

And now all the headings are red. This isn't limited to similar elements either.

```css
h1, h2, p {
  color: red;
}
```

### Universal Selector

Now if we wanted to select everything, we can use `*`, or the universal selector. But I would not recommend it because it will select every tag and it may not be what you want. And we don't need the title or link tag to be red, which it's also selecting.

```css
* {
  color: red;
}
```

### Class Selectors

What if we wanted to be more specific and select the `h1` and then the section paragraph? Most common is by using CSS classes or the HTML class attribute.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Selectors</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1 class="red">Top Level Heading</h1>

    <section>
      <h2>Section Heading</h2>
      <p class="red">Section paragraph</p>
    </section>

    <footer>
      <h2>Footer Heading</h2>
      <p>Footer paragraph</p>
    </footer>
  </body>
</html>
```

Now in our styles.css, we'll switch to class selector which uses `.` and then the name of the class.

```css
.red {
  color: red;
}
```

We could also the comma with this.

```css
.red, h2 {
  color: red;
}
```

### ID Selectors

What if more specific? Just make one single element red. Only the section paragraph. We could give it a class of red and get rid of red class from h2 but probably not the best thing to have classes that exist once. We can use the id attribute.

`<p id="red">Section paragraph</p>`

And for id, we use the `#` sign in CSS.

```css
#red {
  color: red;
}

h1 {
  color: blue;
}
```

So mainly we'll use classes and ids 90%+ of the time.

Let's go to our HTML and add a link. Let's add an anchor tag. Actually 2 anchor tags. One link to Google and one link to LinkedIn.

```html
<html>
    <section>
      <h2>Section Heading</h2>
      <p>Section paragraph</p>
      <a href="https://www.google.com">Google</a>
      <a href="https://www.linkedin.com">LinkedIn</a>
    </section>
</html>
```

So now we have a link to Google and LinkedIn. What if we wanted to style the links? We can use the `a` tag.

```css
a {
  color: green;
}
```

But this styles all the links. 

### Attribute Selectors

But what if we only to affect certain links? One thing is we could do thing is by class or id, but another way is an attribute selector using `[]` next to the type.

```css
a[href="https://www.google.com"] {
  color: green;
}
```

And now you can see the style is only affecting the Google link. Now most of the time with attribute selectors, this is all you need. You have some attribute and some value for that attribute.  

But sometimes we do want to be even more specific with this. But if we had another google link, but that goes to the images page?

```html
<html>
    <section>
      <h2>Section Heading</h2>
      <p>Section paragraph</p>
      <a href="https://www.google.com">Google</a>
      <a href="https://www.google.com/images">Google</a>
      <a href="https://www.linkedin.com">LinkedIn</a>
    </section>
</html>
```

Now you'll see this one is blue. It's not getting the green text. Because it's `https://www.google.com/images`. We can had the little caret. Don't just select `https://www.google.com` but anything that starts with it.

```css
a[href^="https://www.google.com"] {
  color: green;
}
```

Also do note you don't necessarily need the `a` there if you wanted that specific attribute for all tags.

### Combinators

I want to go back to what we said about classes. The classes worked. Allows us to select more specific elements but it would get complicated and it would get hard to follow. Good in some scenarios, but bad in others. We want selectors that follow some criteria, called combinators. Combinators use the context of the elements in the DOM as to whether apply the rules.

What if we want to select section paragraph but not the footer paragraph? We can do this through the descendant combinator.

```css
footer p {
  color: red;
}
```

What this says is looks for footers and then look for paragraphs inside footers.

Let's go to our HTML and change it a bit for demonstration purposes.

```html
<html>
    <footer>
      <h2>Footer Heading</h2>
      <p>Footer paragraph</p>
      <div>
        <p>Footer paragraph</p>
      </div>
    </footer>
  </body>
</html>
```

So both divs are now red. Now this CSS may be what we want, but it may be not what it want.

If we want direct children of `footer` to be red, we can add a `>` and this is known as a child selector.

```css
footer > p {
  color: red;
}
```

So now only the first `p` is red because it's a direct descendant of `footer`.

Now the final set of selectors I want to talk about sibling selectors. Siblings share a parent element. For example, all 5 of the elements under `section` could be considered sibling elements. Adjacent siblings are siblings that are directly next to each other. We can select for both of these things.

We can do something like this.

```css
h2 ~ p {
  color: red;
}
```

This says get any `p` that is a sibling of an `h2`

We can change this to be an `a` is a sibling of an `h2` and we see all anchor tags be red.

```css
h2 ~ a {
  color: red;
}
```

Now for adjacent siblings we can change `~` to `+`.

```css
h2 + a {
  color: red;
}
```

Now none of them are red because none of the anchor tags are adjacent to the h2, but we can comment out the section paragraph.

```html
<html>
    <section>
      <h2>Section Heading</h2>
      <!-- <p id="red">Section paragraph</p> -->
      <a href="https://www.google.com">Google</a>
      <a href="https://www.google.com/images">Google</a>
      <a href="https://www.linkedin.com">LinkedIn</a>
    </section>
</html>
```

And now the first `a` is red but not the other two because they are not adjacent to an anchor tag.

### Outro

That's going to be the final CSS selector, and that should cover the vast majority that you'll see, and other selectors you'll see are combinations of what you've seen, and more complex versions of them.
