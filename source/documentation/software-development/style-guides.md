# Programming language style guides

You should read this guide alongside the
[programming language recommendations](../choose-a-programming-language).

## Code style guides

Developers read code much more often than they write it. These guidelines
are intended to improve the readability of code and make it consistent
across GDS projects.

A style guide is about consistency. Consistency with this style guide is
important. Consistency within a project is more important. Consistency within
one module or function is most important.

But most importantly: know when it's ok to be inconsistent. Sometimes the style guide
just does not apply. When in doubt, use your best judgement. Look at other
examples and decide what looks best. And do not hesitate to ask if you're unsure.

Some good reasons to ignore a particular guideline include:

- when applying the guideline would make the code less readable, even for
  someone who is used to reading code that follows this style guide
- to be consistent with surrounding code that also breaks it (maybe for
  historic reasons) -- although this is also an opportunity to clean up the
  existing code
- when the code in question is older than the introduction of the guideline and
  there is no reason to modify that code
- when the code needs to remain compatible with older versions that
  do not support the feature recommended by the style guide

We've got a consistent style for:

- [CSS/Sass](css)
- [Docker](docker)
- [Go](go)
- [HTML](programming-languages/html.html)
- [Java](programming-languages/java.html)
- [JavaScript](programming-languages/js.html)
- [Node.js](programming-languages/nodejs/)
- [Python](programming-languages/python/python.html)
- [Ruby](programming-languages/ruby.html) (tested with [RSpec](../standards/testing-with-rspec.html))

Some of the guidelines in the style guides are codified in a
[.editorconfig](editorconfig) file. Place a copy of this
file in your project’s repository to have tooling that supports
[EditorConfig](http://editorconfig.org/) automatically meet the
guidelines.
