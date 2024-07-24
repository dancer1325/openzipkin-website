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
* TODO: 
If you have Java 17 or higher installed, the quickest way to get started is to fetch the [latest release](https://search.maven.org/remote_content?g=io.zipkin&a=zipkin-server&v=LATEST&c=exec) as a self-contained executable jar:

~~~ bash
curl -sSL https://zipkin.io/quickstart.sh | bash -s
java -jar zipkin.jar
~~~

## Homebrew

If you have [Homebrew](https://brew.sh/) installed, the quickest way to get started is to install
the [zipkin formula](https://formulae.brew.sh/formula/zipkin).

~~~ bash
brew install zipkin
# to run in foreground
zipkin
# to run in background
brew services start zipkin
~~~

## Running from Source

Zipkin can be run from source if you are developing new features. To achieve this, you'll need to
get [Zipkin's source](https://github.com/openzipkin/zipkin) and build it.

~~~ bash
# get the latest source
git clone https://github.com/openzipkin/zipkin
cd zipkin
# Build the server and also make its dependencies
./mvnw -T1C -q --batch-mode -DskipTests --also-make -pl zipkin-server clean package
# Run the server
java -jar ./zipkin-server/target/zipkin-server-*exec.jar
# or Run the slim server
java -jar ./zipkin-server/target/zipkin-server-*slim.jar
~~~

Stop by and socialize with us on [gitter](https://gitter.im/openzipkin/zipkin), if you end up making something interesting!
