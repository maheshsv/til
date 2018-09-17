# ElasticSearch Concepts and High Level API

> **Elasticsearch** is a [search engine](https://en.wikipedia.org/wiki/Search_engine_(computing)) based on [Lucene](https://en.wikipedia.org/wiki/Lucene). It provides a distributed, [multitenant](https://en.wikipedia.org/wiki/Multitenancy)-capable [full-text search](https://en.wikipedia.org/wiki/Full-text_search) engine with an [HTTP](https://en.wikipedia.org/wiki/HTTP) web interface and schema-free [JSON](https://en.wikipedia.org/wiki/JSON) documents.

## Basic Concepts:

- Cluster: A cluster is a collection of one or more nodes (servers) that together holds your entire data and provides federated indexing and search capabilities across all nodes.
- Node: A node can be configured to join a specific cluster by the cluster name.
- Index: An index is a collection of documents that have somewhat similar characteristics.

- Document: A document is a basic unit of information that can be indexed. 

- Shards & Replicas: each index is devided into multiple shards and each shard can have one or more replicas.

### [High Level REST Client](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/master/java-rest-high.html)

> The Java High Level REST Client works on top of the Java Low Level REST client. Its main goal is to expose API specific methods, that accept request objects as an argument and return response objects, so that request marshalling and response un-marshalling is handled by the client itself.

Java high level REST client includes REST APIs such as Document index, get, exists, delete, update, bulk update, multi-get, re-index, update by query, delete by query API, search APIs and various other APIs.

