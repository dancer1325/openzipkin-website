---
title: Tracers and Instrumentation
weight: 3
---

* Tracing information
  * collected | each host -- via the -- instrumented libraries
  * -- sent to -- Zipkin
  * how does it work?
    * host -- makes a request to -- another application / 
      * few tracing identifiers -- along -- request -> data is tied together | spans

### Supported by Zipkin

| Language | Library | Framework | Propagation Supported | Transports Supported | Sampling Supported? | Other notes |
|:---------|:--------|:----------|:----------------------|:---------------------|:--------------------|:------------|{% for lib in site.data.tracers_instrumentation %}
| {{ lib.language }} | {{ lib.library }} | {{lib.framework}} | {{ lib.propagation }} | {{ lib.transports }} | {{ lib.sampling }} | {{ lib.notes }} |{% endfor %}
{: .wide-table}


### Community supported

| Language | Library | Framework | Propagation Supported | Transports Supported | Sampling Supported? | Other notes |
|:---------|:--------|:----------|:----------------------|:---------------------|:--------------------|:------------|{% for lib in site.data.community_tracers_instrumentation %}
| {{ lib.language }} | {{ lib.library }} | {{lib.framework}} | {{ lib.propagation }} | {{ lib.transports }} | {{ lib.sampling }} | {{ lib.notes }} |{% endfor %}
{: .wide-table}

Did we miss a library? Please open a pull-request to
[openzipkin.github.io](https://github.com/openzipkin/openzipkin.github.io).

Want to create instrumentation for another framework or platform? We have documentation on [instrumenting a library]({{ site.github.url }}/pages/instrumenting).
