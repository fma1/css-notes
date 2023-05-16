## Pseudo-Classes and Pseudo-Elements.

__Pseudo-Classes__ are a way to select elements based on their current state in their DOM. For example, we might want to select only inputs that are disabled.

__Pseudo-Elements__ are similar but select only portions of element. First letter or first line of a paragraph, for example.

Let's look at the HTML file.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Pseudo-Classes and Elements</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Hello World</h1>
    <p>
        Go to
        <a href="https://www.google.com">Google</a>
    </p>

    <p>Google is the best!</p>
    <p>Apple is the best!</p>

    <label for="input">Input</label>
    <label id="input" type="text" />
  </body>
</html>
```

### Pseudo-Classes

Pseudo-classes use a colon and then the name of the class.

So we can do `:link` and this will specifically select links which are unvisited, and we can do this on the anchor tag. So let's make the Google text red.

```css
a:link {
  color: red;
}
```

So we click on the link which is red and go back, and the text is now purple. But why is it purple and not red? Because the selector we wrote was on the link pseudo-class and that only selects unvisited links. But we can select ones that are visited.

So there's another pseudo-class `:visited` for visited links.

```css
a:visited {
  color: green;
}
```

And now you'll see the Google text has turned green.

Let's select focused inputs now. Actively used by the user. Normally when clicks on mouse but can be when tabs on keyboard too or other things depending on assistive technologies. Let's change the outline to be blue and a little bit bigger at 2px.

```css
input:focused {
  outline: 2px solid blue outline;
}
```

We might also want to select based on what has been typed in, that currently have invalid input, with `:input`. They are not following the requirements set out in HTML.

```css
input:invalid {
  outline: 2px solid red;
}
```

Let's add a requirement, a minimum length of 6 to the HTML input.

```html
<label id="input" type="text" minlength="6" />
```

And now if we type we get this red outline until we type 6 charactesr. While I was typing, it was red. We don't want it to turn up as red before they're even finished typing. To understand why this is happening, take a look at our CSS. At the top is the `:focus` setting it to blue and `:invalid` below setting it to red. And in the case of a few characters, it is both in focus and invalid so CSS is defaulting to the lower one in the file. We could change the order, but I think a slighter cleaner way to avoid relying on the order is to add another pseudo-class. Pseudo-classes are chainable and we can add the not pseudo-class.

```css
input:invalid:not(:focus) {
  outline: 2px solid red;
}
```

So this says to select inputs that are invalid but are also not in focus. And we can come back and we can say it does not become red while we are typing.

Finally, we can select elements based on their location in the DOM. I want paragraphs but `first-of-type`. It says select the first paragraph of a set of siblings.

```css
p:first-of-type {
    color:orange;
}
```

You'll see the "Go to" text is orange because it's the first paragraph among the siblings that share the same parent. But if I were to add a `<div>` around the latter 2 paragraphs the `Google is the best!` paragraph would also be orange.

We can also say `last-of-type`, which is the exact opposite, the last element in a set of siblings.

```css
p:first-of-type {
    color:orange;
}
```

We can also say `nth-of-type`, which is similar but can be any nth one among siblings.

```css
p:nth-of-type(1) {
    color:orange;
}
```

We can also use `odd`, `even`, `2n-1` in the parentheses for `nth-of-type`.

We also have similar pseudo-classes for children, like `:first-child`, `:last-child` and `:nth-child()`


So this is what we have now.

```css
input:focused {
  outline: 2px solid blue outline;
}

input:invalid:not(:focus) {
  outline: 2px solid red;
}

a:link {
  color: red;
}

a:visited {
  color: green;
}
```

### Pseudo-Elements

Pseudo-Elements use two colons and then the name of the element.

```css
p::first-letter {
  font-size: 2em;
}

p::first-line {
  font-size: red;
}
```

Next I want to look at `::before` and `::after`.

What `::before` is it inserts an invisible element before the content in the beginning of the paragraph being selected. We can use this `content` CSS rule to add some content. So we can maybe add an arrow that points to our content.

```css
p::before {
  content: ">"
}
```

So we see an `>` in the front of each paragraph. You'll notice the content we added with `::before` is actually being applied by the first letter selector.


Finally, `::after` works very similar.

```css
p::after {
  content: "!"
}
```

And you'll see each one gets a new exclamation point.

You might notice that is there a space after `Google` but before `!` and it is because we went onto a newline after the `<a>` so that condensed to a single whitespace. And we would have to make the closing tag of `</p>` together with `</a>` on the same line to avoid that whitespace.
