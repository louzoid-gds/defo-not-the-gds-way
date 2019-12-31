# Python

This manual is designed to aid developers in writing Python code that is clear
and consistent, within, and across, projects at GDS.


### Code formatting

We follow [PEP 8][]; where [PEP 8][] doesn't express a view (e.g. on the usage of
language features such as metaclasses) we defer to the [Google Python style guide][GPSG].
Use these as references unless something is explicitly mentioned here. As
always these rules should be followed only in conjunction with the advice on consistency
on the main [programming languages manual page][gds-way-code-style-guides].

If you want to add a new rule or exception please create a pull request against this repo.


### Maximum line length of 120 characters

[PEP 8] dictates a preferred maximum line length of <= 79. This is is a hangover from
developing in a Unix terminal window. The vast majority of developers are now using an
IDE which can handle a greater line length comfortably.

Couple this with the fact that much of the time GDS developers are coding web apps and
have to deal with nested `JSON` objects, ORM model definitions/ queries, and error/ url
strings and this convention begins to show its age.

```
# Don't do

if not models.Address.query(
    models.Address.street_address_line_1
    == user['address']['street_address_line_1']
):
    pass


# Do

if not models.Address.query(models.Address.street_address_line_1 == user['address']['street_address_line_1']):
    pass
```


### Linting

_For more on linting (including standard settings and config) see the [linting][] section of this manual._

[Flake8][] is the preferred linting tool. It incorporates:

* [PEP 8][] inspired style checks using [pycodestyle][]
* [Complexity][WikiCyclomatic_complexity] checking using the [McCabe project][McCabe]
* Lint checks using [Pyflakes][]


### Dependencies

A Python application project typically brings together Python packages from PyPI, with
others written in-house (or otherwise not distributed via PyPI).

These packages are the applications immediate dependencies. Additionally, any
package can have its own immediate dependencies, where they draw on other
packages. From an application's point of view, the dependencies of the packages
it requires are its sub-dependencies.

The below diagram shows a simplified view of the resulting pyramid of dependencies;
however it is important to note that the hierarchy can repeat itself infinitely.

```
                               Application

                                    |
                              +-----+-----+
                              |     |     |

                          Immediate dependencies

                              |     |     |
                        +--+--+--+--+--+--+--+--+
                        |  |  |  |  |  |  |  |  |

                         ... Sub-dependencies ...
```

There are two ways of specifying dependencies in Python world: as a specific version or
as an allowable range.

Different considerations apply to dependency management depending whether you are packaging a library, or creating
an end-product such as an application or a bundle of scripts. In general, you should only specify specific versions
when creating a Python system that sits at the top of the dependency pyramid; otherwise there is a danger of creating
version conflicts.

#### Applications

These recommendations apply wherever you need a reproducible set of dependencies, such
as a complete web application, perhaps with many dependencies and sub-dependencies. It also
applies to a collection of scripts that are deployed into the cloud and run automatically
(for example, batch jobs).

A good strategy for specifying your application's Python dependencies has two desirable
characteristics - they should be:

1. Reproducible (predictable)

    Pin your application's full dependencies – specific versions, rather than ranges – or you'll
    get unpredictability between your dev environment and other environments. You want a
    new starter to avoid small hard-to-spot problems. And you want parity between what you
    test locally, what is tested by CI, and what you deploy, or you risk new issues appearing on
    a live server. Additionally these things can be hard to diagnose.

2. Kept up-to-date

    Security issues are found in libraries, so it is important to choose libraries that are
    maintained and to ensure your team has a strategy to ensure security updates are installed
    without significant delay. The [how to manage third party software dependencies][gds-way-deps] section
    gives further context and discusses tools that can help, such as [snyk.io][].

Your README should document an easy-to-follow process by which all your Python
dependencies can be upgraded to get bug fixes and security fixes, without introducing
breaking changes to your build.

Your pinned dependencies should be fully specified in a file called `requirements.txt`, and checked
into your version control system (VCS). For projects with only a small number of dependencies, maintaining
this manually (for example, installing with `pip install`, then using `pip freeze`) may be adequate.

