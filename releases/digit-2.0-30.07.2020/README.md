# DIGIT 2.0 \(30.07.2020\)

## **New Features:** <a id="new-features"></a>

* Ability to handle [advanced payments](https://digit-discuss.atlassian.net/wiki/spaces/ED/pages/604307457/Release+Notes+for+Advance+Payment+implementation+in+W+S) - platform and Reference implementation in W&S.
* Advance Collection integration with W&S
  * API Contracts

## **Enhancements:** <a id="enhancements"></a>

* Bulk persister changes to support bulk persisting for migration in Persister Service.
* Localization URL params to be changed to request params in Localization service
* Receipt download link in SMS and email notifications.
* Rainwater Harvesting attribute in Property Service
* Filestore service enhancement - Support for SDC and S3 implementation.
* Maven dependencies upgrade and merging the backend services to the master branch \(Upgraded Tracer to 2.0.0, spring boot to 2.2.6, flyway-core to 6.4.3, etc along with code cleanup\) for all the services across the services. The Changelog has been added.
* Baseline versioning of all the services as per the streaming strategy.
* UI Enhancements
  * Generalized Client-side PDF generation component and integration with Property, Fire NOC, Trade License, and W&S applications\).
  * Generalize acknowledgment screens component
  * MDMS namespace common component and integration with PT and TL modules.

## **New Features:** <a id="new-features-1"></a>

**Infra and Operations Simplification**

* Infra & Service monitoring v1.0.0 \(Prometheus, Alertmanager & Grafana\)
  * Cluster Resource monitoring
  * Request Traffic monitoring
  * DIGIT Service monitoring
* All Java based services SpringBoot upgraded from 1.5.X to 2.2.6 for better security, performance and metrics.
* Backbone Services migrated to Helm templates to ease deployment on kubernetes.
* Introduced Minio as a digit platform service for SDCs to leverage S3 like object storage feature.
* DIGIT on Spot Instances for AWS users, saves 60% of the cloud cost.
* Configurable SSO with GitHub or Google SSO oauth for all the Infra apps like Jaeger, Grafana, Kibana.
* DIGIT Jenkins as a service
* 
## **Enhancements:** <a id="enhancements-1"></a>

* Versioned Git Tags for all the services
* Versioned MDMS and Config data.

