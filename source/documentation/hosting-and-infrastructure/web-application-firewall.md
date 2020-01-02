# Use a web application firewall (WAF)

A [web application firewall (WAF)](https://www.owasp.org/index.php/Web_Application_Firewall) is an application layer protection for bi-directional web-based traffic. With a WAF, you can track web traffic and use specific tools to configure access control for your web content. Doing this improves your service’s security monitoring and security position.

## Why you should use a WAF

Your continuous integration (CI) and continuous deployment (CD) pipelines should include security tests in their workflows to identify any common vulnerabilities in your code. Some common vulnerabilities like [Cross-site Scripting (XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) and [XML command injection attacks](https://www.owasp.org/index.php/Testing_for_XML_Injection_(OTG-INPVAL-008)) are still possible in your production environments due to human error.

Combine WAF with CI and CD tools to reduce the risk from those tools, and provide enhanced layered security coverage for your service.

You may also need to use a WAF because of:

- GDS or departmental policies or standards
- [Information Assurance (IA)](https://sites.google.com/a/digital.cabinet-office.gov.uk/gds/operations/information-assurance) requirements to minimise risk
- [Payment Card Industry Data Security Standard (PCI DSS)](https://www.pcisecuritystandards.org/) compliance

## When and how to use a WAF

Set up a baseline of tests in your project’s alpha phase to identify any security vulnerabilities. As your service’s features grow, extend your tests to cover new vulnerabilities you identify. For example, through exercises like [application threat modelling](https://www.owasp.org/index.php/Application_Threat_Modeling)

[Good development practices](https://gds-way.cloudapps.digital/#how-to-build-software) should detect and fix common vulnerabilities before they reach production environments. Use your WAF to track digital services vulnerabilities that an attacker could exploit.

You should:

- have an independent security audit in place
- use established [logging techniques](/logging-monitoring/logging)
- encrypt data at rest as well as in transit
- subscribe to and apply security patches
- use query variables instead of plain text (stored procedure) to prevent [SQL injections](https://www.owasp.org/index.php/SQL_Injection)

You should monitor the Open Web Application Security Project (OWASP) [top 10 most critical web application vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) to keep up to date with the latest threats.

Using a WAF should align with your other security monitoring features, like [Security Information Event Management (SIEM)](https://en.wikipedia.org/wiki/Security_information_and_event_management). When developing use cases you should also factor in the extra time and resources needed to configure WAF rules.

### Managing your WAF

Identify any areas in your app not covered by your WAF and define measures to protect them, such as using:

- [alerts](#alerts) - as part of your incident management strategy
- [threat modelling](#threat-modelling) - to assess potential weaknesses in your environment
- [reviews](#reviews) - to manage your security controls

#### Alerts

It’s not always possible to block a detected attack because some services need to process transactions for any user of that service. In these situations you should [raise events as alerts](https://reliability-engineering.cloudapps.digital/monitoring-alerts.html#metrics-and-alerting).

When WAF alerts are raised, make sure you already have an incident policy in place, including:

- who should manage an alerts
- what their responsibilities are
- how to investigate an alert
- how to tune out false positives

#### Threat modelling

As your service matures, explore its architecture and conduct a threat modelling exercise to locate any specific threats to its environment.

For threats you cannot reduce due to their complexity, cost of fixing or project deadlines, change your WAF rules or add new ones to provide reactive coverage.

#### Reviews

Review your WAF after each application change against the risks in the OWASP top 10 category rules.

This should be similar to how you use an [IT Health Check (ITHC)](https://www.itgovernance.co.uk/it-health-check) to test and confirm the effectiveness of security controls in your environment.

### Case study GOV.UK PaaS

A [GOV.UK PaaS](https://www.cloud.service.gov.uk/) tenant uses a pattern with [Amazon Web Services (AWS) WAF](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html) before forwarding traffic to their apps with enabled shield advance for extra protection.

For more information read the proposed architecture for [implementing a DDoS-resistant Website using AWS Services](https://docs.aws.amazon.com/waf/latest/developerguide/tutorials-ddos-cross-service.html).

### Case study GOV.UK Pay

[GOV.UK Pay](https://www.payments.service.gov.uk/) uses a [NAXSI WAF (pay-nginx-proxy)](https://github.com/alphagov/pay-nginx-proxy) for its Nginx, forked from the Home Office.

GOV.UK Pay operates under the governance of [PCI compliance and DSS point 6.6](https://www.pcisecuritystandards.org/pdfs/infosupp_6_6_applicationfirewalls_codereviews.pdf) which states the need for web application scanning.

### Contact Cyber Security

Contact the security architects in the GDS Cyber Security team by email at [cyber.security@digital.cabinet-office.gov.uk](mailto:cyber.security@digital.cabinet-office.gov.uk) or use the [#cyber-security-help Slack channel](https://gds.slack.com/messages/CCMPJKFDK/) for help and advice.

### Further reading

To find out more about WAF refer to:

- [Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/Main_Page) the OWASP Foundation
- [WASC OWASP Web Application Firewall](https://www.owasp.org/index.php/WASC_OWASP_Web_Application_Firewall_Evaluation_Criteria_Project) Evaluation Criteria Project
- [National Cyber Security Centre (NCSC)](https://www.ncsc.gov.uk/) guidance
