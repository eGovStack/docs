---
description: eGov Support Strategy for DIGIT
---

# Partner Support

## Objectives

eGov will enable partners to implement the DIGIT platform and products across ULBs for a State. As part of the enablement process, eGov will assist the partner by providing them product training, implementation training and training them on technical support for supporting the system. The partner is expected to provide the primary support of the overall system and will aim to resolve issues through workarounds and data fixes, as applicable. The partner will reach out to eGov if an issue is attributable to the DIGIT platform or Products.

The key objectives for DIGIT support are:

1. Clearly communicate the DIGIT product and platform release strategy, versioning strategy and support commitment to States and Partners.
2. Assist the clients/partners in resolving incidents that are attributable to DIGIT.
3. Provide the partners with suitable training kits to support DIGIT. Share FAQs and knowledge assets that help the partner support teams.
4. Provide periodic communication on upcoming DIGIT releases as well as release notes when a DIGIT release rolls out.

## Scope of Support

**Version Support**

eGov will support versions ‘n’ and ‘n-1’ of the DIGIT services, where ‘n’ refers to the major version number. Each service follows a major.minor.patch version number \(based on Semantic Versioning standards - [https://semver.org/](https://semver.org/)\). A change in major version number for service indicates a break in backward compatibility. Such major or minor changes are always accompanied by migration scripts to carry data over an upgrade. Support is void if the partner makes changes to the source code of the DIGIT services.

Here’s an illustration for supporting ‘n’ and ‘n-1’ versions:

* Version 2.5.56 is running in a State-supported by a Partner. If they find a bug, we are required to supply a patch for 2.5.56 though the latest version is 3.2.15. Of course, the bug fix needs to be propagated to 3.2.15 as well for other environments.
* Needless to say, if a bug was found in version 3.2.15, it would be fixed. Again, given ‘n-1’ support, we would need to backpropagate the fix to version 2.5.56.

Services are combined to create the DIGIT release package. The release package includes the DIGIT platform, Municipal services and groups for each of the DIGIT products such as PT, TL, PGR, WS, OBPS etc. Inter-dependencies between different services are documented through a service mapping matrix. Changes to these DIGIT services are delivered to the partners as releases.

**Communication**

1. eGov will send release notes \(release may include platform, municipal and product updates\) for each release along with data migration scripts, as applicable. Release Notes specify which services are changing and the details around the changes.
2. eGov will share the DIGIT roadmap with partners every quarter. The roadmap provides enough detail that allows the partners to plan for changes at their end.
3. EOSL \(End of Service Life\) considerations for each version. eGov will flag EOSL for each version well in advance. This will also act as triggers for upgrades.

## Support Process

Partner is responsible for providing primary support for the DIGIT hosting for the client. When a support incident occurs, the partner support team is required to carry out the first level of diagnosis and investigate to identify where the issue lies. If this issue is found to be attributable to DIGIT services, then the incident may be raised with the eGov team. In parallel, the partner support team should aim to provide a suitable workaround to address the issue for the client.

* eGov will provide an email ID for partners to log an incident. An escalation matrix will be provided to allow partners to escalate high severity issues.
* The partner provides details of investigations carried out by their teams along with logs and inferences leading them to believe that the issue lies with the eGov supported version of DIGIT.
* eGov support team acknowledges the issue and provides a reference number to allow the partner to track the issue. The Support Team will check versions to ensure that the services running are supported \(‘n’ and ‘n-1’ versions\). 
  * If not, the solution would be to upgrade to a later version.
  * If this is found to be a genuine bug, eGov will plan to fix in a newer release and partner will get the fix once they upgrade.
* eGov support team will investigate and aim to reproduce the issue. Partner support teams may need to provide additional logs and access to the environment to allow the eGov team to carry out further investigations.
* eGov support team provides a resolution to the issue:
  * Clarification, or workaround to resolve the issue
  * Plan for a patch release, if the issue is found to be in the code of the DIGIT platform
* Provide patch release to the partner to close out the issue.

**Hours of support:** 9 am to 6 pm IST Mon to Fri

| Severity | Description | Response SLA |
| :--- | :--- | :--- |
| P1, Business Halted | Critical application outage impacting service for which the cause is unknown. No bypass or workaround available. | 4 hours |
| P2, Business Slowed | A key component of the application is degraded, unusable or unavailable, some users affected. | 1 day |
| P3 and lower, Business Unaffected | A component of the application is degraded, which causes a minor inconvenience, but a workaround is available. | 2 days |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

