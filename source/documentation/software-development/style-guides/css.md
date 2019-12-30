# CSS

### Contents

* [Whitespace](#whitespace)
* [Spacing](#spacing)
* [Vendor prefixing](#vendor-prefixing)
* [Sass nesting](#sass-nesting)

### Whitespace

Use soft tabs with a 2 space indent. This follows the conventions we use in our other projects.

### Spacing

You should use the [GOV.UK Design System spacing scale](https://design-system.service.gov.uk/styles/spacing/).

#### Use with deprecated libraries

If your project is not using the GOV.UK Design System, you should use the
[variables from the frontend_toolkit][measurements.scss] or use pixel values in multiples of `5px`.

[measurements.scss]: https://github.com/alphagov/govuk_frontend_toolkit/blob/master/stylesheets/_measurements.scss

#### Include fallbacks for rem spacing

Avoid using `rem` units for spacing.

If you are using the GOV.UK Design System without [compatibility mode](https://github.com/alphagov/govuk-frontend/blob/master/docs/installation/installing-with-npm.md#compatibility-mode) turned on, it will use `rem` units for font sizing with pixel fallback.

This allows users to increase the size of the text on a page by adjusting the font size in their browser settings.

If you do need to use `rem` units, include a fallback for browsers that do not support `rem` units.

```css
font-size: 12px;
font-size: 1.2rem; // This line is ignored by older browsers
```

##### Use with deprecated libraries

You should avoid using `rem` units with [GOV.UK Template](https://github.com/alphagov/govuk_template).

Since GOV.UK Template sets the font size at the root level, sizing with `rem` can be unpredicatable.

### Vendor prefixing

When using CSS features which require vendor prefixes use [autoprefixer](https://github.com/postcss/autoprefixer).

You should [configure autoprefixer](https://github.com/postcss/autoprefixer#browsers) to target [our supported browsers](https://www.gov.uk/service-manual/technology/designing-for-different-browsers-and-devices#browsers-to-test-in).

### Sass nesting

Sass nesting should be avoided where possible.

Over use of nesting can make searching for selectors difficult and can hide complicated CSS that should be simplified.

Exceptions to this include pseudo selectors and JavaScript enabled classes.

```scss
.accordion {
  // styles when the accordion is not enhanced here
}
.js-enabled {
  .accordion {
    // styles when the accordion is enhanced here

    &:focus {
      // ...
    }
  }
}
```
