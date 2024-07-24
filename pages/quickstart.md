---
title: Quickstart
weight: 1
---

* Goal
  * build and start an instance of Zipkin locally
* "http://your_host:9411" 
  * default port to find traces!

## Docker

* [Docker Zipkin](https://github.com/openzipkin/docker-zipkin)
  * build docker images
  * provide
    * scripts and
    * pre-built images
      * Docker Compose
        * [Check an example here](https://github.com/openzipkin/zipkin/blob/master/docker/examples/docker-compose.yml)
        * `docker compose up`
      * run the latest image directly

    ~~~ bash
    docker run -d -p 9411:9411 openzipkin/zipkin
    ~~~

## Java
* requirements
  * Java v17+
* `curl -sSL https://zipkin.io/quickstart.sh | bash -s`
  * fetch the [latest release](https://search.maven.org/remote_content?g=io.zipkin&a=zipkin-server&v=LATEST&c=exec)
* `java -jar zipkin.jar`
  * run the executable

## Homebrew
* `brew install zipkin`
* ways to run
  * `zipkin`
    * foreground
  * `brew services start zipkin`
    * background

## Running from Source

* uses
  * you are developing new features | zipkin
* `git clone https://github.com/openzipkin/zipkin`
* `cd zipkin`
* `./mvnw -T1C -q --batch-mode -DskipTests --also-make -pl zipkin-server clean package`
  * Build the server and also make its dependencies
* available servers to run
  * `java -jar ./zipkin-server/target/zipkin-server-*exec.jar`
    * common server
  * `java -jar ./zipkin-server/target/zipkin-server-*slim.jar`
    * slim server
