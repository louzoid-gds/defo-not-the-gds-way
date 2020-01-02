# How to manage alerts

Your service should have a system in place to send automated alerts if its monitoring system detects a problem. Sending alerts help services meet service level agreements (SLAs).

## Sending alerts

Your service should send an alert when your [service monitoring][] detects an issue that:

* affects service users
* requires action to fix
* lasts for a sustained period of time

You should only send an alert for things that need action. This includes immediate action for critical or high priority alerts, or less urgent alerts. Alert text should be specific and [include actionable information][]. You should not include sensitive material in this text.

Create alerts based on events affecting users, such as slow service requests or unavailable webpages. You should also track events like disks being full or almost full, or databases being down. These are both events that can lead to more serious alerts that do affect users.

You must set up your alerts to distinguish between when something is wrong for a sustained period of time, and when it's a brief issue caused by temporary network conditions. [Prometheus][] supports this by using the `for` parameter in its alerting rule, which indicates the condition has to be true for a set period of time before it triggers an alert.

### When you should not send an alert

You do not need to send an alert if no action is needed. For example, an alert showing a system's status is really a monitoring tool and you should use a dashboard to display this information instead. The GDS Way has more guidance on [how to monitor your service][].

Specific examples of issues that should not trigger an alert include:

* an individual container instance dying
* a single task invocation failing

This is because the systems running the architecture like [Amazon Elastic Container Service (Amazon ECS)][] or [Kubernetes][] will bring the instance back up, and the task will retry.

Situations where there’s a long period of fewer than expected instances or repeated task failures should trigger alerts, as they show underlying problems.

## Prioritising alerts

You must prioritise alerts based on whether they need an immediate fix. It can help to class issues as:

* interrupting - need immediate investigate and resolution
* non-interrupting - do not need immediate resolution

The [Google Site Reliability Engineering (SRE)][] handbook classifies “interrupting” issues as “pages”, and “non-interrupting” issues as “tickets”. Put non-interrupting alerts into a ticket queue for your support team to solve. Keep the ticket queue and team backlog separate to avoid confusion. You should specify an SLA for how long both types of alert take to resolve.

You should manage alerts using a dedicated tool which will allow you to:

* manage alerts in a queue
* triage alerts for review
* attach statuses to alerts, for example, in progress or resolved
* gather data about alerts to help improve processes

Recommended tools are:

- [PagerDuty][] to send high-priority / interrupting alerts
- [Zendesk][] to manage non-interrupting alerts as tickets

You can also configure these tools to send alert notifications using email or Slack. However, you should only use email and Slack as additions to your primary alerting tool. If alerts only go to email or Slack, people may ignore, overlook, filter them out, or treat them like spam.

We recommend using dashboards and information radiators, also known as Big Visible Charts (BVC), like [Smashing][] or [BlinkenJS][] in combination with alert management tools.

### Further reading

For more information refer to the:

* Service Manual for [more information on how to write alerts][]
* GDS way for [information about monitoring][]
* Google SRE handbook to find out more about [site reliability engineering][]

You can also read more on how the Reliability Engineering team [manages monitoring and alerts][].

[service monitoring]: /logging-monitoring/monitoring
[Google Site Reliability Engineering (SRE)]: https://landing.google.com/sre/book.html
[PagerDuty]: https://www.pagerduty.com
[Zendesk]: https://www.zendesk.com
[Smashing]: https://github.com/Smashing/smashing
[BlinkenJS]: https://github.com/alphagov/blinkenjs
[information about monitoring]: /logging-monitoring/monitoring
[site reliability engineering]: https://landing.google.com/sre/book/index.html
[more information on how to write alerts]: https://www.gov.uk/service-manual/technology/monitoring-the-status-of-your-service
[include actionable information]: https://response.pagerduty.com/oncall/alerting_principles/#alert-content
[Prometheus]: https://prometheus.io/
[how to monitor your service]: /logging-monitoring/monitoring
[Amazon Elastic Container Service (Amazon ECS)]: https://aws.amazon.com/ecs/
[Kubernetes]: https://kubernetes.io/
[manages monitoring and alerts]: https://reliability-engineering.cloudapps.digital/monitoring-alerts.html
