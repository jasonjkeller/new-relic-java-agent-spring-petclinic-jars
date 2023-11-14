# New Relic Java Agent And SpringBoot Jars

Simple project for quickly starting up a SpringBoot Petclinic service with the New Relic Java agent without having to build anything.

## Requirements

Java 17+ is required to run the Petclinic service.

## Configure New Relic Java Agent

At a minimum the `license_key` must be set for the New Relic APM account that the agent should report to. It is also recommended to set the `app_name`, or it will use the default name of `My Application`. 

If the `newrelic.yml` is sitting alongside the agent jar it will be automatically detected and config will be read from it. If the config file is located elsewhere you can configure the agent to find it by setting the system property `-Dnewrelic.config.file=/path/to/newrelic.yml` or environment variable `NEW_RELIC_CONFIG_FILE=/path/to/newrelic.yml`. All agent config can be done via the config file if desired.

Alternatively, the `newrelic.yml` config file isn't required and all agent config can be done via [system properties](https://docs.newrelic.com/docs/apm/agents/java-agent/configuration/java-agent-configuration-config-file/#System_Properties) or [environment variables](https://docs.newrelic.com/docs/apm/agents/java-agent/configuration/java-agent-configuration-config-file/#Environment_Variables).

Environment variable:
```
NEW_RELIC_APP_NAME='app_name'
NEW_RELIC_LICENSE_KEY='license_key'
```

System properties:
```
-Dnewrelic.config.app_name='app_name'
-Dnewrelic.config.license_key='license_key'
```

### Configure APM Environment

By default, the New Relic Java agent will report to a US Production APM account, to use a staging or EU account additional configuration will be required as shown below.

#### Environment Variables
* US Production
    ```
    NEW_RELIC_HOST=collector.newrelic.com
    NEW_RELIC_API_HOST=rpm.newrelic.com
    NEW_RELIC_METRIC_INGEST_URI=https://metric-api.newrelic.com/metric/v1
    NEW_RELIC_EVENT_INGEST_URI=https://insights-collector.newrelic.com/v1/accounts/events
    ```
* EU Production
    ```
    NEW_RELIC_HOST=collector.eu01.nr-data.net
    NEW_RELIC_API_HOST=api.eu.newrelic.com
    NEW_RELIC_METRIC_INGEST_URI=https://metric-api.eu.newrelic.com/metric/v1
    NEW_RELIC_EVENT_INGEST_URI=https://insights-collector.eu01.nr-data.net/v1/accounts/events
    ```
* US Staging
    ```
    NEW_RELIC_HOST=staging-collector.newrelic.com
    NEW_RELIC_API_HOST=staging.newrelic.com
    NEW_RELIC_METRIC_INGEST_URI=https://staging-metric-api.newrelic.com/metric/v1
    NEW_RELIC_EVENT_INGEST_URI=https://staging-insights-collector.newrelic.com/v1/accounts/events
    ```
#### System Properties
* US Production
    ```
    -Dnewrelic.config.host=collector.newrelic.com
    -Dnewrelic.config.api_host=rpm.newrelic.com
    -Dnewrelic.config.metric_ingest_uri=https://metric-api.newrelic.com/metric/v1
    -Dnewrelic.config.event_ingest_uri=https://insights-collector.newrelic.com/v1/accounts/events
    ```
* EU Production
    ```
    -Dnewrelic.config.host=collector.eu01.nr-data.net
    -Dnewrelic.config.api_host=api.eu.newrelic.com
    -Dnewrelic.config.metric_ingest_uri=https://metric-api.eu.newrelic.com/metric/v1
    -Dnewrelic.config.event_ingest_uri=https://insights-collector.eu01.nr-data.net/v1/accounts/events
    ```
* US Staging
    ```
    -Dnewrelic.config.host=staging-collector.newrelic.com
    -Dnewrelic.config.api_host=staging.newrelic.com
    -Dnewrelic.config.metric_ingest_uri=https://staging-metric-api.newrelic.com/metric/v1
    -Dnewrelic.config.event_ingest_uri=https://staging-insights-collector.newrelic.com/v1/accounts/events
    ```

## Start SpringBoot Petclinic Service With Agent

Run the Petclinic jar with the Java agent attached (configured via `newrelic.yml` or environment variables):
```shell
java -javaagent:newrelic-agent-8.7.0.jar -jar spring-petclinic-3.1.0-SNAPSHOT.jar
```

Run the Petclinic jar with the Java agent attached (configured via system properties):
```shell
java -javaagent:newrelic-agent-8.7.0.jar -Dnewrelic.config.license_key='license_key' -Dnewrelic.config.app_name='app_name' -jar spring-petclinic-3.1.0-SNAPSHOT.jar
```

## Make a Request to the Petclinic Service

By default, the Petclinic Service will be accessible at: http://localhost:8080

Example `curl` request:  
```shell
curl --request GET --url http://localhost:8080/vets --header 'content-type: application/json'
```
