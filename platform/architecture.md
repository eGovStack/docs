---
description: DIGIT Infra and architecture details
---

# Architecture

DIGIT is India’s largest open-source platform for digital governance. It is built on OpenAPI (OAS 2.0) and provides API-based access to a variety of urban/municipal services enabling state governments and city administrators to provide citizen services with relevant new services and also integrating the existing system into the platform and run seamlessly on any commercial/on-prem cloud infrastructure with scale and speed.

### Key Architecture Highlights <a href="#key-architecture-highlights" id="key-architecture-highlights"></a>

* DIGIT is a microservices-based platform that is built to scale. Microservices are small, autonomous and developer-friendly services that work together.

![](<../.gitbook/assets/image (84).png>)

* A big software or system can be broken down into multiple small components or services. These components can be designed, developed & deployed independently without compromising the integrity of the application.
* Parallelism in development: Microservices architectures are mainly business-centric.
* MicroServices have smart endpoints that process info and apply logic. They receive requests, process them, and generate a response accordingly.
* Decentralized control between teams, so that its developers strive to produce useful tools that can then be used by others to solve the same problems.

![](<../.gitbook/assets/image (85) (1).png>)

* MicroServices architecture allows its neighbouring services to function while it bows out of service. This architecture also scales to cater to its clients’ sudden spike in demand.
* MicroService is ideal for evolutionary systems where it is difficult to anticipate the types of devices that may be accessing our application.

![](<../.gitbook/assets/image (36).png>)

![](<../.gitbook/assets/image (13) (1) (1).png>)

### Multi-layer Architecture

DIGIT follows Multilayer or n-tiered distributed architecture pattern. As seen in the illustration above there are different horizontal layers with some set of components eg. Data Access Layer, Infra Services, Business Services, different modules layers, client Apps and some vertical adapters. Every layer consists of a set of microservices. Each layer of the layered architecture pattern has a specific role and responsibility within the application.

* Layered architecture increases flexibility, maintainability, and scalability
* Multiple applications can reuse the components
* Parallelism
* Different components of the application can be independently deployed, maintained, and updated, on different time schedules
* Layered architecture also makes it possible to configure different levels of security to different components
* Layered architecture also helps users test the components independent of each other

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
