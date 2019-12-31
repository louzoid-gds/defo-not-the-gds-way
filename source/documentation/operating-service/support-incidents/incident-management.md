# How to manage technical incidents

GDS incident management focuses on restoring normal operations quickly with minimal impact on users.

## Define incident priority

Define incident priority levels for your service’s applications. For example potential incidents include:

- system access problems
- wider technical failures with possible reputational impact to GDS
- denial of service (DoS)
- data breach or leak
- defacement
- unauthorised use of systems
- suspicious activity, such as traffic from an unknown source

Assign a priority level to incidents based on their complexity, urgency and resolution time. Incident severity also determines response times and support level.

### Incident priority table

|Classification|Type|Example|Response time|Update frequency|
|---|---|---|---|---|
|P1|Critical|Complete outage, or ongoing unauthorised access|20 minutes (office and out of hours)|1 hour|
|P2|Major|Substantial degradation of service|60 minutes (office and out of hours)|2 hours|
|P3|Significant|Users experiencing intermittent or degraded service due to platform issue|2 hours (office hours only)|Once after 2 business days|
|P4|Minor|Component failure that does not immediately impact a service, or an unsuccessful DoS attempt|1 business day (office hours only)|Once after 5 business|

## Develop an incident workflow

Your team must understand what to do during an incident. Develop and document your incident workflow to reflect your service needs and team size.

### Example workflow

