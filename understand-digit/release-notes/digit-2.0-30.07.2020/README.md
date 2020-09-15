---
description: Baselined and Standardised Release
---

# DIGIT 2.0 \(30.07.2020\)

## **Release Summary:**

* DIGIT 2.0 is a baselined release that has got very few functional changes, but more of a non-functional standardisation changes.
* Functional: Introducing advance payment feature and Advance collection integration with W/S.
* Non-functional: Upgrading spring boot and tracer version of all the backend services to enhance the range of non-functional benefits like performance, metrics, and security. Also all digit services/configs are baselined to follow the Semantic Versioning. These would enable the partner eco-system, system Integrators and state teams for an easy on-going upgrades and integrations.

## Upgrade Instructions:

* DIGIT 2.0 is a baselined release - considering simplification and standardization as a theme. It is strongly recommended all state teams upgrade to leverage benefits.
  * All services versioning will follow [**SemVer 2.0**](https://medium.com/@pmuens/understanding-semver-3f75d11b4d)**,** naming conventions and Git Tagging are improved for better tracing.
  * Next release we might have few more enhancements to the services naming conventions and handling MDMS and Configs better.
* **Impact**: Functionally, the upgrade to DIGIT 2.0 should not impact the existing environments.

## What has changed

{% tabs %}
{% tab title="Functional Changes" %}
### **New Features:**

* Ability to handle [advanced payments](https://digit-discuss.atlassian.net/wiki/spaces/ED/pages/604307457/Release+Notes+for+Advance+Payment+implementation+in+W+S) - platform and Reference implementation in W&S.
* Advance Collection integration with W&S
  * API Contracts

### **Enhancements:**

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
{% endtab %}

{% tab title="Non-functional Changes" %}
### **New Features:**

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
* DIGIT CI/CD [Pipelines-as-a-service](https://github.com/egovernments/CIOps)

### **Enhancements:**

* Versioned Git Tags for all the services
* Versioned MDMS and Config data.
{% endtab %}
{% endtabs %}

\*\*\*\*

