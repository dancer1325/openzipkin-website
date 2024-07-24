---
title: Server extensions and choices
weight: 4
---

## Server extensions

* Zipkin server -- bundles extension for --
  * span collection over
    * http
    * Kafka
    * RabbitMQ 
  * storage
    * in-memory
    * MySQL
    * Cassandra
    * Elasticsearch
* modules / to the default server build, add
  * transport extensions
  * storage 

### OpenZipkin supported

* hosted | [OpenZipkin GitHub](https://github.com/openzipkin/)

| Type | Module | Related product | Other notes |
|:-----|:--------|:----------------|:------------|{% for extension in site.data.extensions %}
| {{ extension.type }} | {{ extension.module }} | {{extension.product}} | {{ extension.notes }} |{% endfor %}
{: .wide-table}

### Community supported

| Type | Module | Related product | Other notes |
|:-----|:--------|:----------------|:------------|{% for extension in site.data.community_extensions %}
| {{ extension.type }} | {{ extension.module }} | {{extension.product}} | {{ extension.notes }} |{% endfor %}
{: .wide-table}


## Alternative servers

* alternate backends (to the default Zipkin server) / process the same data sent
  * via
    * API
    * data formats
    * shared libraries 

### Community supported

* alternative backends / accept Zipkin format
  * how can be splited ?
    * those / use the same code as Zipkin | same endpoints
    * those / alternative endpoints OR partially support features
  * cases
    * [Apache SkyWalking](https://skywalking.apache.org/)
      * if [zipkin trace component](https://skywalking.apache.org/docs/main/next/en/setup/backend/zipkin-trace/) is enabled -> Skywalking
        * exposes
          * == HTTP POST endpoints to Zipkin
            * http port 9411 accepts POST requests |
              * `/api/v1/spans` (thrift, json)
              * `/api/v2/spans` (json, proto)  
          * == Kafka topic to Zipkin
            * kafka topic `zipkin`
            * groupID `zipkin`
            * v2 spans -- encoded as a -- thrift/json/proto list / message 
        * == encoding library 
    * Zipkin Lens UI
      * bundled in SkyWalking booster UI since 9.4.0
      * `/zipkin` -- is exposed by -- SkyWalking webapp
    * [Jaeger](https://github.com/jaegertracing/jaeger)
      * if `COLLECTOR_ZIPKIN_HTTP_PORT=9411` is set -> Jaeger exposes a
        * partial implementation of Zipkin's HTTP POST endpoints
          * http port 9411 accepts POST requests
            * `/api/v1/spans` (thrift, json)
            * `/api/v2/spans` (json, proto) 
      * if `SPAN_STORAGE_TYPE=kafka` and `zipkin-thrift` -> Jaeger reads
        * Zipkin v1 thrift encoded span messages | Kafka topic.
          * Note: The above is a [deprecated practice](https://github.com/openzipkin/zipkin/tree/master/zipkin-collector/kafka#legacy-encoding) in Zipkin. Most instrumentation bundle multiple spans per message in v2 format.
    * [Pitchfork](https://github.com/HotelsDotCom/pitchfork)
      * exposes
        * == HTTP POST endpoints Zipkin
          * http port 9411 accepts POST requests
            * `/api/v1/spans` (thrift, json)
            * `/api/v2/spans` (json, proto) 
