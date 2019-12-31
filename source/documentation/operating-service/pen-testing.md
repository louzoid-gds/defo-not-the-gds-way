# How to do penetration tests

You should aim to run [penetration tests](https://www.gov.uk/service-manual/technology/vulnerability-and-penetration-testing) on your service every 6 months. You must work with the [GDS Information Assurance (IA) team](https://sites.google.com/a/digital.cabinet-office.gov.uk/gds/operations/information-assurance) to agree when you will test and to procure external tests.

Tests should be carried out by an approved third party through the [National Cyber Security Centre (NCSC) CHECK scheme](https://www.ncsc.gov.uk/articles/check-fundamental-principles) or internally by a member of the GDS Cyber Security Team, depending on your need.

You may need to schedule additional testing if you make significant changes to your service. You should meet with the IA team regularly to discuss ongoing changes.

A significant change could be when you:

* change a cloud service provider
* change stored data, for example if you introduce new data which can be classified as [personally identifiable information (PII)](https://en.wikipedia.org/wiki/Personally_identifiable_information)
* add a third-party partner, for example, a database processor or email provider (especially if the third-party partner is processing PII)

## Scope your test

Before testing you should define:

* the beginning and end test dates
* the areas you want the tester to target, for example bypassing authentication
* what should be excluded, for example third party managed infrastructure
* any specific technical capabilities to allow third-party testers to complete testing, for example experience working with AWS security groups

## Prepare for your test

Before the test you will be expected to share documentation with the testers, for example up to date architecture diagrams. The documentation could also include information about the individual components of each application being tested.

You should run the tests  on a separate test environment which replicates the behaviour of your live service.

To prepare your test environment you should:

 * create temporary credentials for testers (testers should provide their own SSH public keys)
 * notify your service providers in advance, for example by [emailing GOV.UK PaaS Support](mailto:gov-uk-paas-support@digital.cabinet-office.gov.uk)

## What to do after testing

After your test you should meet with the IA team to discuss the test results. You can then prioritise work to mitigate any issues identified in the test and schedule a retest if needed.

## Schedule a test

To schedule a test [contact the IA team](https://sites.google.com/a/digital.cabinet-office.gov.uk/gds/operations/information-assurance).

If you plan to test with a third-party, you must contact the IA team at least 3 months in advance so they can organise the procurement for you.