For larger projects, GDS recommends the following approach, which was developed after various issues
were found in current mainstream tooling (see [this commit message][dm-deps-commit], and note also the
[lack of support for specifying VCS dependencies](https://github.com/jazzband/pip-tools/issues/355)
in `pip-compile`).

Put your top-level requirements in a `requirements-app.txt` file.

Use a "freeze" script (as seen in [this Makefile][dm-deps-commit-makefile]) to generate the
fully specified `requirements.txt`, which is used whenever you need to pip-install the
dependencies.

* The script creates a temporary virtualenv, pip-installs the `requirements-app.txt` and
  pip-freezes the result as `requirements.txt`.

> The Makefile freeze script we currently have is constructed such that your `requirements-app.txt`
> file can only contain pinned version numbers for your application's immediate dependencies. This is
> not a particularly desirable feature: in principle we only demand that the final `requirements.txt`
> has no ambiguity and ends up containing pinned versions for all dependencies.

List dependencies only needed for development or testing into a separate `requirements-dev.txt` file.

#### Libraries

This recommendation applies to any Python repository that intended to be installable (into
a virtual environment, a container, or onto bare metal) as a dependency of some larger system
or application. It may be applicable to repositories that provide scripts to be run by
developers or other end-users, but is not recommended for code that's intended to be deployed
on its own into the cloud.

Use a [`setup.py`][setup-deps]
to specify the dependencies of your library, and the version ranges with which it
can be reasonably expected to work.

- The range you choose will depend on the guarantees each dependency makes about
  backward-compatibility. For example, if you're currently using version 1.3.1 of
  a semantically-versioned library, it would be reasonable to specify a range such
  as `<2.0,>=1.3.1`. However, for a library that doesn't make that guarantee,
  you might specify a more restricted range, such as `<1.4,>=1.3.1`.

- Update this file whenever you are ready to test and validate a new version that falls
  outside the existing range.

> If you have dependencies that aren't available on PyPI (for example, because you've fixed
> a bug by forking the code), then you can use a [PEP 440][]
> git reference in your `install_requires` list.
>
> - This requires pip 18.1, and we haven't tried it much at GDS.
>
> - In the past, we've documented such dependencies in a `requirements.txt` file
> ([example](https://github.com/alphagov/digitalmarketplace-utils/commit/dc16012af6b55d9eda4e8dd7fee514103682a5c7#diff-b4ef698db8ca845e5845c4618278f29a)),
> but any application wanting to depend on your library then needs to manually copy those sub-dependencies into its
> own list
> ([example](https://github.com/alphagov/digitalmarketplace-briefs-frontend/commit/5fb3df85bf9fa109ba3eaf1750a4fba4e92ef2a8#diff-28ad48f17e559daf5f2116b1d6a7f620)).

Specify dependencies needed only for testing your library in `tox.ini` if you are using [Tox](https://tox.readthedocs.io/en/latest/)
([example](https://github.com/alphagov/notifications-python-client/blob/f27b67a53371c68c36583f985c29b0526e2294b9/tox.ini)),
or in a `requirements-dev.txt` ([example](https://github.com/alphagov/digitalmarketplace-utils/blob/222e50c022eae4d9b2569b148cdfc642b08733cf/requirements-dev.txt))
file otherwise.


### Updating this manual

This manual, and by extension the [GDS Python Style Guide][GDSPSG], is not presumed to be infallible or beyond dispute.
If you think something is missing or if you'd like to see something changed then:

1. _(optional)_ Start with the [#python][slack-python] Slack channel. See what other developers think and you'll get an idea
of how likely your proposal is of being accepted as a pull request even before you put in any work.
2. Check out the making changes section of the [GDS Way repo][github-gds-way-readme-making-changes]
3. Create a pull request against [GDS Way repo][github-gds-way]



[github-gds-way]: https://github.com/alphagov/gds-way
[gds-way-deps]: /standards/tracking-dependencies.html
[github-gds-way-readme-making-changes]: https://github.com/alphagov/gds-way/blob/master/README.md#making-changes
[gds-way-code-style-guides]: /manuals/programming-languages.html#code-style-guides
[slack-python]: https://gds.slack.com/messages/python
[linting]: linting.html
[WikiCyclomatic_complexity]: https://en.wikipedia.org/wiki/Cyclomatic_complexity
[PyCharm]: https://www.jetbrains.com/pycharm/
[GPSG]: https://github.com/google/styleguide/blob/gh-pages/pyguide.md
[PEP8]: https://www.python.org/dev/peps/pep-0008/
[PEP373]: https://www.python.org/dev/peps/pep-0373/
[GPSG]: https://google.github.io/styleguide/pyguide.html
[PEP 8]: https://www.python.org/dev/peps/pep-0008/
[Flake8]: http://flake8.pycqa.org/en/latest/
[pycodestyle]: http://pycodestyle.pycqa.org/en/latest/
[Pyflakes]: https://github.com/pycqa/pyflakes
[McCabe]: https://pypi.python.org/pypi/mccabe
[dm-deps-commit]: https://github.com/alphagov/digitalmarketplace-api/commit/95ac12206d26e6b219dd381dd63641c33467afbd
[dm-deps-commit-makefile]: https://github.com/alphagov/digitalmarketplace-api/commit/95ac12206d26e6b219dd381dd63641c33467afbd#diff-b67911656ef5d18c4ae36cb6741b7965
[snyk.io]: https://snyk.io/
[GDSPSG]: style-guide.html
[setup-deps]: https://docs.python.org/3/distutils/setupscript.html#relationships-between-distributions-and-packages
[PEP 440]: https://www.python.org/dev/peps/pep-0440/#direct-references
