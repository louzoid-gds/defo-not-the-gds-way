# Use continuous delivery

[Continuous delivery][] helps you implement changes like new features into production quickly and safely. 

Using continuous delivery has multiple benefits.

## Iterate code frequently

It’s cheaper and easier to deliver small changes to production, meaning you can get feedback from users quickly.

## Low-risk releases

Frequent small changes make it easier to diagnose problems, and the cost of fixing them is much lower than with large releases.

## Quality software builds

Automated test suites allow you to quickly identify regressions in your software. This means you can focus on exploratory, usability, performance and security testing.

## Maintainable code

Building and releasing software in small pieces helps you focus on writing small composable bits of code. This means your code is easier to maintain and update.

## Essential concepts

With continuous delivery use frequent integration with the master branch, automatic build promotion and production monitoring.

### Frequent integrations with master branch

With [continuous integration][] you integrate with a master branch at least once a day, for example using source-control branching models like [Trunk-Based Development][].

If your team’s environment is regulated, and you need evidence that you review all code changes, raise and merge frequent small pull requests. For example, [Fourth Wall Helpful][], a client-side pull request and build status monitor for Github repositories, could help you build a team culture to support this practice.

Use approaches like [feature-flagging][] or [modular architectures][] to deploy partially complete features. This reduces the size of changes going to production and encourages your team to build modular, configurable systems. 

### Automatic build promotion

You can quickly distinguish between good and bad builds with automatic build promotion. By deploying builds that have to pass multiple test jobs downstream of the initial build process you can get quicker feedback if the build fails.

### Use production monitoring and alerting

You can understand the effect of your changes on production using [production monitoring and alerting][]. Monitoring essential parts of your system allows you to see if changes have any unintended impacts and to respond quickly in case of problems.

## How to measure continuous delivery

It’s important to set [performance metrics for your service][] and [monitor its status][].

[Accelerate: The Science of Lean Software and Devops: Building and Scaling High Performing Technology Organizations][] suggests 3 metrics that correlate with high performing teams:

- lead time to change
- mean time to recovery
- frequency of releases

You could use these metrics to understand how effective your build and release process is and measure any changes.

## Further reading

Find out more about continuous delivery from:

- [Architecting for Continuous Delivery][] - Jez Humble at Agile India 2016 (video)
- [2018 State of DevOps Report][] - see where you are and how to get to the next stage
- [Accelerate: The Science of Lean Software and Devops: Building and Scaling High Performing Technology Organizations][] - by Nicole Forsgren Jez Humble Gene Kim
- [Trunk Based Development][] - a source control branching method



[Continuous delivery]: https://www.continuousdelivery.com
[Enable frequent iterations]: https://medium.com/continuous-delivery/why-continuous-deployment-matters-to-business-6a79b5602145
[Deploy low risk releases]: http://www.informit.com/articles/article.aspx?p=1833567
[Build quality software]: https://continuousdelivery.com/foundations/test-automation/
[continuous integration]: https://martinfowler.com/bliki/ContinuousIntegrationCertification.html
[Trunk-Based Development]: https://trunkbaseddevelopment.com/
[Fourth Wall Helpful]: https://github.com/alphagov/fourth-wall
[feature-flagging]: https://featureflags.io/2016/10/28/continuous-delivery-coding-patterns-feature-toggles/
[modular architectures]: https://continuousdelivery.com/implementing/architecture/
[feature branching]: https://www.martinfowler.com/bliki/FeatureBranch.html
[production monitoring and alerting]: /logging-monitoring/monitoring
[performance metrics for your service]: https://www.gov.uk/service-manual/measuring-success/how-to-set-performance-metrics-for-your-service
[monitor its status]: https://www.gov.uk/service-manual/technology/monitoring-the-status-of-your-service
[Accelerate: The Science of Lean Software and Devops: Building and Scaling High Performing Technology Organizations]: https://medium.com/slashdeploy/book-review-accelerate-92ebc00f4354
[Architecting for Continuous Delivery]: https://www.youtube.com/watch?v=Lx9ssegE6FA
[Accelerate]: https://wordery.com/accelerate-nicole-forsgren-phd-9781942788331?cTrk=OTc2NDYwNzZ8NWI2ZDg5NGJkYzAyZjoxOjE6NWI2ZDg5NDQwM2ZhODguNDU0MTgxMTU6ODJlODM3ODY%3D
[Trunk Based Development]: https://trunkbaseddevelopment.com/
[2018 State of DevOps Report]: https://puppet.com/resources/whitepaper/state-of-devops-report
