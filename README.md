# ELK Stack

A simple [ELK](https://www.elastic.co/elk-stack) setup with docker-compose inspired by [deviantony](https://github.com/deviantony/docker-elk).

Utilizing the official Docker images from Elastic, with exposed ports:

* [elasticsearch](https://github.com/elastic/elasticsearch-docker)
  * 9200: Elasticsearch HTTP
  * 9300: Elasticsearch TCP transport
* [logstash](https://github.com/elastic/logstash-docker)
  * 5000: Logstash TCP input
* [kibana](https://github.com/elastic/kibana-docker)
  * 5601: Kibana

## Setup

#### FIRST setup .env file in root

`.env` example:

```shell
# General
ELASTIC_VERSION=6.3.0
ES_JAVA_OPTS=-Xmx256m -Xms256m

# elasticsearch
CLUSTER_NAME=elk-docker-cluster
NETWORK_HOST=0.0.0.0
DISCOVERY_ZEN_MINIMUM_MASTER_NODES=1
DISCOVERY_TYPE=single-node

# logstash
HTTP_HOST=0.0.0.0
PATH_CONFIG=/usr/share/logstash/pipeline

# kibana
SERVER_NAME=kibana
SERVER_HOST=0
ELASTICSEARCH_URL=http://elasticsearch:9200
```

| Variable          | Description                                                                                                                                      |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| ELASTIC_VERSION   | Sync stack versions                                                                                                                              |
| ES_JAVA_OPTS      | [JVM Tuning](https://github.com/deviantony/docker-elk#jvm-tuning)                                                                                |
| <br>              | <br>                                                                                                                                             |
| CLUSTER_NAME      | [Cluster Description](https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster.name.html)                                         |
| NETWORK_HOST      | [To communicate and form a cluster with nodes on the servers](https://www.elastic.co/guide/en/elasticsearch/reference/current/network.host.html) |
| NETWORK_HOST      | [To prevent data loss](https://www.elastic.co/guide/en/elasticsearch/reference/6.3/discovery-settings.html#minimum_master_nodes)                 |
| DISCOVERY_TYPE    | [For testing usage of transport client](https://www.elastic.co/guide/en/elasticsearch/reference/6.3/bootstrap-checks.html#single-node-discovery) |
| <br>              | <br>                                                                                                                                             |
| HTTP_HOST         | [To set the http.bind_host and the http.publish_host](https://www.elastic.co/guide/en/elasticsearch/reference/6.3/modules-http.html)             |
| PATH_CONFIG       | [Location of pipline configs](https://www.elastic.co/blog/logstash-multiple-pipelines)                                                           |
| <br>              | <br>                                                                                                                                             |
| SERVER_NAME       | [A human-readable display name that identifies this Kibana instance](https://www.elastic.co/guide/en/kibana/current/settings.html)               |
| SERVER_HOST       | [This setting specifies the host of the back end server](https://www.elastic.co/guide/en/kibana/current/settings.html)                           |
| ELASTICSEARCH_URL | [The URL of the Elasticsearch instance to use for all your queries](https://www.elastic.co/guide/en/kibana/current/settings.html)                |

## Usage

```console
# Create and configure
$ touch .env && vim $_

# start
$ docker-compose up

# stop
$ doccker-compose down
```