Follow a prepared workflow to manage an incident to minimise its impact on your team and service users. Ensure that every step of the way is documented in writing using the [incident report template](https://docs.google.com/document/d/1WHDh7wzqVsKa2OVeBj2JU7Jm2Xc_iQJO2tm6i0DU1AQ/edit). 

1. [Establish an incident lead](#1-establish-an-incident-lead).
1. [Inform your team](#2-inform-your-team).
1. [Prioritise the incident](#3-prioritise-the-incident).
1. [Form a response team](#4-form-a-response-team).
1. [Investigate](#5-investigate).
1. [Contain](#6-contain).
1. [Eradicate](#7-eradicate).
1. [Recover](#8-recover).
1. [Communicate to a wider audience](#9-communicate-to-a-wider-audience).
1. [Resolve the incident](#10-resolve-the-incident).

#### 1. Establish an incident lead

Establish who your incident lead is. Find out who noticed the problem and if anyone else is investigating and fixing it. If that person is you, assume the role of incident lead.

#### 2. Inform your team

Inform your team using your chosen tool, like [Slack](https://gds.slack.com). If the incident involves a data or security breach, notify the Cyber Security team who’ll help you manage the incident. Contact them using the [#cyber-security-help Slack channel](https://gds.slack.com/messages/CCMPJKFDK/) or the [GDS Rotas app](https://rotas.cloudapps.digital/teams/cyber-security).

#### 3. Prioritise the incident

Prioritise the incident and start tracking actions, updates and communications. Teams like [GOV.UK PaaS](https://www.cloud.service.gov.uk/) and [Notify](https://www.notifications.service.gov.uk/) do this by creating a new incident report - copied from the [incident report template](https://docs.google.com/document/d/1YDA13RU6wicXoKgDv5VucJe3o_Z0k_Qhug9EJC_XdSE/) - and use it to track updates and progress.

####  4. Form an Incident Response team

Form a team with both an incident lead and a communications lead. The communications lead will make sure relevant parties are updated according to the incident priority table.

#### 5. Investigate

Make sure you keep your incident report up to date. If the incident involves a data breach follow your team’s GDPR documentation.

If the incident is a data or security breach you should follow steps 6, 7 and 8.
If the incident is not cyber security-related, skip to step 9. 

#### 6. Contain

You should determine the right containment procedures. In some cases, you may require a forensic clone.

##### 6.1 Short-term containment

You should start short-term containment measures as soon as you detect an incident. This could help minimise impact and maintain availability. Make sure that all affected systems are isolated from the non-affected systems.

##### 6.2 Long-term containment

You’ll need to make sure long-term containment is in place.

You should take the system offline if possible. Once the system is offline, you can proceed to step 7.

If the system has to remain in production, remove all malware and other artifacts from the affected systems, and harden the affected systems from further attacks. You should reimage the affected systems, or restore from the last known good backup.

##### 6.3 Forensic clone

As well as gathering evidence to help resolve an incident, you should collect evidence to support any potential follow-on disciplinary or legal proceedings.

To maintain the forensic integrity of the environment you should:

- document all commands used during the investigation and keep the documentation up to date - include how the evidence has been preserved
- store any forensic images taken during the investigation in a secure location, to prevent accidental damage or tampering

#### 7. Eradicate

Eradication may be necessary to remove components of the incident that remain on your systems, such as traces of malware. To help with eradication you should:

- identify all affected hosts
- remove all malware and other artifacts left behind by the attackers
- reimage and patch the affected system
- check backups, code, images and the affected systems are protected against further attacks

#### 8. Recover

Recovery is necessary to reduce the impact on user confidence and to reduce the likelihood of further successful attacks.

You should:

- confirm the affected systems are patched and hardened against the recent attack, and possible future attacks
- decide what day and time to restore the affected systems back into production (if they were taken offline)
- check the systems you’re restoring to production are not compromised in the same way as the original incident
- consider how long to [monitor](https://gds-way.cloudapps.digital/standards/monitoring.html) the restored systems for, and what to look out for

#### 9. Communicate to a wider audience

If the incident is serious (P1 or P2) you’ll need to contact a wider GDS audience and potentially your service users.

Your communications lead must manage:

- external and internal communications
- incident escalations

**External and internal communications**

Make sure internal and external parties, like Information Assurance (IA) or your service users are fully informed at every stage of your incident management process.

For example, teams including [GOV.UK Platform as a Service (PaaS)](https://status.cloud.service.gov.uk/), [GOV.UK Notify](https://www.notifications.service.gov.uk/) and [GOV.UK Pay](https://www.payments.service.gov.uk/) use the [StatusPage service](https://www.statuspage.io/) to trigger notifications to subscribed users.

Post regular updates to the status of an incident in the [#incident Slack channel](https://gds.slack.com/messages/CAD6S2B9Q). This helps people across GDS without having to find and follow multiple notification mechanisms for the different programmes.

**Incident escalations**

Notify escalation contacts of all high priority incidents (P1/P2). [Support Operations](https://gds.slack.com/messages/CADFJBDQU/details/#) can help you decide your service’s escalation route and associated contact details.

**Report cyber security incidents**

The incident lead must inform the National Cyber Security Centre (NCSC) of any category 1, 2 or 3 incidents. The NCSC defines security incidents in its [categorisation system prioritisation framework](https://www.ncsc.gov.uk/news/new-cyber-attack-categorisation-system-improve-uk-response-incidents). 

Depending on the incident, the NCSC may be able to provide technical support. 

#### 10. Resolve the incident

Hold an incident and lesson learned review following a [blameless post mortem culture](https://codeascraft.com/2012/05/22/blameless-postmortems/) so your service can improve. Add a row to the central [GDS incidents summary spreadsheet](https://docs.google.com/spreadsheets/d/1TmKiIAUr6EH1XZa5MJquSyHGZnQBjrORUJjs6l4TwHU) linking to your incident report document.

## Example incident management

Read the GOV.UK PaaS and Digital Marketplace incident management processes:

- GOV.UK PaaS [incident management process](https://team-manual.cloud.service.gov.uk/#incident-management)
- Digital Marketplace [incident response manual](https://alphagov.github.io/digitalmarketplace-manual/2nd-line-runbook/incidents.html)

## Further reading

Read the [GDS Technical Incident and Management Process](https://docs.google.com/document/d/1VPMc64iCXyVhof9Yu8KyqjLdL_guIQLdOko7mtiP-h4/edit#heading=h.lusoi4mhjuim) document for more information. For example, you can read more about:

- classifying incidents
- routes to support
- incident workflows - from request to resolution
- roles in the Incident Team for P1 and P2