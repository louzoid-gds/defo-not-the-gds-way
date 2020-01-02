# How to monitor your service

At GDS, we follow the Service Manual guidance on how to [monitor the status of services][] and set [performance metrics][].

We recommend using [Pingdom][] to monitor your service’s availability. To further make sure your service is working, you should:

* run regular [smoke tests][] using a browser automation app such as Selenium
* implement a tool to ensure user journeys are working as you expect
* monitor applications for errors using an error tracking app such as [Sentry][]
* implement configuration management to set up repeatable monitoring

## Using metrics-based monitoring

Collecting metrics on the performance of your service is useful for [capacity planning][] and autoscaling. You should apply metrics-based monitoring to measure aggregated numerical data about your service and create [Grafana][] dashboards to view metrics from your datasource, for example related to your infrastructure or application.

Reliability Engineering is running a beta on using [Prometheus][] as the operational metrics service for GDS. It will be available to all teams that use the [recommended hosting][] options. Read the [reliability engineering docs][] to find out more.


[monitor the status of services]: https://www.gov.uk/service-manual/technology/monitoring-the-status-of-your-service
[performance metrics]: https://www.gov.uk/service-manual/measuring-success/how-to-set-performance-metrics-for-your-service
[Pingdom]: https://www.pingdom.com/
[smoke tests]: https://www.gov.uk/service-manual/technology/deploying-software-regularly#using-smoke-tests-after-you-deploy
[Sentry]: https://sentry.io/welcome/
[capacity planning]: https://www.gov.uk/service-manual/technology/test-your-services-performance#start-with-capacity-planning
[Grafana]: http://grafana.org/
[Prometheus]: https://prometheus.io/
[recommended hosting]: /hosting-and-infrastructure/hosting
[reliability engineering docs]: https://reliability-engineering.cloudapps.digital/#metrics
