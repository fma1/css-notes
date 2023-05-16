## Selector Specificity

What happens to Conflicting Declarations?

```css
a[href="https://www.google.com"] {
  color: green;
}

section.links a {
  color:red;
}
```

__Specific Selectors Win__
- The most "specific" selector is used
- Defaults to the last rule in the stylesheet

### Calculating Specificity

- Inline: 1000 points
- IDs: 100 points
- Classes: 10 points
- Pseudo-Classes: 10 points
- Attributes: 10 points
- Elements: 1 point
- Pseudo-Element: 1 point

Now let's look back at the example. With the first selector, we first have the `a` element, so 1 point. We have the `href` attribute and attributes have 10 points. `1 + 10 = 11 points`.

We look at the second selector. It starts with `section` element, so 1 point. We have the `links` class, which is 10 points. And the `a` element is 1 point. `1 + 10 + 1 = 12 points`.

And that's all there is to it. The second selector wins in terms of specificity because it has a higher score.

### `!important` Rule

- Overriding specificity
- Avoid using if possible

This says specific selectors should be used regardless how specific the selector is.

This goes after declaration but before the semicolon. 

```css
a {
  color: orange !important;
}
```

This can also override a user stylesheet if it doesn't use `!important`. Normally this is considered an anti-pattern because we are overriding the cascading nature of CSS, but there are exceptions. For example if we are using a library we might want to use `!important` to override a declaration from the library without worrying about the specificity of that rule.
