---
description: 'New release features, enhancements, and fixes'
---

# Release Notes DIGIT 2.0

### Release Summary

‌DIGIT 2.0 is a baselined release that has got few functional changes, but more of non-functional standardisation changes.

* Functional: Introducing advance payment feature and Advance collection integration with W/S.
* Non-functional: Upgrading spring boot and tracer version of all the backend services to enhance the range of non-functional benefits like performance, metrics, and security. Also, all digit services/configs are baselined to follow the Semantic Versioning. These would enable the partner eco-system, system Integrators and state teams for easy on-going upgrades and integrations.

### New ‌Feature Additions

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Advance Payments</td>
      <td style="text-align:left">
        <p>Ability to handle <a href="advance-payments-release-notes.md">advanced payments </a>-
          platform and Reference implementation in W&amp;S.</p>
        <p>Advance Collection integration with W&amp;S</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">API Contracts</td>
      <td style="text-align:left">Advance Collection integration with W&amp;S</td>
    </tr>
    <tr>
      <td style="text-align:left">Infra/Ops Simplification &amp; Enablement</td>
      <td style="text-align:left">
        <p>Infra &amp; Service monitoring v1.0.0 (Prometheus, Alertmanager &amp;
          Grafana)</p>
        <ul>
          <li>Cluster Resource monitoring</li>
          <li>Request Traffic monitoring</li>
          <li>DIGIT Service monitoring</li>
          <li>All Java-based services SpringBoot upgraded from 1.5.X to 2.2.6 for better
            security, performance and metrics.</li>
          <li>Backbone Services migrated to Helm templates to ease deployment on Kubernetes.</li>
          <li>Introduced Minio as a digit platform service for SDCs to leverage S3 like
            object storage feature.</li>
          <li>DIGIT on Spot Instances for AWS users saves 60% of the cloud cost.</li>
          <li>Configurable SSO with GitHub or Google SSO OAuth for all the Infra apps
            like Jaeger, Grafana, Kibana.</li>
          <li><a href="https://github.com/egovernments/CIOps">Jenkins CI/CD as a servic</a>e
            with the pipelines</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Baseline version upgrades</td>
      <td style="text-align:left">
        <ul>
          <li>Bulk persister changes to support bulk persisting for migration in Persister
            Service.</li>
          <li>Localization URL params to be changed to request params in Localization
            service</li>
          <li>Receipt download link in SMS and email notifications.</li>
          <li>Rainwater Harvesting attribute in Property Service</li>
          <li>Filestore service enhancement - Support for SDC and S3 implementation.</li>
          <li>Maven dependencies upgrade and merging the backend services to the master
            branch (Upgraded Tracer to 2.0.0, spring boot to 2.2.6, flyway-core to
            6.4.3, etc along with code cleanup) for all the services across the services.
            The Changelog has been added.</li>
          <li>Baseline versioning of all the services as per the streaming strategy.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Generalized Client-side PDF generation component and integration with
            Property, Fire NOC, Trade License, and W&amp;S applications).</li>
          <li>Generalize acknowledgement screens component</li>
          <li>MDMS namespace common component and integration with PT and TL modules.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-functional enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Versioned Git Tags for all the services</li>
          <li>Versioned MDMS and Config data.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

**Upgrade Notes**

DIGIT 2.0 is a baselined release - considering simplification and standardization as a theme. It is strongly recommended all-state teams upgrade to leverage benefits.

