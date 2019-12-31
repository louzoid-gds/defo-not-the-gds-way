# Setting up logging

This page contains information on how to manage logs.  See
the [logging recommendation](../standards/logging.html) for specific
recommendations.

## Standard field names

In order to make logs easier to query, we should adopt a standard set
of field names for sending logs.

### Naming conventions

We should use current logstash naming conventions, as documented in
[LOGSTASH-675](https://logstash.jira.com/browse/LOGSTASH-675).  In particular:

  - the only guaranteed fields are `@timestamp` and `@version`
  - `@version` is always `1`
  - `@timestamp` is always an ISO-8601 formatted timestamp
  - you should not prefix field names with `@fields.`

We should use the
[elastic beats naming conventions](https://www.elastic.co/guide/en/beats/libbeat/current/event-conventions.html).  In particular:

  - fields are lower case and `snake_case`
  - use dots to group related metrics, for example `cpu.user` and `cpu.system`

An alternative to using dots to group related metrics is to use a
nested document. For example: `"cpu": {"user":30.0,"system":40.0}`

### HTTP fields

Lots of fields related to http access logs should be grouped under the
`access` namespace.  You do not need to provide every field,
and some may be more convenient than others (for example, it might be
easier to produce `url` rather than `path` and `query_string` from
nginx access logs, but `path` and `query_string` might be easier from
Rails logs).  You may wish to omit or anonymise certain fields for
policy reasons.

If a field has no value, you can omit it.  If this is difficult to do,
you can use the value `"-"` instead.  This may be more convenient, for
example, when writing grok filters on access logs.

  - `agent`
      - type: string
      - meaning: HTTP User-Agent header contents
  - `body_sent.bytes`
      - type: integer
      - meaning: actual number of bytes sent in the response body.
        (Not necessarily the same as the Content-length header.)
  - `host`
      - type: string
      - meaning: HTTP Host header
  - `method`
      - type: string
      - meaning: HTTP method used in request
      - examples: `"GET"`, `"POST"`
  - `path`
      - type: string
      - meaning: HTTP path, *excluding* query string
      - example: `/dir1/dir2/resource`
  - `query_string`
      - type: string
      - meaning: HTTP query string, *excluding* initial question mark
        character
      - example: `lang=en&q=hello`
  - `referrer` (not `referer`)
      - type: string
      - meaning: HTTP Referer header contents
  - `response_code`
      - type: integer
      - meaning: HTTP status code
      - If the status code does not exist for some reason (say,
        because the connection was closed or reset before the status
        was sent) then a special numerical value can be used, or the
        field can be dropped.
      - examples: `200`, `404`
  - `url`
      - type: string
      - meaning: requested URL, relative to server root, including
        query string if provided
      - example: `/dir1/dir2/resource?lang=en&q=hello`
  - `user_agent`
      - type: object
      - meaning: parsed fields representing user agent.  Generated
        using logstash `useragent` filter, or elasticsearch
        ingest-user-agent plugin.
  - `user_name`
      - type: string
      - meaning: user name of authenticated user.  In particular, this
        refers to HTTP authentication such as basic auth, rather than
        application-level authentication.

Example:

```json
{
  "@version": 1,
  "@timestamp": "2017-07-11T15:49:00Z",
  "access": {
    "response_code": 404,
    "method": "GET",
    "url": "/foo/bar?q=hello"
  }
}
```

## Advice for particular application frameworks

### Dropwizard

The
[dropwizard-logstash](https://github.com/alphagov/dropwizard-logstash)
library will set things up for you using the standard names.

## Advice for particular environments

### Cloud Foundry

The
[GOV.UK PaaS Logging](https://docs.cloud.service.gov.uk/monitoring_apps.html#set-up-the-logit-io-log-management-service)
documentation will help you configure logit and drain logs into it
from your app.
