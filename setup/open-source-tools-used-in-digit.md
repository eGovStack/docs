---
description: Overall tool stack used in DIGIT
---

# Open Source Tools used in DIGIT

DIGIT being an open source platform, all the tools and tech stack used to build, deploy and operate DIGIT - are also [open source](https://opensource.com/resources/what-open-source) and community edition.  All the various tools used are listed below with the specific versions used and their short description.

| Platform Tools |  Version | Description | License Type |
| :--- | :--- | :--- | :--- |
| [Kafka](https://kafka.apache.org/intro) | 5.4.1 | Apache **Kafka** is a open sourced and community distributed event streaming platform capable of handling trillions of events a day. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [Zookeeper](https://dattell.com/data-architecture-blog/what-is-zookeeper-how-does-it-support-kafka/) | 5.4.1 | **ZooKeeper** is an **open source** Apache project that provides a centralized service for providing configuration information, naming, synchronization and group services over large clusters in distributed systems. When working with Apache **Kafka**, **ZooKeeper** is primarily used to track the status of nodes in the **Kafka** cluster and maintain a list of **Kafka** topics and messages. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [Zuul](https://blog.heroku.com/using_netflix_zuul_to_proxy_your_microservices) | 2.2.2 | **Zuul** is an open sourced edge service that proxies requests to multiple backing services. It provides a unified “front door” to your system, which allows a browser, mobile app, or other user interface to consume services from multiple hosts without managing cross-origin resource sharing \(CORS\) and authentication for each one. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [Elasticsearch](https://www.elastic.co/what-is/elasticsearch) | 6.6.2 | _**Elasticsearch**_ is a distributed, free and open search and analytics engine for all types of data, including textual, numerical, geospatial, structured and unstructured. | [Elastic License 2.0](https://github.com/elastic/kibana/tree/7.13/licenses/ELASTIC-LICENSE-2.0.txt) |
| [Kibana](https://www.elastic.co/what-is/kibana) | 6.6.2 | _**Kibana**_ is a free and open frontend application that sits on top of the Elastic Stack, providing search and data visualization capabilities for data indexed in Elasticsearch. | [Elastic License 2.0](https://github.com/elastic/kibana/tree/7.13/licenses/ELASTIC-LICENSE-2.0.txt) |
| [fluentbit](https://fluentbit.io) | 1.0.6 | _**Fluent Bit**_ is an open source and multi-platform Log Processor and Forwarder which allows you to collect data/logs from different sources, unify and send them to multiple destinations. It's fully compatible with Docker and Kubernetes environments. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [Postgresql](https://www.postgresql.org/) | 9.6 and 10.6 | _**PostgreSQL**_ is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance | [PostGres License](https://www.postgresql.org/about/licence/) |
| [redis](https://redis.io/) | 3.2.6 | _**Redis**_ is an open source \(BSD licensed\), in-memory data structure store, used as a database, cache, and message broker. Redis provides data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes, and streams. | [BSD License](https://snyk.io/learn/what-is-bsd-license/) |
| [Jaeger](https://www.jaegertracing.io/) | 1.18 | _**Jaeger**_ is open source software for tracing transactions between distributed services. It's used for monitoring and troubleshooting complex microservices environments. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |

| Dev Stack | Version | Description | License Type |
| :--- | :--- | :--- | :--- |
| [OpenJDK](https://openjdk.java.net/) | 8u212 | _**OpenJDK**_ is completely **open source** and can be used it freely | [GPL-2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html) |
| [SpringBoot](https://spring.io/projects/spring-boot) | 2.2.6 | _**Spring Boot**_ is an open-source micro framework maintained by a company called Pivotal. It provides Java developers with a platform to get started with an auto configurable production-grade Spring application. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [React](https://reactjs.org/docs/how-to-contribute.html#:~:text=React%20is%20one%20of%20Facebook's,to%20everybody%20on%20facebook.com.) | 16.7.0 | _**React**_ is one of Facebook's first **open source** projects that is both under very active development and is also being used to ship code to everybody on facebook.com. | [MIT](https://www.mit.edu/~amini/LICENSE.md) |
| [Material-UI-React](https://material-ui.com/) | 16.8.0 | **Material**-**UI** CE \(Community Edition\) has been 100% **open**-**source** \(MIT\) since the very beginning, and always will be. Developers can ensure **Material**-**UI** is the right choice for their React applications through **Material**-**UI's** community maintenance strategy. | [MIT](https://www.mit.edu/~amini/LICENSE.md) |
| [NodeJS](https://github.com/nodejs/node) | 8.4.0 | Node. js is an **open**-**source**, cross-platform, JavaScript runtime environment. It executes JavaScript code outside of a browser. | [MIT](https://www.mit.edu/~amini/LICENSE.md) |



| DevOps Stack | Version | Description | License Type |
| :--- | :--- | :--- | :--- |
| Kubernetes | 1.18.x | _Kubernetes_, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| Docker | 19.x | _Docker_, a subset of the Moby project, is a software framework for building, running, and managing containers on servers and the cloud. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| Helm | 3.x.x | _Helm_ helps you manage Kubernetes applications — _Helm_ Charts help you define, install, and upgrade even the most complex Kubernetes. | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| [Terraform](https://www.terraform.io/) | v0.14.10 | Terraform allows infrastructure to be expressed as code in a simple, human readable language called HCL \(HashiCorp Configuration Language\). | [Mozilla Public _License_ 2.0](https://github.com/hashicorp/terraform/blob/main/LICENSE) |
| Jenkins | 2.289 | _Jenkins_ – an open source automation server which enables developers around the world to reliably build, test, and deploy their software. | [MIT](https://www.mit.edu/~amini/LICENSE.md) |
| Go Lang | 1.13.3 | Go is an open source programming language that makes it easy to build simple, reliable, and efficient software. | [3-clause BSD + patent grant](https://golang.org/LICENSE) |
| Groovy | 3.0 | Apache _Groovy_ is a powerful, optionally typed and dynamic language, with static-​typing and static compilation capabilities, for the Java platform aimed at improving developer productivity thanks to a concise, **familiar and easy to learn syntax**.  | [Apache **License** 2.0](https://www.apache.org/licenses/LICENSE-2.0) |
| Python | [v3.9.6](https://github.com/python/cpython/releases/tag/v3.9.6) | _Python_ software and documentation are licensed under the PSF _License_ Agreement. Starting with _Python_ 3.8.6, | PSF |
| [Sops](https://github.com/mozilla/sops/blob/master/LICENSE) | [v3.7.1](https://github.com/mozilla/sops/releases/tag/v3.7.1) | **sops** is an editor of encrypted files that supports YAML, JSON, ENV, INI and BINARY formats and encrypts with AWS KMS, GCP KMS, Azure Key Vault, age, and PGP.  | [Mozilla Public _License_ 2.0](https://github.com/hashicorp/terraform/blob/main/LICENSE) |
| Ansible | v2.9.23 | _Ansible_ is an open source community project sponsored by Red Hat, it's the simplest way to automate IT.  | GNU General Public **License** |
| [yaml](https://blog.stackpath.com/yaml/) | 1.2 | YAML is a human-readable data serialization standard that can be used in conjunction with all programming languages and is often used to write configuration files. | [License](https://github.com/yamlcss/yaml/blob/master/License.txt) |



