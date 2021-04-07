# Configuring Workflows For An Entity

## Overview

Workflow is defined as a sequence of tasks that has to be performed on an application/Entity to process it. The _egov-workflow-v2_ is a workflow engine which helps in performing these operations seamlessly using a predefined configuration. We will discuss how to create this configuration for a new product in this document.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _egov-workflow-v2 service is up and running_
* Role-Action mapping are added for business Service API’s 

## Key Functionalities

* Create and modify workflow configuration according to the product requirements
* Configure State level as well BusinessService level SLA to efficiently track the progress of the application
* Control access to perform actions through configuration

| **Attribute Name** | **Description** |
| :--- | :--- |
| tenantId | The tenantId \(ULB code\) for which the workflow configuration is defined |
| businessService | The name of the workflow |
| business | The name of the module which uses this workflow configuration |
| businessServiceSla | The overall SLA to process the application \(_in milliseconds_\) |
| state | Name of the state |
| applicationStatus | Status of the application when in the given state |
| docUploadRequired | Boolean flag representing if document are required to enter the state |
| isStartState | Boolean flag representing if the state can be used as starting state in workflow |
| isTerminateState | Boolean flag representing if the state is the leaf node or end state in the workflow configuration. _\(No Actions can be taken on states with this flag as true\)_ |
| isStateUpdatable | Boolean flag representing whether data can be updated in the application when taking action on the state |
| currentState | The current state on which action can be performed |
| nextState | The resultant state after action is performed |
| roles | A list containing the roles which can perform the actions |
| auditDetails | Contains fields to audit edits on the data. _\(createdTime, createdBy,lastModifiedTIme,lastModifiedby\)_ |

## Deployment Details

1. Deploy the latest version of egov-workflow-v2 service
2. Add businessService persister yaml path in persister configuration
3. Add Role-Action mapping for BusinessService API’s
4. Overwrite the egov.wf.statelevel flag \( _true_ for state level and _false_ for tenant level\)

## Configuration Details

The Workflow configuration has 3 levels of hierarchy:  
a. BusinessService  
b. State  
c. Action  
The top-level object is BusinessService, it contains fields describing the workflow and list of States that are part of the workflow. The businessService can be defined at tenant level like pb.amritsar or at the state level like pb. All objects maintain an audit sub-object which keeps track of who is creating and updating and the time of it.

```text
{
        "tenantId": "pb.amritsar",
        "businessService": "PGR",
        "business": "pgr-services",
        "businessServiceSla": 432000000,
        "states": [...]
    }
```

Each State object is a valid status for the application. The State object contains the information of the state and what actions can be performed on it.

```text
{
        "sla": 36000000,
        "state": "PENDINGFORASSIGNMENT",
        "applicationStatus": "PENDINGFORASSIGNMENT",
        "docUploadRequired": false,
        "isStartState": false,
        "isTerminateState": false,
        "isStateUpdatable": false,
        "actions": [...]
    }
```

The action object is the last object in the hierarchy, it defines the name of the action and the roles that can perform the action.

```text
      {
          "action": "ASSIGN",
          "roles": [
              "GRO",
              "DGRO"
          ],
          "nextState": "PENDINGATLME",
      }
```

The workflow should always start from the null state as the service treats new applications as having null as the initial state. eg:

```text
{
                    "sla": null,
                    "state": null,
                    "applicationStatus": null,
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "action": "APPLY",
                            "nextState": "APPLIED",
                            "roles": [
                                "CITIZEN",
                                "CSR"
                            ]
                        }
                    ]
                }
```

In action object whatever nextState is defined, the application will be sent to that state. It can be to another forward state or even some backward state from where the application has already passed  
_\(generally, such actions are named SENDBACK\)_

SENDBACKTOCITIZEN is a special keyword for action name. This action sends back the application to the citizen’s inbox for him to take action. A new State should be created on which Citizen can take action and should be the nextState of this action. While calling this action from module _assignees_ should be enriched by the module with the uuids of the owners of the application

## Integration

For integration-related steps please refer to the document [**Setting Up Workflows**](setting-up-workflow.md).

## Reference Docs

### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| Workflow Service Documentation | [https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664174657/Workflow+Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664174657/Workflow+Service) |
| Setting Up Workflows | [ttps://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644546619/Setting+Up+Workflows](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644546619/Setting+Up+Workflows) |

### API List

|  | **Link** |
| :--- | :--- |
| _\_create_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| _\_update_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |
| _\_search_ | [https://www.getpostman.com/collections/8552e3de40c819e34190](https://www.getpostman.com/collections/8552e3de40c819e34190) |

_\(Note: All the API’s are in the same postman collection therefore same link is added in each row\)_

