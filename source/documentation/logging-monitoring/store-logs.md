# How to store and query logs

You will store and query logs to detect any potential errors within infrastructure that could be critical. Use the shared GDS [Logit][] account to store and query all your infrastructure and application logs.

Logit offers cloud-based on-demand, shared [ELK (Elasticsearch, Logstash and Kibana)][] stacks as a service. They are suitable for short-term storage of logs, and are accessible and queryable. The [Reliability Engineering documentation][] has more information about using Logit.

You should not operate your own self-hosted ELK stacks for logging. The Logit cloud-hosted ELK solution is easier to manage.

Your product may have legal or other requirements determining how long you should store logs. For example, the [Payment Card Industry Data Security Standard (PCI-DSS)][] requires 3 months of easily accessible logs and 12 months of archived logs.

## Short-term storage

You should not need to store logs spanning long periods in your short-term queryable store. Practical retention periods for short-term queryable logs are:

* no more than 7 days for non-production environments
* no more than 30 days production environments

## Long-term storage

When storing logs, you should focus on long-term durability for compliance reasons or to identify long-term performance trends.

ELK is not appropriate for long-term storage. There are other services which are less expensive and more reliable, for example if you use [Amazon Web Services (AWS)][] you could use [Amazon CloudWatch][] to run basic queries on older logs which may be a suitable solution.

### Log shipping

If you have set up log shipping, you should consider:

* how your logs will get to short and long-term stores - we recommend using the [Elastic Beats family of tools][] as a platform to collect and ship your data.
* what happens if one of these stores is unavailable
* whether the store will be overloaded when it comes back online

You could have one process to ship logs to your long-term archive, and a second process to fill a short-term query tool from the long-term archive, for example you could combine [Elasticsearch and Amazon Cloudwatch][]. This way you can be confident everything is safely stored.

The Beats tools can detect periods of service unavailability. The Beats tools recall how much data is sent to your store and will resume sending data, where they left off, when your service comes back online. By using a protocol which is backpressure-aware Beats tools also will not overload [Logstash][] with data.


[Logit]: https://logit.io/
[ELK (Elasticsearch, Logstash and Kibana)]: https://www.elastic.co/elk-stack
[Reliability Engineering documentation]: https://reliability-engineering.cloudapps.digital/#logging
[Payment Card Industry Data Security Standard (PCI-DSS)]: https://www.pcisecuritystandards.org/pci_security/
[Amazon Web Services (AWS)]: https://aws.amazon.com/
[Amazon CloudWatch]: https://aws.amazon.com/cloudwatch/
[Elastic Beats family of tools]: https://www.elastic.co/products/beats
[Elasticsearch and Amazon Cloudwatch]: https://www.elastic.co/guide/en/logstash-versioned-plugins/versioned_plugin_docs/v3.0.7-plugins-outputs-cloudwatch.html#v3.0.7-plugins-outputs-cloudwatch-options
[Logstash]: https://www.elastic.co/products/logstash