* All services versioning will follow [**SemVer 2.0**](https://medium.com/@pmuens/understanding-semver-3f75d11b4d)**,** naming conventions and Git Tagging are improved for better tracing.
* Next release might have a few more enhancements to the services naming conventions and handling MDMS and Configs better.
* **Impact**: Functionally, the upgrade to DIGIT 2.0 will not impact the existing environments.

### Document Resources and Links

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>UI Technical Documents</b>
      </th>
      <th style="text-align:left"><b>Backend Service Documents</b>
      </th>
      <th style="text-align:left"><b>Infra/Deployment Documents</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li><a href="../user-guides/guide-pgr/">PGR</a>
          </li>
          <li><a href="../user-guides/guide-pt/">Property Tax</a>
          </li>
          <li><a href="../user-guides/guide-tl/">Trade License</a>
          </li>
          <li>Fire NOC</li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/436502610/BillGenie?atlOrigin=eyJpIjoiN2EzZmY2ZjFlYzIxNDc2Zjk4YzIwM2FmOGI1NmM1MDAiLCJwIjoiYyJ9">Bill Genie</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/438894719/Universal+Collection?atlOrigin=eyJpIjoiNjAzNzBiMTAwMzNlNDk2NDk0ZTQxNjdlMzMwYzE5N2IiLCJwIjoiYyJ9">MCS</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/NjoYpKzK">Common Pay</a>
          </li>
          <li><a href="advance-payments-release-notes.md">Advance Payment</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/QX3zRcjW">mSeva 2.0</a>
          </li>
          <li>Water &amp; Sewerage</li>
          <li>MDMS UI Configurations</li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/449085476/Required+documents+dialog+implementation?atlOrigin=eyJpIjoiNDEwZDdkNWYzY2EwNDRkZWE0Nzg2NTcwOTM5NDg1YzMiLCJwIjoiYyJ9">Required documents dialogue implementation</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/dVxJH2B5">Generation of Acknowledgement PDF</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/450789466/How+to+add+dynamic+drop+down+for+mdms+data?atlOrigin=eyJpIjoiNDY0ZGQxY2RhNTBkNDExOWE4ZTc1MTUxOTk4MTZmOTAiLCJwIjoiYyJ9">How to add dynamic dropdown for MDMS data</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/572522501/Acknowledgment+screens?atlOrigin=eyJpIjoiNWI5YzdmZDkyNThmNGI4MGFlMjI2MDg0NzRkMWQ4ZTgiLCJwIjoiYyJ9">Common Acknowledgment screens</a>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li><a href="https://digit-discuss.atlassian.net/l/c/1P512Vzx">Advance Payment</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/41XVUCh6">Kafka Connect for reindex</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/cRAR1xcf">TL Service Renewal Upgradation</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/37060620/File-Store-Service?atlOrigin=eyJpIjoiOWQwYWZmYjNkNTU0NDFlMzk4YjdiNTk1YTI3ZDY3NTciLCJwIjoiYyJ9">Filestore service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/hydmp2YA">Persister Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/152567827/Collection+Migration+V1+to+V2?atlOrigin=eyJpIjoiNjEwNjQ1MWE5ZDNmNGU5Nzk0MWI5YWJlNjU0N2E1YWQiLCJwIjoiYyJ9">Collection Migration v1 to v2</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/155910170/Consumer+Code+Uniqueness+Migration?atlOrigin=eyJpIjoiMTc5Y2Q1OWQ0NDBmNDA2MmJhNjRjZGY5NjY3ZTJjYWQiLCJwIjoiYyJ9">Consumer Code Uniqueness Migration</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/dgM6oHg1">Property Registry Migration</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/0y774J0V">Notification SMS service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328925216/Water+Service+-+Technical+Document?atlOrigin=eyJpIjoiNDM4Yjc3MmJmNDBiNDViZGEwZjJmYTg2MzVhNDdkOTgiLCJwIjoiYyJ9">Water Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/PM2Ho3A1">Sewerage Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/p3MGjvPw">Water Calculator Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/o0gRiR1n">Sewerage Calculator Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/l/c/Z2yYBY2b">W&amp;S Promotion document</a>
          </li>
        </ul>
      </td>
      <td style="text-align:left">
        <ul>
          <li><a href="https://github.com/egovernments/eGov-infraOps/commit/274aab0e90a10673972ddc769f2fc89015f0fe8d">Monitoring &amp; Alerting</a>
          </li>
          <li><a href="https://github.com/egovernments/eGov-infraOps/commit/4aae58e8560c726a44c9347795fd9db80aaed6c8">SSO OAuth (GitHub)</a> for
            Kibana, Jaeger, etc</li>
          <li><a href="https://github.com/egovernments/eGov-infraOps/commit/c7a4c3d5eb8b188e5083f3e0f33a9405bb995895">Grafana</a> dashboard
            for Infra and Service monitoring</li>
          <li><a href="https://github.com/egovernments/eGov-infraOps/commit/274aab0e90a10673972ddc769f2fc89015f0fe8d">Jenkins as a service</a> for
            CI/CD</li>
          <li>Minio <a href="https://github.com/egovernments/eGov-infraOps/pull/764/files">Helm templates</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Upcoming Release Highlights

* Renaming of the backend services with a naming convention in place.
* Config \(MDMS, Configs\) Baseline versioning.
* Readme.md and Localsetup.md documentations for Core, Business, Municipal, and Other services.

