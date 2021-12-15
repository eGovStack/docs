# Workflow Auto Escalation Release Notes

## Overview

This is an enhancement in the workflow service where applications can get auto escalated to a designated role on breach of an SLA

## Release Highlights

* Configure SLA at a workflow state level
* Escalate the application to a role if there is a breach in SLA
* Make the application status as deemed approved or reject on breach of an SLA
* Escalate the application to the next logical step in the workflow ladder if there is a breach in SLA

## Release Features

|                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Key Feature**                                                                                                        | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <ul><li>Configure SLA at a workflow state level</li></ul>                                                              | <p>In the earlier versions, the SLA can be configured only at the business service level. Now it has been enhanced in a way that either the SLA can be configured at a business service level for a business service or it can be configured at each workflow state in the business service.</p><p>If a business service has 3 workflow states A-B-C , now there can be an SLA definition for application movement from A to B and one a separate definition for movement from B-C</p> |
| <ul><li>Escalate the application to a role if there is a breach in SLA</li></ul>                                       | <p>Either if the SLA breach is at the business service level or at the workflow state level, the application can be configured to move the application from an existing state to a role.</p><p>For Example: If the config is in breach of SLA move the application to the Field inspector role, then the application will be moved automatically to the role field inspector when the SLA timeline is reached.</p>                                                                     |
| <ul><li>Make the application status as deemed approved or reject on breach of an SLA</li></ul>                         | <p>On breach of an SLA either at the business service level or at the workflow state level, it can be configured to make the application deemed approved or rejected.</p><p>Deemed reject will come in use cases where citizen fails to take any action</p><p>Deemed approval will come in use cases where employees fail to take action within the stipulated SLA</p>                                                                                                                 |
| <ul><li>Escalate the application to the next logical step in the workflow ladder if there is a breach in SLA</li></ul> | <p>On breach of SLA in a workflow state, it can be configured to move the application to the next logical stage in the workflow ladder.</p><p>For example: if the flow of the application is from A-B-C, now in step B if there is a breach in SLA, automatically the application will be moved to step C.</p>                                                                                                                                                                         |

## Known Issues

* One UX issue which will go out in the next patch release

## Upcoming Release Features

*

## Reference Doc Links <a href="#reference-doc-links" id="reference-doc-links"></a>

|               |                 |
| ------------- | --------------- |
| **Doc Links** | **Description** |
|               |                 |
|               |                 |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
