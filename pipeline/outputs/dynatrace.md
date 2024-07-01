# Dynatrace

Output your data to [Dynatrace](https://www.dynatrace.com) by utilizing the **http** plugin to send data to Dynatrace [generic log ingest API](https://www.dynatrace.com/support/help/observe-and-explore/logs/log-monitoring/acquire-log-data/log-data-ingest).

Before starting you need to get a Dynatrace API token with the `logs.ingest` (Ingest Logs) scope. Then configure **http** output pluginwith the following HTTP parameters.

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
| tls.verify                 | TLS verification                                                                                                                                                                                                                    | off                                                |

### Configuration File

In your main configuration file, append the following _Output_ section:

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
    tls.verify   Off
```


See more [how Fluent Bit integrates with Dynatrace here](https://www.dynatrace.com/hub/detail/fluent-bit/?filter=log-management-and-analytics) and [Dynatrace Fluent Bit documentation](https://docs.dynatrace.com/docs/shortlink/lma-stream-logs-with-fluent-bit).
