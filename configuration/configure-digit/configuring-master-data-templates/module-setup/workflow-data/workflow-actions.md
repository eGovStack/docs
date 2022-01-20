# Workflow Actions

### Introduction

Workflow action defined as an activity which is performed by a workflow user on a service request/ application during the workflow. All the workflow actions are predefined and performed a well-defined job once performed.

In its nature actions are not configurable, only the localization of actions is permissible as a configuration.

### Data Table

| S. No. | Action                 | Description                                                                                                                                                                                  | Module(s)                                            |
| ------ | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| 1      | Initiate               | The action will start the application for citizen and CEMP                                                                                                                                   | Trade Licenses, Property Tax, Building Plan Approval |
| 2      | Edit                   | Using this action the application can be opened in editable form and any changes can be performed                                                                                            | Trade Licenses, Property Tax, Building Plan Approval |
| 3      | Submit                 | This action will freeze the application from citizen or CEMP and proceed further for workflow                                                                                                | Trade Licenses, Property Tax, Building Plan Approval |
| 4      | Verify and Forward     | This action will proceed application to the next stage of the workflow process and also assigns tasks to the next user in the workflow (if needed)                                           | Trade Licenses, Property Tax, Building Plan Approval |
| 5      | Pay                    | This action will help to pay application fees                                                                                                                                                | Trade Licenses, Property Tax, Building Plan Approval |
| 6      | Approve                | This action will be the last stage of application workflow which will grant permission for a specific application                                                                            | Trade Licenses, Property Tax, Building Plan Approval |
| 7      | Activate connection    | This action will create a consumer no. against the application and demand generation can start                                                                                               | Water and Sewerage Charges                           |
| 8      | Reject                 | This action will reject the application, the application rejected can’t be processed further or with the help of it, citizens can not re-apply. He has to start a new application next time. | Trade Licenses, Property Tax, Building Plan Approval |
| 9      | Send Back              | An actor can assign back the application to the previous state if any edits/changes are required                                                                                             | Trade Licenses, Property Tax, Building Plan Approval |
| 10     | Send Back to Citizen   | An actor can assign back the application to the citizen if any edits/changes are required                                                                                                    | Trade Licenses, Property Tax, Building Plan Approval |
| 11     | View                   | Anyone in the workflow can view the application and task details                                                                                                                             | Trade Licenses, Property Tax, Building Plan Approval |
| 12     | Comment                | Comments can be recorded before any action is taken which can change the state of the application                                                                                            | Trade Licenses, Property Tax, Building Plan Approval |
| 13     | Download/ Print        | Download/Print of any artefacts can be configured as per the requirement for application processing                                                                                          | All Modules                                          |
| 14     | Forward                | This action will not create any bill but will be forwarded to the next level review and approve                                                                                              | Finance                                              |
| 15     | Create and Approve     | In this action, the user who initiates the action can create and approve the bill. (Here there should a threshold amount to be set up)                                                       | Finance                                              |
| 16     | Save                   | In this action, the approver can Save the bill before it is approved or rejected                                                                                                             | Finance                                              |
| 17     | Verify and Approve     | This action will help the approver to approve the bill if he/she feels all the information is updated correctly                                                                              | Finance                                              |
| 18     | Reject                 | This action will help the approver to reject the bill if he/she feels all the information is not correct and may need further clarification.                                                 | Finance                                              |
| 19     | Send back to Assistant | This action will help to send back the notification on the bill is rejected from the approver                                                                                                | Finance                                              |
| 20     | Cancel                 | This action will help the approver to cancel the bill if he/she feels that the bill need to be rejected                                                                                      | Finance                                              |

### Procedure

Actions are standard and are not configurable, hence the template, data definition and standard procedure to fill the template are not needed. This page is created to provide the information and helping the defined workflow process.

#### Data Definition

Not applicable

#### Steps to fill data

Not applicable

### Checklist

Not applicable

### Attachments

Not applicable

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
