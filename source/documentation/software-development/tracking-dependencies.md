# How to manage third party software dependencies

When you develop and operate a service, it’s important to keep any third party dependencies you use up to date. By doing this, you can avoid potential security vulnerabilities.

Any automated tools you use to manage third party dependencies should be compatible with [GDS supported programming languages][]. The tools you use should neither slow down your development process nor disclose potential security vulnerabilities to the public.

You can read more about [managing software dependencies in the Service Manual][], where you will find a list of common dependency management tools.

Our [programming language style guides][] also contain language-specific advice about managing dependencies (for example, [managing Python dependencies][]).

## Update dependencies frequently

Update your dependencies frequently rather than in ‘big bang’ batches. This works well with [continuous delivery][] principles, ensuring the changes introduced are small and can be automatically tested.

Tools exist that will scan GitHub repositories and raise PRs when dependency updates are found. Teams at GDS are using:

* [Dependabot][] - used by GOV.UK, GOV.UK Pay and GovWifi. The GOV.UK team manual contains [guidance on using dependabot][] and [how the PRs raised should be reviewed][]
* [PyUp][] - a Python dependency checker. Used by Digital Marketplace and GOV.UK Notify, PyUp will monitor for updates and vulnerabilities
* [Greenkeeper][] - a npm dependency checker used by the GOV.UK Verify team on the [Node.js client for the Verify Service Provider][]

All the above tools are free to use on public repositories.

Dependabot has been turned on by GitHub for all repositories that are active, public and have not been forked.

The Cyber Security team will review the repositories that do not have dependency management in use and will turn on Dependabot where required. Service teams are free to use a different tool such as [Snyk](https://snyk.io/), but will need to add a `no-dependabot` tag to their repository for monitoring purposes. You can [contact Cyber Security](https://gds.slack.com/archives/CCMPJKFDK) if you have any questions or need help.


### Docker base images

Like dependencies, Docker base images are also frequently updated. If you run containers as part of your service, you should regularly rebuild your images (and base images) to include the latest updates. Automate this process where possible.

## Monitoring for vulnerabilities

You should monitor for potential vulnerabilities in every layer of your technology stack. This is not straightforward but tooling exists to help. The Service Manual provides [guidance on browser technology, tooling and mailing lists you can subscribe to][].

Most of the tooling that helps you stay on top of dependency updates will also highlight vulnerabilities. Additional tooling includes:

* [GitHub security alerts][] - When GitHub discovers or is informed about a vulnerability, it will email an alert to the repository owner and users with admin access. GitHub security alerts will be turned on for all Alphagov repositories. If services wish to opt out of security advisories on their repository, they can contact cyber security and then add the `no-security-advisories` tag to their repository.
* [Snyk][] - Snyk is capable of detecting vulnerabilities in a variety of languages including all the [GDS supported programming languages][]. Snyk can be configured to raise PRs, email regular reports and alert you when new vulnerabilities are detected

If you have an old repository that is receiving security alerts but it is not being worked on or maintained, you may wish to archive your repository instead.

The Cyber Security team has created a Splunk dashboard. This gives service teams visibility of vulnerabilities in their repositories. To allow for your repositories to be categorised correctly in the Splunk dashboard, please ensure you tag your repository with the service name. If you would like to access the dashboard [contact Cyber Security](https://gds.slack.com/archives/CCMPJKFDK).

### Docker images

Always use [official base images][]. Docker Hub regularly scans official images and the results can be viewed by logging into Docker Hub. If you do not regularly update your base image, you must ensure a manual process exists to monitor and prioritise fixes for vulnerabilities detected.

The Digital Marketplace team uses [Snyk container vulnerability management tooling][] to regularly scan base images.

## Minimising what you need to monitor

Minimise the things you need to monitor by minimising dependencies where practically possible. For example, if running containers, make sure you pick the smallest base images.

Also consider managed solutions where possible. For example:

* Use [GOV.UK PaaS buildpacks][] so you do not have to monitor for Operating System (OS), runtime or programming language vulnerabilities
* Consider managed container orchestration technology such as [AWS Fargate][] or similar so you do not have to monitor for vulnerabilities in your OS or control plane

This guidance is inline with the GDS Reliability Engineering strategic principle of [use fully managed cloud services by default][].

[GDS supported programming languages]: /software-development/choose-a-programming-language
[managing software dependencies in the Service Manual]: https://www.gov.uk/service-manual/technology/managing-software-dependencies
[programming language style guides]: /software-development/style-guides
[managing Python dependencies]: /software-development/style-guides/python
[Snyk]: https://snyk.io/
[monitor code dependencies]: https://snyk.io/features
[continuous delivery]: /version-control-deployments/continuous-delivery
[Dependabot]: https://dependabot.com/
[guidance on using Dependabot]: https://docs.publishing.service.gov.uk/manual/manage-ruby-dependencies.html
[how the PRs raised should be reviewed]: https://docs.publishing.service.gov.uk/manual/merge-pr.html#dependabot
[PyUp]: https://pyup.io/
[Greenkeeper]: https://greenkeeper.io/
[Node.js client for the Verify Service Provider]: https://github.com/alphagov/passport-verify
[guidance on browser technology, tooling and mailing lists you can subscribe to]: https://www.gov.uk/service-manual/technology/managing-software-dependencies#managing-risks-in-third-party-code
[GitHub security alerts]: https://help.github.com/en/articles/about-security-alerts-for-vulnerable-dependencies
[official base images]: https://docs.docker.com/docker-hub/official_images/
[Snyk container vulnerability management tooling]: https://snyk.io/features/container-vulnerability-management/
[GOV.UK PaaS buildpacks]: https://docs.cloud.service.gov.uk/guidance.html#responsibility-model
[AWS Fargate]: https://aws.amazon.com/fargate/
[use fully managed cloud services by default]: https://reliability-engineering.cloudapps.digital/documentation/strategy-and-principles/re-principles.html#3-use-fully-managed-cloud-services-by-default
