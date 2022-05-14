# Auto Escalation UI Flow

## **Objective**

Before going to read this Auto Escalation, please refer to inbox technical documentation here.

{% file src="../../.gitbook/assets/employee-inbox (1).pdf" %}
Employee Inbox
{% endfile %}

Provide Employee to show escalated applications that are pending for action.

Route - [https://egov-micro-uat.egovernments.org/employee/inbox](https://egov-micro-uat.egovernments.org/employee/inbox)

![](<../../.gitbook/assets/image (133).png>)

## **Technical Implementation Details**

**Note:**

1. Here we inter-changed the tabs like **ASSIGNED TO ME** to **ALL** vice versa added **Escalated tab** in the 3rd position.
2. **Nearing Escalation and Escalated**: Here we changed the localisation message of **Escalated** to **SLA Breached.**

Please find the Escalated API using file path:[ ![](https://github.com/fluidicon.png)frontend/actions.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-ui-kit-dev/src/redux/app/actions.js). We are calling escalated API based on the condtions.

![](<../../.gitbook/assets/image (129).png>)

![](<../../.gitbook/assets/image (219).png>)

1. get all applications in `payload.ProcessInstances` using `egov-workflow-v2/egov-wf/process/_search`
2. get the escalated applications in `escalatedPayload.ProcessInstances` using `egov-workflow-v2/egov-wf/escalate/_search`
3. pushing escalated applications into all applications with `isEscalatedApplication` flag with true value, for finding the escalated application in all applications.
4. Then it will work same like inbox[ Employee Inbox](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/1004437517)

**Escalated Tab**

Escalated Tab which shows the Escalated applications.

From the process instance response, we get all the records from which we filter the records based on the following condition

```
if (get(item, "isEscalatedApplication", false)) {
      escalatedToMe.push([...dataRows])
  }
```

here `isEscalatedApplication` is the flag added initially for separating the escalated application to show in the escalated tab.

OnClick on History:

The functionality works as it is but the only change is showing the symbol to identifying from which state it is escalated.

Functionality file path:[ ![](https://github.com/fluidicon.png)frontend/index.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/packages/employee/src/modules/employee/Inbox/components/Table/index.js)

![](<../../.gitbook/assets/image (227).png>)

Note: Inbox functionality will work the same as before as outlined in the Employee Inbox document attached here.

{% file src="../../.gitbook/assets/employee-inbox (1).pdf" %}
Employee Inbox
{% endfile %}

**Role Action Mapping**

|                          |                                              |            |               |
| ------------------------ | -------------------------------------------- | ---------- | ------------- |
| [**S.NO**](http://s.no/) | **API**                                      | **ROLES**  | **ACTION ID** |
| 1                        | `/egov-workflow-v2/egov-wf/escalate/_search` | `EMPLOYEE` | `2150`        |
