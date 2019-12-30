# Choosing a programming language

We use a range of programming languages at GDS because we think
using the right tool for the job gives us the best chance of building
services that best meet users’ needs. This document does not apply to
choosing 'off the shelf' software (open source or not).

We focus on using a small number of programming languages for
core software development tasks.

This should make it easier for developers to:

- move around the organisation
- develop shared components
- improve their personal development
- master how they operate applications

## Frontend development

The Service Manual has information on
[using client-side JavaScript][manual_js]. For server-side JavaScript we use [Node.js][nodejs].


[nodejs]: https://nodejs.org/
[manual_js]: https://www.gov.uk/service-manual/technology/using-progressive-enhancement

GDS projects using Node.js include:

- [GOV.UK Frontend](https://github.com/alphagov/govuk-frontend)
- [GOV.UK Pay](https://www.payments.service.gov.uk/)
- [Performance Platform](https://www.gov.uk/performance)
- [GOV.UK PaaS](https://www.cloud.service.gov.uk/) (TypeScript)
- [Passport Verify](https://github.com/alphagov/passport-verify) (TypeScript)

You can use Node.js to render a web interface for your service, but you should
not use it to implement any significant ‘application logic’. For example,
GOV.UK Pay has created thin, client-facing applications that do not store
data (although they may retrieve data from an API).

You can use [TypeScript](https://www.typescriptlang.org/) when teams think it's
appropriate. For example, the GOV.UK PaaS team uses TypeScript
because they are used to working with a statically typed, compiled language,
and they think the compilation and static-analysis tooling is better for
their workflow. There's more information about TypeScript on the
[Node.js][nodejs] page.

## Backend development

Our core languages for backend development are:

- [Java](https://github.com/alphagov?language=java)
- [Python](https://github.com/alphagov?language=python)
- [Ruby](https://github.com/alphagov?language=ruby)
- [Go](https://github.com/alphagov?language=go)

We've chosen these languages because they are successfully used by
teams at the moment, and we are confident in how to host and operate
applications written in them. You should carry out new
development in one of these languages.

### Python

You should write new Python projects in Python 3.  Python 2 will
[reach end of life in 2020][PEP373]. Python 3 is now well-supported
by application frameworks and libraries, and is commonly used in
production.

[PEP373]: https://www.python.org/dev/peps/pep-0373/

### Go

We built the GOV.UK router using Go, and it's the core language for [Cloud
Foundry](https://www.cloudfoundry.org/), which GOV.UK PaaS uses.

Go is an appropriate language for systems programming, like proxying, routing,
and transforming HTTP requests. However you should only write these sorts of components if there is no alternative maintained open source tool available.

Go has a feature complete standard library, good concurrency primitives and is
a memory safe language. These features make it a good choice for backend
application which aggregate or transform APIs, or have performance
requirements.

### Languages we don't use for new projects

We used Scala in the early days of GDS. GOV.UK Licensing is the only remaining
application written in Scala but we've found it hard to support because of a lack
of skills in GDS. Do not use Scala for new projects.

## Using other languages

There will be sensible reasons to not follow the above guidance on languages.
For example when you're:

- extending an existing codebase or ecosystem
- scripting in a particular environment
- experimenting during an alpha (with an expectation that it's replaced by something we have more confidence in for beta)
- working in a very specific or unusual problem domain, like heavy use of WebSockets

The set of languages we're comfortable supporting will change over time.

If you want to use a new language, talk to your technical architect and the
Deputy Director Technology Operations and then create
a prototype. If it goes well you can [open a pull request](https://gds-way.cloudapps.digital/standards/pull-requests.html) to change this document.

If you're having problems using one of the languages we support, open a pull request to
document the issues.
