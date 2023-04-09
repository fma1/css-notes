## CSS Basics

CSS stands for Cascading Style Sheets.

There are primary purposes of CSS:

1. __Style__ our websites by adding colors fonts
2. Describe the __layout__ of how we want our website to presented such as size and positioning of elements

### Cascading

The Cascading part of CSS represents the order of which browser decides between stylesheets.

There are 3 main types:

1. User-Agent stylesheets defines browser defaults
2. User stylesheets contain user saved preferences in the browser which override the User-agent stylesheet
3. Author stylesheets contains the CSS that the author of the website writes and take precedence over all other stylesheets

### Declarations


CSS is a collection of declarations which is just a bunch of property-value pairs.

`property: value;`

`color: red;`

### Ruleset

Next we need a way to tell CSS what elements we want to style. And we do that by including our declaration in a ruleset.

The ruleset has two parts:

```css
h1, p {
    color: blue;
    margin: 10px;
}
```

1. The selector, which states what elements should be affected by this ruleset.
2. Declarations, which we have already seen.

### Comments

```
/* This is a comment */
```

Can be one or multiple lines but always use this same syntax.

### Linking to HTML

Through the link tag, which goes in the head since it does not affect the actual markup of the page. Takes 2 primary attributes. It takes the `rel` or relationship document, and this is stylesheet for CSS. And next is `href` and works like other `href` attributes. It is the path to the CSS file, relative or absolute.

`<link rel="stylesheet" href="styles.css" />
