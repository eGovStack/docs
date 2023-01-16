# Auto Escalation UI Flow

## **Objective**

Refer to the employee inbox technical documentation below before reading the auto-escalation flow details.

{% file src="../../../.gitbook/assets/employee-inbox (1).pdf" %}
Employee Inbox
{% endfile %}

The auto-escalation option provides employees with the option to view all escalated applications that have not been acted on.

Route - [https://egov-micro-uat.egovernments.org/employee/inbox](https://egov-micro-uat.egovernments.org/employee/inbox)

![](<../../../.gitbook/assets/image (133).png>)

## **Technical Implementation Details**

{% hint style="info" %}
**Note**

1. The tab **ASSIGNED TO ME** is inter-changed to **ALL** vice versa and the **Escalated** tab **** is added in the 3rd position.
2. **Nearing Escalation and Escalated**: The localisation message of **Escalated** is changed to **SLA Breached.**
{% endhint %}

Escalated API file path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/actions.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-ui-kit-dev/src/redux/app/actions.js). The escalated API is called based on given conditions.

![](<../../../.gitbook/assets/image (129).png>)

![](<../../../.gitbook/assets/image (219) (1).png>)

1. get all applications in `payload.ProcessInstances` using `egov-workflow-v2/egov-wf/process/_search`
2. get the escalated applications in `escalatedPayload.ProcessInstances` using `egov-workflow-v2/egov-wf/escalate/_search`
3. pushing escalated applications into all applications with `isEscalatedApplication` flag with true value, for finding the escalated application in all applications.
4. This works the same as [Employee Inbox](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/1004437517).

### **Escalated Tab**

The Escalated tab shows all Escalated applications.

The process instance response fetches all records from which the records are filtered based on the following condition:

```
if (get(item, "isEscalatedApplication", false)) {
      escalatedToMe.push([...dataRows])
  }
```

The `isEscalatedApplication` is the flag added initially for separating the escalated applications to show in the escalated tab.

### On-Click History

The functionality works as it is but the only change is showing the symbol to identify the state from which it has escalated.

Functionality file path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/index.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/packages/employee/src/modules/employee/Inbox/components/Table/index.js)

![](<../../../.gitbook/assets/image (227).png>)

{% hint style="info" %}
**Note:** Inbox functionality works the same as before as outlined in the Employee Inbox document attached here.
{% endhint %}

{% file src="../../../.gitbook/assets/employee-inbox (1).pdf" %}
Employee Inbox
{% endfile %}

## **Role Action Mapping**

| API                                          | Roles      | Action ID |
| -------------------------------------------- | ---------- | --------- |
| `/egov-workflow-v2/egov-wf/escalate/_search` | `EMPLOYEE` | `2150`    |
