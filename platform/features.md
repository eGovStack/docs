# Features

DIGIT is an open-source platform licensed under the MIT license ([https://opensource.org/licenses/MIT](https://opensource.org/licenses/MIT)) compliant with the NUIS digital blueprint.

Detailed mapping of DIGIT’s capabilities with the core requirements mentioned in the NUIS digital blueprint has been done below:

| Key Principles                               | Description                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Interoperability                             | <ol><li>DIGIT is designed as an API-first platform and with Open APIs &#x26; Open Standard interoperability is maintained.</li><li>Along with this, taxonomies are available for the key domain entities/registries on DIGIT.</li></ol>                                                                                                                                                                         |
| Data privacy and security by design          | <ol><li>Data privacy and security design are a very critical part of the design of DIGIT.</li><li>Core service layer of DIGIT includes a signing and encryption service that provides capabilities to sign/encrypt/mask sensitive data.</li><li>Appropriate access controls can be defined in the APIs to ensure authorised access to sensitive data</li></ol>                                                  |
| Transparency and Accountability through data | <p>DIGIT has</p><ol><li>The capability to define registries, preferably through standard specifications like OpenAPI 3.0</li><li>The capability to configure registry attributes for security and protection as per the configuration.</li><li>Mechanisms to verify data and its provenance through audit logs (access and changelogs), preferably through APIs.</li></ol>                                      |
| Reusability and Extensibility                | <ol><li>The DIGIT platform is designed as a collection of more than 55+ atomic microservices which are bundled together in a given context to provide an end solution.</li><li>DIGIT allows the extension of existing capabilities without needing architectural interventions.</li><li>Components are designed to be independently reusable without any tight coupling.</li></ol>                              |
| Evolvability and Scale                       | <p>On DIGIT:</p><ol><li>Capabilities can be added without needing overall system re-architecture.</li><li>Individual components can evolve separately to enable heterogeneous evolution of the system.</li><li>Scaling can be done horizontally to handle changes in request volumes.</li><li>Individual components can be scaled independent of each other, to enable efficient resource utilisation</li></ol> |
| Multi-channel access                         | <ol><li>DIGIT allows multiple channels of solution delivery - ULB counters, Web portals, Mobile App, WhatsApp Chatbot and 3rd party applications like Paytm, tablets, etc.</li><li>DIGIT’s access control mechanism can be configured to provide different levels of access based on channels and roles.</li></ol>                                                                                              |
| Ecosystem-driven                             | <ol><li>DIGIT leverages open source technologies to reduce the cost of solutions.</li><li>Leverages or integrates with or extends existing platforms/stacks like IndiaStack, IUDX, ICTRA infrastructure etc.</li><li>Provides the capability to gather feedback from the ecosystem in a digital manner.</li></ol>                                                                                               |

### Interoperability&#x20;

Data specifications/models are available for domain entities. DIGIT is designed as an API-first platform wherein data specs/models are created for all key entities thus ensuring interoperability through open APIs and open standards. Taxonomies are available for the key domain entities/registries. These can later be harmonised with standard taxonomies in the domain as and when they are made available.&#x20;

DIGIT data models and APIs are published as Open APIs freely available to everyone in the ecosystem. In Punjab, the DIGIT module was easily integrated with 3rd party payment apps like Paytm, Airtel Money, BBPS, etc to increase citizen access and improve collections. At present, DIGIT provides at least 3 key distinct APIs for all domain entities - create, update and search.&#x20;

Deactivation/Cancellation of key entities in DIGIT is achieved through updating their status to inactive as per their defined specification/API contracts. Given the API-first and micro-services-driven nature of DIGIT, current APIs and models can be quickly harmonised with national standards as and when they are made available. DIGIT strives to leverage established domain standards (national/international) wherever available.&#x20;

## Data Privacy And Security By Design&#x20;

### Data Privacy&#x20;

Data privacy capabilities are available to mark and protect sensitive data. The core service layer of DIGIT includes signing and encryption service as one of the core services that provide capabilities to sign/encrypt/mask sensitive data. It is designed such that it can work against software key stores and can be extended to integrate with any kind of hardware key store to store and protect signing and encryption keys.&#x20;

Encryption requirements can be defined and adhered to for the storage of sensitive data. DIGIT requires the User PII data to be stored in its User service which is by default enabled for encryption of sensitive data as User Data Vault. All other services in DIGIT are required to access PII data by explicitly calling the User service - which in turn audits all access to PII. In addition, individual services in DIGIT can leverage DIGIT’s signing and encryption service (which is what User Service leverages to create User Data Vault) to further protect additional sensitive data available with the services. &#x20;

DIGIT provides the capability to define workflows for data modification that can be configured to have approval steps to get needed consent for any data modification activities. DIGIT currently provides RBAC (Role-Based Access Control) based access control for access (search) to data.&#x20;

### Security&#x20;

Appropriate access controls can be defined in the APIs to ensure authorised access to sensitive data. DIGIT is designed to handle authentication and authorisation as perimeter control at its API gateway layer to ensure unauthorised calls are not allowed to even contact the respective micro-services. DIGIT provides an RBAC (Role-Based Access Control) mechanism where users are explicitly provided access to relevant resources by assigning them appropriate roles. By default, DIGIT supports OAUTH-based authentication for individual users and APIs. However, the Authentication and Authorization filter on DIGIT is designed to be easily extendable to support any further Auth and Auth needs.&#x20;

Perimeter security mechanism in DIGIT also helps developers in focusing on the functional developments in further services and offloading the access control requirements for new resources and their APIs to the API gateway using simple configurations.&#x20;

DIGIT also ensures that risks like the following are taken care of:&#x20;

* Privilege escalation – form field manipulation&#x20;
* Failure to restrict URL access&#x20;
* Insecure direct object references (IDOR)&#x20;
* Malicious file upload leads to cross-site scripting&#x20;
* Improper authentication&#x20;
* Missing account lockout&#x20;
* Request throttling attack&#x20;
* Weak encoding mechanism&#x20;
* Sensitive information in URL&#x20;
* Lack of automatic session expiration&#x20;
* Insecure banner implementation&#x20;
* Concurrent session&#x20;
* Clickjacking&#x20;
* Improper error handling

### Transparency And Accountability Through Data&#x20;

DIGIT has the capability to define key registries in OpenAPI 3.0 specs formats and easily achieve key APIs like create/update/search using its building blocks in core services mainly through configurations and using lightweight extensions on a needs basis.

DIGIT has the capability to protect person-specific sensitive data by encrypting them in the user data vault (User Registry) which allows configuration-based protection of sensitive PII. DIGIT requires additional registries to reference PII using this mechanism. In addition, registries in DIGIT can leverage its data protection (Signing and Encryption) core service to provide additional protection to registry-specific attributes.&#x20;

Registry data in DIGIT can be signed for tamper-proofing using its signing and encryption core service. A proof of concept for this has already been done on the ePass module that was built on the DIGT platform. All key data modifications in DIGIT are access logged to provide an audit trail, which can be accessed through APIs. The upcoming version of DIGIT is planning to bring in the concept of immutable event logs to further strengthen this capability. DIGIT leverages open-source telemetry to provide the ability to gather telemetry data and extends it for the DIGIT-specific processing pipeline. This framework allows for additional event definitions and contextual extension of the telemetry processing pipeline thereby future-proofing this capability in DIGIT.

### Reusability and Extensibility&#x20;

DIGIT platform is designed as a collection of more than 50+ atomic microservices which are bundled together in a given context to provide end solutions. Microservices in DIGIT can be mainly categorized in three categories: Data services (Registries, reference Master data management, etc.), Tech infrastructure services (Authentication, authorisation, notification engine etc.) and domain services (Assessment, NOC etc.). Citizen, employee and administrative interfaces in DIGIT use these microservices to achieve the needed functionality.&#x20;

Data models and APIs in DIGIT are defined as OpenAPI 3.0 specifications and can be extended by using a combination of configuration and extension techniques. E.g. if the additional attributes are only needed to be stored with format validation, it can be a simple schema extension, while if the additional business checks/functionality need to be implemented using the extended attributes then it can be achieved using pre/post request filters or extending underlying microservices.&#x20;

DIGIT allows extension of existing capabilities without needing architectural interventions. As described above extension of existing functionality on DIGIT can be achieved using additional configurations, additional extension services or request/response filters.&#x20;

Several partners have extended DIGIT modules to cater to new use cases. For instance DIGIT mCollect module caters to collection of fees for more than 50 services on the counter, but it did not have a citizen interface for payment of these services online. Directorate General Defence Estates (DGDE) wanted to introduce this interface for the citizen’s of cantonment boards in India and were able to easily enhance the mCollect module to include this capability. Similarly Punjab has reused several DIGIT core services to develop new modules on the platform with minimum efforts.&#x20;

DIGIT supports single-instance multi-tenancy to enable sharing of the underlying infrastructure, also all DIGIT data models and services are designed to be multi-tenanted.&#x20;

DIGIT uses API first approach in its design and development to ensure loose coupling between its various components. These APIs are clearly defined using OpenAPI 3.0 specifications to ensure clear documentation.

### Evolvability and Scale&#x20;

As described above, extension of existing functionality on DIGIT can be achieved using additional configurations, additional extension services or request/response filters. Similarly new functionality can be added by rebundling existing building blocks in context of new use cases and implementing only additionally required services without requiring any architectural overhaul. Additionally due to its loosely coupled API driven design DIGIT allows for new components to be implemented in the technology that is most useful for that use case.&#x20;

API driven, microservices based architecture of DIGIT enables its components to evolve separately. On DIGIT Individual components can evolve separately to enable heterogeneous evolution of the system.&#x20;

DIGIT uses SemVer 2.0 for versioning of its microservices and interfaces. Semantic versioning is a formal convention for specifying compatibility using a three-part version number: major version; minor version; and patch. More details on this can be found on this link: https://semver.org/.&#x20;

DIGIT is designed to be horizontally scalable. Microservices based architecture of DIGIT also enables it to scale only needed components/services, thereby providing resource efficiency. E.g. Billing and Collection services can be scaled separately during financial year closing if the load pattern indicates increasing volume of bill payments during that period.&#x20;

DIGIT is designed to be hardware agnostic and can be run on any hardware. It has been tested on multiple commercial clouds and state sponsored bare metal infrastructure. Components of DIGIT that need to use underlying hardware have been carefully chosen (in case where DIGIT is using other open source components) or designed (DIGIT’s own components) to provide a layer of abstraction that can be extended for any types of hardware.

### Multi-channel Access&#x20;

DIGIT is designed using API first approach, therefore enabling any user interface channel to leverage it. DIGIT’s own user interfaces (Web/mobile app, WhatsApp chatbot) are implemented using its APIs to ensure offered platform capabilities and data are accessible to any delivery channel based on configured policies. In states like Punjab and AP where DIGIT modules are being used, the citizens have been given multi-channel access - ULB counters, Web portals, Mobile App, WhatsApp Chatbot and 3rd party applications like Paytm, BBPS to avail local government services.&#x20;

DIGIT’s access control mechanism can be configured to provide different levels of access based on channels and roles.

### Ecosystem-driven&#x20;

DIGIT platform and its user interfaces are completely open source. Also, all external components used in DIGIT are also Open Source.\
Due to its API based and event driven architecture DIGIT can be integrated with any existing stack. Wherever appropriate, DIGIT also provides out of box integrations with crucial stacks/platforms. The most common integrations are to payment gateways, SMS providers and SMTP email servers for a typical implementation.&#x20;

More than 14 organizations have already partnered with us to implement DIGIT across multiple implementations in the country and have built more than 20 new solutions on top of the platform.&#x20;

DIGIT also provides the capability to gather feedback from the ecosystem in a digital manner. Feedback capability in DIGIT can be looked at the following levels:&#x20;

* Service Delivery feedback on services offered through DIGIT - DIGIT provides a highly configurable and extensible Public Grievance module to enable this kind of feedback/redressal for functional users (Citizens, employees etc)&#x20;
* Service Usage feedback - DIGIT user interfaces include a telemetry SDK which is backed by telemetry infrastructure in DIGIT platform. Coupled with API access logs, this enables DIGIT to gather usage feedback through live action and can be used for fine tuning interfaces and APIs&#x20;
* Design/Feature feedback - As an open source project on github, DIGIT provides a mechanism to provide comments/feedback on its various components using github. This feedback can be leveraged to create a Point of View on the future roadmap for the platform.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
