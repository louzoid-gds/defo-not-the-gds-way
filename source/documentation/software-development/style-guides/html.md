# HTML

### Browser support

The GOV.UK Service Manual lists the [minimum browsers that GOV.UK services are required
to support](https://www.gov.uk/service-manual/technology/designing-for-different-browsers-and-devices#browsers-to-test-in).
Tools such as GOV.UK Frontend, that are used to help build services, may have
[stricter standards of browser support](https://github.com/alphagov/govuk-frontend#browser-support).
Therefore, you will need to test your code in different browsers depending on
which part of GDS you are working in.

Whatever your level of browser support, HTML should be written in such a way
that older browsers see an appropriate fallback or warning message. For example,
some browsers do not support the `<video>` element, so you should ensure that
some contextual information is included (the `<p>` element in this example):

```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  <p>Unable to load video. Please upgrade your browser.</p>
</video>
```

When using HTML5 elements such as `<main>`, ensure that you include a
[shim that allows them to be styled](https://github.com/aFarkas/html5shiv) in
legacy browsers. Include the script inside a `<!--[if lt IE 9]><![endif]-->`
conditional comment so that modern browsers do not download them.

Your page should work with just HTML, before adding any CSS or JavaScript. Read
[building a resilient frontend using progressive enhancement](https://www.gov.uk/service-manual/technology/using-progressive-enhancement).

### Document structure

Use HTML5 to structure your page semantically. Use ARIA roles to help
older assistive technologies map the sections correctly.

Léonie Watson explains [why using ARIA landmark roles in this way delivers the
best experience for screen reader users](http://tink.uk/screen-readers-aria-roles-html5-support/).

This document doesn't prescribe whether to use single or double quotes in attributes,
whether to omit values from attributes that don't need them or whether to add
trailing slashes to void elements. However, the approach you adopt should be
consistent throughout your code.

#### Header

`<header role="banner">` should be used to contain your home link, branding, search,
and any global navigation you may have.

#### Main content

`<main role="main">` should be used to identify the main content of your page.

A "Skip to main content" link should be added to help screen reader and keyboard
users skip past your general site navigation and get straight to the content.
You can use the [GOV.UK skip link component from the design system](https://design-system.service.gov.uk/components/skip-link/)
for this.

#### Sectioned content

Use the `<section>` tag to represent standalone, thematic groupings of content
where a more specific semantic element would not be appropriate.

Examples of sections would be chapters, or various tabbed pages in a tabbed dialog box,
or a home page split into sections such as introduction, news items and contact information.

You should add an `aria-labelledby` attribute linking to the id of the heading
that identifies that section.

Example:

```html
<section aria-labelledby="introduction">
    <h1 id="introduction">Introduction</h1>
    <p>People have been catching fish for food since before recorded history...</p>
</section>

<section aria-labelledby="equipment">
    <h1 id="equipment">Equipment</h1>
    <p>The first thing you'll need is a fishing rod or pole that you find comfortable
    and is strong enough for the kind of fish you're expecting to try to land...</p>
</section>
```

#### Navigational elements

Use `<nav role="navigation">` to wrap groups of links that aren't already in
another context (e.g. `<footer>`). Common examples of navigation sections are
menus, tables of contents, and indexes.

As with `<section>`, it is advisable to use `aria-labelledby` to label your `<nav>`.
This helps to distinguish different `<nav>` blocks in the page.

The GOV.UK blog has [more information regarding the use of the `<nav>` tag](https://insidegovuk.blog.gov.uk/2013/07/03/rethinking-navigation/).

#### Aside

`<aside role="complementary">` should be used for content related to the primary content
of the webpage, but which does not constitute the primary content of the page.

Examples include author information, related links and related content.

##### Footer

`<footer role="contentinfo">` should be used for the footer of the site.

### Individual element guidance

#### Headings

Headings should be in order - for example `<h1>` then `<h2>`, but not `<h1>` then `<h3>`.

There should only be one `<h1>` element in a page.

#### Text emphasis

Italics should be avoided according to the [GOV.UK content style guide](https://www.gov.uk/guidance/style-guide).
Bold can be used sparingly, but can make large blocks of text difficult to read.

Semantically, words voiced with emphasis can be marked up with `<em>`, whereas
words conveying a sense or urgency or warning should be marked up with `<strong>`.
In theory, screen readers could adopt a different tone of voice for this markup,
though none of the major ones currently do. Browsers traditionally render these
in italics and bold respectively, so you may need to override `em` to not use italics.

As a rule, avoid using `<i>` or `<b>`, which are only useful in rare cases. It
is usually better to use the `font-style` and `font-weight` CSS properties.

#### Images

Read the [Design System's Images section](https://design-system.service.gov.uk/styles/images/).

#### Buttons vs Links

Links should be used for navigating to another page. Buttons should be used for submitting forms
or interactions within the page (for example, expanding an element). Empty links (`<a href="#">`)
should therefore be avoided.

Links should not open new tabs or windows by default, but if users choose to to so (via keyboard
shortcuts or right-click context menu) then we should respect their choice.

#### Visually hidden elements

Sometimes it can be helpful to provide additional content for screen reader users
that might not be needed for sighted users. For example, the 'Skip to main content'
link covered earlier.

Do not use `display: none` on this text, as this will get ignored by screen readers.

Instead, use CSS which ensures the text gets 'conceptually' rendered, even if the result
is not visible on the screen. You can use the
[Sass mixins from govuk-frontend](https://github.com/alphagov/govuk-frontend/blob/master/src/govuk/utilities/_visually-hidden.scss).

Visually hidden text is often a sign that something can be simplified or made visible to
benefit sighted users too, so should be used sparingly.
