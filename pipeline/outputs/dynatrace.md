---
description: Send logs to Dynatrace
---

# Dynatrace

Stream logs to [Dynatrace](https://www.dynatrace.com) by utilizing the **http** plugin to send data to [Dynatrace generic log ingest API](https://docs.dynatrace.com/docs/shortlink/lma-generic-log-ingestion).

Before starting you need to get a [Dynatrace API](https://docs.dynatrace.com/docs/shortlink/api-authentication) token with the `logs.ingest` (Ingest Logs) scope, and determine your [environment ID](https://docs.dynatrace.com/docs/shortlink/monitoring-environment#environment-id).  Then configure **http** output plugin with the following HTTP parameters.

## Configuration Parameters

| Key                        | Description                                                                                                                                                                                                                         | default                                            |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| header                     | The specific header for content-type                                                                                                                                                                                                | Content-Type application/json; charset=utf-8       |
| header                     | The specific header for authorization token, where {your-API-token-here} is the Dynatrace API token with log ingest scope                                                                                                           | Authorization Api-Token {your-API-token-here}      |
| Allow_Duplicated_Headers   | Specifies duplicated header use                                                                                                                                                                                                     |  false                                             |
| host                       | Your Dynatrace environment hostname where {your-environment-id} is your environment ID.                                                                                                                                             | {your-environment-id}.live.dynatrace.com           |
| port                       | TCP port of your Dynatrace host                                                                                                                                                                                                     | 443                                                |
| uri                        | Specify the HTTP URI for Dynatrace log ingest API                                                                                                                                                                                   | /api/v2/logs/ingest                                |
| format                     | The data format to be used in the HTTP request body                                                                                                                                                                                 | json                                               |
| json_date_format           | Date format standard for JSON                                                                                                                                                                                                       | iso8601                                            |
| json_date_key              | Fieldname specifying message timestamp                                                                                                                                                                                              | timestamp                                          |
| tls                        | Specify to use TLS                                                                                                                                                                                                                  | on                                                 |
| tls.verify                 | TLS verification                                                                                                                                                                                                                    | on                                                 |

## Getting Started

1. Get a [Dynatrace API](https://docs.dynatrace.com/docs/shortlink/api-authentication) token with the `logs.ingest` (Ingest Logs) scope.
2. Determine your Dynatrace [environment ID](https://docs.dynatrace.com/docs/shortlink/monitoring-environment#environment-id).
3. In your main Fluent Bit configuration file, append the following _Output_ section:

```text
[OUTPUT]
    name         http
    match        *
    header       Content-Type application/json; charset=utf-8
    header       Authorization Api-Token {your-API-token-here}
    allow_duplicated_headers false
    host         {your-environment-id}.live.dynatrace.com
    Port         443
    URI          /api/v2/logs/ingest
    Format       json
    json_date_format iso8601
    json_date_key timestamp
    tls          On
    tls.verify   On
```

4. Once the configuration is applied and new logs are appended, verify their receipt within Dynatrace. This can be done using Dynatrace [Notebooks](https://docs.dynatrace.com/docs/observe-and-explore/dashboards-and-notebooks/notebooks) with a Dynatrace Query Language query, for example:

    ```
    fetch logs
    ```

## References

* [Dynatrace Fluent Bit documentation](https://docs.dynatrace.com/docs/shortlink/lma-stream-logs-with-fluent-bit)
* [Fluent Bit integration in Dynatrace Hub](https://www.dynatrace.com/hub/detail/fluent-bit/?filter=log-management-and-analytics) 
* [Video: Stream a Log File to Dynatrace using Fluent Bit](https://www.youtube.com/watch?v=JJJNxhtJ6R0)
* [Blog: Easily stream logs from Fluent Bit to Dynatrace](https://www.dynatrace.com/news/blog/easily-stream-logs-with-fluent-bit-to-dynatrace/)