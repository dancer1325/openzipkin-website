---
title: Architecture
weight: 2
---

Architecture Overview
----------------------

* Tracers
  * live | applications
  * allows
    * recording 👁️timing and metadata 👁️ about operations / took place
  * uses
    * instrument libraries
      * -> their use -- is transparent to -- users
  * _Example:_ instrumented web server / records when it
    * received a request
    * sent a response 
  * [available ones / platform]({{ site.github.url}}/pages/tracers_instrumentation)
* Span
  * := trace data collected
* Instrumentation
  * design
    * safe in production
    * little overhead ->
      * 👁 for trace in progress️ -- ONLY propagate IDs in-band / tell to the -- receiver 👁️
        * if you need to make an outgoing HTTP request, -- few headers (NOT the operationName) are added to -- propagate IDs 
      * completed spans -- are reported 👁️ out-of-band 👁️, to -- Zipkin
        * == 👁️asynchronously 👁️
          * Reason: 🧠 prevent delays or failures | user code 🧠
* Reporter
  * := component | instrumented app / -- sends data to -- Zipkin
    * data -- is sent via >= 1 transports, to -- Zipkin Collectors / persist it | storage
    *  data provided | Zipkin UI -- is retrieved via the Zipkin API, from the -- storage
* Transport
  * media / spans sent by the instrumented library -- are transported to -- Zipkin Collectors 
  * primary transports
    * HTTP
    * Kafka
    * Scribe
* Zipkin == collector + storage + searchOrQuery + web UI
  * collector
    * collector daemon, about the trace data,
      * validate
      * store
      * index
  * storage
    * pluggable / 
      * natively support
        * Cassandra
        * ElasticSearch
        * MySQL
      * could exist TP extensions 
    * originally, just to store | Cassandra
      * Reason: scalable, flexible schema, and heavily used | Twitter
  * searchOrQuery
    * searchOrQuery daemon -- provides a -- simple JSON API / find and retrieve traces
      * primary consumer of this API --  Web UI
  * web UI
    * == GUI / nice interface -- for viewing -- traces
      * traces -- are based on -- service, time, and annotations
      * NO built-in authentication | UI!

![Zipkin architecture]({{ site.github.url }}/public/img/architecture-1.png)

---

Example flow
-----------------------

* http tracing / user code -- calls -- /foo
  * once, user received a http response -- 1! span is sent asynchronously to -- Zipkin 


```
┌─────────────┐ ┌───────────────────────┐  ┌─────────────┐  ┌──────────────────┐
│ User Code   │ │ Trace Instrumentation │  │ Http Client │  │ Zipkin Collector │
└─────────────┘ └───────────────────────┘  └─────────────┘  └──────────────────┘
       │                 │                         │                 │
           ┌─────────┐
       │ ──┤GET /foo ├─▶ │ ────┐                   │                 │
           └─────────┘         │ record tags
       │                 │ ◀───┘                   │                 │
                           ────┐
       │                 │     │ add trace headers │                 │
                           ◀───┘
       │                 │ ────┐                   │                 │
                               │ record timestamp
       │                 │ ◀───┘                   │                 │
                             ┌─────────────────┐
       │                 │ ──┤GET /foo         ├─▶ │                 │
                             │X-B3-TraceId: aa │     ────┐
       │                 │   │X-B3-SpanId: 6b  │   │     │           │
                             └─────────────────┘         │ invoke
       │                 │                         │     │ request   │
                                                         │
       │                 │                         │     │           │
                                 ┌────────┐          ◀───┘
       │                 │ ◀─────┤200 OK  ├─────── │                 │
                           ────┐ └────────┘
       │                 │     │ record duration   │                 │
            ┌────────┐     ◀───┘
       │ ◀──┤200 OK  ├── │                         │                 │
            └────────┘       ┌────────────────────────────────┐
       │                 │ ──┤ asynchronously report span     ├────▶ │
                             │                                │
                             │{                               │
                             │  "traceId": "aa",              │
                             │  "id": "6b",                   │
                             │  "name": "get",                │
                             │  "timestamp": 1483945573944000,│
                             │  "duration": 386000,           │
                             │  "annotations": [              │
                             │--snip--                        │
                             └────────────────────────────────┘
```