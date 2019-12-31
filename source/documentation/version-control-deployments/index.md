# Version control and deployments

At GDS, we follow the principles set out in the Service Manual for managing the code we write by:

- [using version control](https://www.gov.uk/service-manual/technology/maintaining-version-control-in-coding)
- [making source code open](https://www.gov.uk/service-manual/technology/making-source-code-open-and-reusable)

## Publish open source code

Wherever possible, we [make our source code open and reusable][]. This means other government departments and people in outside organisations can benefit from our work. We also maintain several open source projects developed for use on GOV.UK and with other work we do, such as the [Puppet module for go-audit][] or the [GDS Operations open source web site][].

It’s not always appropriate to open code. There are situations [when you should keep some data and code closed][], for example:
- keys and credentials
- algorithms used to detect fraud
- code or data that makes clear details of unannounced policy

The Service Manual explains [how to open previously closed code and your responsibilities for maintaining open code][].

When you publish open source code, your project must:

* include a README, using [guidance for writing a README][]
* have useful and informative commit messages about why a change was made
* provide a changelog, for example the [specification for CPAN Changes files][]
* include an MIT and OGL licence file
* link to a public list of known issues and bugs, for example [GOV.UK frontend toolkit][]
* have an email address to submit security related bug reports
* list a version number compatible with [Semantic Versioning][]

Your open source code project should:

* publish packages to relevant language specific repositories such as [PyPI - the Python Package Index][] or [RubyGems][]
* post contributors' guidelines in a contributing file, like the [Go repository][]
* set up any tests to run in a public continuous integration environment using tools such as [Travis CI][], [CircleCI][] or [Jenkins][]

You could also provide a mailing list so people can discuss your project.

## More in this section

- [how to store source code](source-code)
- [using Pull Requests](pull-requests)
- [writing READMEs](readme-guidance)
- [Licensing](licensing)
- [use continuous delivery](continuous-delivery)

[make our source code open and reusable]: https://www.gov.uk/service-manual/technology/making-source-code-open-and-reusable
[Puppet module for go-audit]: https://github.com/gds-operations/puppet-goaudit
[GDS Operations open source web site]: https://github.com/gds-operations/gds-operations.github.io
[Specification for CPAN Changes files]: https://metacpan.org/pod/CPAN::Changes::Spec
[Semantic Versioning]: https://semver.org/spec/v2.0.0.html
[PyPI - the Python Package Index]: https://pypi.python.org/pypi
[RubyGems]: https://rubygems.org/
[Travis CI]: https://travis-ci.org/
[CircleCI]: https://circleci.com/
[Jenkins]: https://jenkins.io/
[Go repository]: https://golang.org/CONTRIBUTORS
[when you should keep some data and code closed]: https://www.gov.uk/government/publications/open-source-guidance/when-code-should-be-open-or-closed
[how to open previously closed code and your responsibilities for maintaining open code]: https://www.gov.uk/service-manual/technology/making-source-code-open-and-reusable
[Go repository]: https://golang.org/CONTRIBUTORS
[guidance for writing a README]: /version-control-deployments/readme-guidance
[GOV.UK frontend toolkit]: https://github.com/alphagov/govuk_frontend_toolkit/issues
