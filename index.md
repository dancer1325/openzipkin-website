---
title: Home
weight: 0
---
* Zipkin
  * := distributed tracing system
  * allows
    * gathering timing data
      * uses
        * troubleshoot latency problems | service architectures
    * looking up this data -- via --
      * trace Id 
        * normally stored | log file
      * attributes
        * *Example:* service, operation name, tags and duration
    * summarizing some data for you
      * _Example:_ percentage of time spent | service, operations failed or suceed

    ![Trace view screenshot]({{ site.github.url }}/public/img/web-screenshot.png)

    * displaying dependency diagram about how many traced requests -- went through -- each application
      * uses
        * check aggregated behavior

    ![Dependency graph screenshot]({{ site.github.url }}/public/img/dependency-graph.png)

* requirements | applications
  * configure a [tracer or instrumentation library]({{ site.github.url }}/pages/tracers_instrumentation)
    * allows
      * reporting trace data to -- Zipkin
        * ways to report it
          * HTTP
          * Kafka
          * Apache ActiveMQ
          * gRPC
          * RabbitMQ
  * store data / -- served to -- Zipkin UI
    * ways
      * in-memory
      * persistently -- with a -- supported backend
        * *Example:* Apache Cassandra or Elasticsearch

## Where to go next?

 * [Quickstart guide]({{ site.github.url }}/pages/quickstart)
   * try out Zipkin 
 * [tracer or instrumentation library]({{ site.github.url }}/pages/tracers_instrumentation)
   * check if your platform support it 
 * [server extension or alternative]({{ site.github.url }}/pages/extensions_choices)
   * check if it's relevant | your site
 * [Zipkin Gitter chat channel](https://gitter.im/openzipkin/zipkin)
 * [openzipkin/zipkin](https://github.com/openzipkin/zipkin/)
 * [Zipkin issues](https://github.com/openzipkin/zipkin/issues)
