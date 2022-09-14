# FSM Workflow Configuration Changes

## **FSM Post Pay Create Business Service Request**

Instructions for production execution:

1. Replace the tenant id for the production environment
2. Replace the request info object with production user info details
3. Copy-paste the request in the \_create business service API to create the business service.

```
{
  "BusinessServices": [
        {
            "tenantId": "pb",
            "businessService": "FSM_POST_PAY_SERVICE",
            "business": "fsm",
            "businessServiceSla": 172800000,
            "states": [
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": null,
                    "applicationStatus": null,
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
							"currentState": null,
                            "action": "APPLY",
                            "nextState": "ASSIGN_DSO",
                            "roles": [
                                "FSM_CREATOR_EMP"
                            ]
                        },
                        {
                            "tenantId": "pb",
							"currentState": null,
                            "action": "CREATE",
                            "nextState": "CREATED",
                            "roles": [
                                "CITIZEN"
                            ]
                        }
                    ]
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "CREATED",
                    "applicationStatus": "CREATED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
							"currentState": "CREATED",
                            "action": "REJECT",
                            "nextState": "REJECTED",
                            "roles": [
                                "FSM_ADMIN"
                            ]
                        },
                        {
                            "tenantId": "pb",
							"currentState": "CREATED",
                            "action": "SUBMIT",
                            "nextState": "ASSIGN_DSO",
                            "roles": [
                                "FSM_EDITOR_EMP"
                            ]
                        }
                    ]
                },
                
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "ASSIGN_DSO",
                    "applicationStatus": "ASSIGN_DSO",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
							"currentState": "ASSIGN_DSO",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ]
                        },
                        {
                            "tenantId": "pb",
							"currentState": "ASSIGN_DSO",
                            "action": "ASSIGN",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_EDITOR_EMP"
                            ]
                        }
                    ]
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "PENDING_DSO_APPROVAL",
                    "applicationStatus": "PENDING_DSO_APPROVAL",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                       	{
                            "tenantId": "pb",
                            "currentState": "PENDING_DSO_APPROVAL",
                            "action": "DSO_ACCEPT",
                            "nextState": "DSO_INPROGRESS",
                            "roles": [
                                 "FSM_DSO",
                                 "FSM_EDITOR_EMP"
                            ]
                        },
						{
                            "tenantId": "pb",
                            "currentState": "PENDING_DSO_APPROVAL",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ]
                        },
						{
                            "tenantId": "pb",
                            "currentState": "PENDING_DSO_APPROVAL",
                            "action": "REASSING",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_EDITOR_EMP"
                            ]
                        },
						{
                            "tenantId": "pb",
                            "currentState": "PENDING_DSO_APPROVAL",
                            "action": "DSO_REJECT",
                            "nextState": "DSO_REJECTED",
                            "roles": [
                                 "FSM_DSO",
                                 "FSM_EDITOR_EMP"
                            ]
                        }
                    ]
                },
				 {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "DSO_REJECTED",
                    "applicationStatus": "DSO_REJECTED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_REJECTED",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ],
							"active": true
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_REJECTED",
                            "action": "REASSING",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_EDITOR_EMP"
                            ],
							 "active": true
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_REJECTED",
                            "action": "SENDBACK",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_ADMIN"
                            ],
							"active": true
                        }
                    ]
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "DSO_INPROGRESS",
                    "applicationStatus": "DSO_INPROGRESS",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_INPROGRESS",
                            "action": "SENDBACK",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_ADMIN"
                            ]
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_INPROGRESS",
                            "action": "DECLINE",
                            "nextState": "ASSIGN_DSO",
                            "roles": [
                                "FSM_DSO",
                                "FSM_EDITOR_EMP"
                            ]
                        },
                       
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_INPROGRESS",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ]
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "DSO_INPROGRESS",
                            "action": "REASSING",
                            "nextState": "PENDING_DSO_APPROVAL",
                            "roles": [
                                "FSM_EDITOR_EMP"
                            ]
                        },
						{
                            "tenantId": "pb",
                            "currentState": "DSO_INPROGRESS",
                            "action": "SCHEDULE",
                            "nextState": "PENDING_APPL_FEE_PAYMENT",
                            "roles": [
                                "FSM_EDITOR_EMP",
								"FSM_DSO"
							]
                        }
                    ]
                },
				{
                    "tenantId": "pb",
                    "sla": null,
                    "state": "PENDING_APPL_FEE_PAYMENT",
                    "applicationStatus": "PENDING_APPL_FEE_PAYMENT",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "currentState": "PENDING_APPL_FEE_PAYMENT",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "PENDING_APPL_FEE_PAYMENT",
                            "action": "SENDBACK",
                            "nextState": "DSO_INPROGRESS",
                            "roles": [
                                "FSM_ADMIN"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "PENDING_APPL_FEE_PAYMENT",
                            "action": "PAY",
                            "nextState": "DISPOSAL_IN_PROGRESS",
                            "roles": [
                                "CITIZEN",
                                "FSM_COLLECTOR"
                            ],
                            "active": true
                        }
                    ]
                },
				{
                    "tenantId": "pb",
                    "sla": null,
                    "state": "DISPOSAL_IN_PROGRESS",
                    "applicationStatus": "DISPOSAL_IN_PROGRESS",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "currentState": "DISPOSAL_IN_PROGRESS",
                            "action": "CANCEL",
                            "nextState": "CANCELED",
                            "roles": [
                                "FSM_ADMIN"
                            ],
                            "active": true
                        },
                        {
                            "tenantId": "pb",
                            "currentState": "DISPOSAL_IN_PROGRESS",
                            "action": "COMPLETED",
                            "nextState": "CITIZEN_FEEDBACK_PENDING",
                            "roles": [
                                "FSM_DSO",
                                "FSM_EDITOR_EMP"
                            ],
                            "active": true
                        }
                       
                    ]
                },
				{
                    "tenantId": "pb",
                    "sla": null,
                    "state": "CITIZEN_FEEDBACK_PENDING",
                    "applicationStatus": "CITIZEN_FEEDBACK_PENDING",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "currentState": "CITIZEN_FEEDBACK_PENDING",
                            "action": "RATE",
                            "nextState": "COMPLETED",
                            "roles": [
                                "CITIZEN"
                            ],
						    "active": true
                        }
                    ]
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "COMPLETED",
                    "applicationStatus": "COMPLETED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
					"actions": null
                },
                {
                    "tenantId": "pb",
					"sla": null,
                    "state": "REJECTED",
                    "applicationStatus": "REJECTED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "CANCELED",
                    "applicationStatus": "CANCELED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
                    "actions": null
                }
                
            ]
        }
    ],
	 "RequestInfo": {
    "apiId": "Rainmaker",
    "authToken": "e37d7087-6436-492f-ad5b-692a515cba58",
    "userInfo": {
      "id": 24226,
      "uuid": "11b0e02b-0145-4de2-bc42-c97b96264807",
      "userName": "amr001",
      "name": "leela",
      "mobileNumber": "9814424443",
      "emailId": "leela@llgmail.com",
      "locale": null,
      "type": "EMPLOYEE",
      "roles": [
        {
          "name": "NoC counter employee",
          "code": "NOC_CEMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Grievance Routing Officer",
          "code": "GRO",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "WS Document Verifier",
          "code": "WS_DOC_VERIFIER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "autoescalation emp",
          "code": "AUTO_ESCALATE",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "FSM Employee Report Viewer",
          "code": "FSM_REPORT_VIEWER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "PGR Last Mile Employee",
          "code": "PGR_LME",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "TL Field Inspector",
          "code": "TL_FIELD_INSPECTOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "BPA Field Inspector",
          "code": "BPA_FIELD_INSPECTOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "TL Approver",
          "code": "TL_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "BPA Services Approver",
          "code": "BPA_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Fire Noc Department Approver",
          "code": "FIRE_NOC_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Field Employee",
          "code": "FEMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Counter Employee",
          "code": "CEMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "WS Counter Employee",
          "code": "WS_CEMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "BPAREG Approver",
          "code": "BPAREG_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "WS Field Inspector",
          "code": "WS_FIELD_INSPECTOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Collection Operator",
          "code": "COLL_OPERATOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "TL doc verifier",
          "code": "TL_DOC_VERIFIER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "CSC Collection Operator",
          "code": "CSC_COLL_OPERATOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Employee",
          "code": "EMPLOYEE",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "TL Counter Employee",
          "code": "TL_CEMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "FSM Desluding Operator",
          "code": "FSM_DSO",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "TL Creator",
          "code": "TL_CREATOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "BPAREG doc verifier",
          "code": "BPAREG_DOC_VERIFIER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Customer Support Representative",
          "code": "CSR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "NoC counter Approver",
          "code": "NOC_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "HRMS Admin",
          "code": "HRMS_ADMIN",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Universal Collection Employee",
          "code": "UC_EMP",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "WS Approver",
          "code": "WS_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "BPA Services verifier",
          "code": "BPA_VERIFIER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "PT Counter Approver",
          "code": "PT_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "NoC Field Inpector",
          "code": "NOC_FIELD_INSPECTOR",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Grievance Officer",
          "code": "GO",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "Super User",
          "code": "SUPERUSER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "NOC Department Approver",
          "code": "NOC_DEPT_APPROVER",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "WS Clerk",
          "code": "WS_CLERK",
          "tenantId": "pb.amritsar"
        },
        {
          "name": "NoC Doc Verifier",
          "code": "NOC_DOC_VERIFIER",
          "tenantId": "pb.amritsar"
        }
      ],
      "active": true,
      "tenantId": "pb.amritsar",
      "permanentCity": null
    },
    "msgId": "1646071179143|en_IN"
  }
}


```

## **FSM Vehicle Trip Update Business Service Request**

Instructions for production execution:

1. Replace the tenant id for the production environment
2. Replace the request info object with production user info details
3. Fetch the production instance of the FSM\_VEHICLE\_TRIP business object and add the Vehicle Decline action and state in the Business service definition and then use the \_update business service for updating the workflow for vehicle trip.

```
{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "action": "",
        "did": 1,
        "key": "",
        "msgId": "20170310130900|en_IN",
        "requesterId": "",
        "ts": 1513579888683,
        "ver": ".01",
        "authToken": "9d7c1ba7-ecd2-49cb-8eb4-96de45698e4f"
    },

     "BusinessServices": [
        {
            "tenantId": "pb.amritsar",
            "uuid": "22c802e6-5354-43be-979a-8a653753459e",
            "businessService": "FSM_VEHICLE_TRIP",
            "business": "vehicle",
            "businessServiceSla": 172800000,
            "states": [
                {
                    "auditDetails": {
                        "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "createdTime": 1613116718088,
                        "lastModifiedTime": 1613116718088
                    },
                    "uuid": "61e01ccd-be34-4705-ae82-13ae93200fb3",
                    "tenantId": "pb.amritsar",
                    "businessServiceId": "22c802e6-5354-43be-979a-8a653753459e",
                    "sla": null,
                    "state": null,
                    "applicationStatus": null,
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": true,
                    "actions": [
                        {
                            "auditDetails": {
                                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "createdTime": 1613116718088,
                                "lastModifiedTime": 1613116718088
                            },
                            "uuid": "96e88b11-25d8-4cc1-b35c-6ce5edcb5904",
                            "tenantId": "pb.amritsar",
                            "currentState": "61e01ccd-be34-4705-ae82-13ae93200fb3",
                            "action": "SCHEDULE",
                            "nextState": "71f17154-40b8-4595-903a-c8d93c124abe",
                            "roles": [
                                "FSM_DSO"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "auditDetails": {
                        "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "createdTime": 1613116718088,
                        "lastModifiedTime": 1613116718088
                    },
                    "uuid": "71f17154-40b8-4595-903a-c8d93c124abe",
                    "tenantId": "pb.amritsar",
                    "businessServiceId": "22c802e6-5354-43be-979a-8a653753459e",
                    "sla": null,
                    "state": "SCHEDULED",
                    "applicationStatus": "SCHEDULED",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "auditDetails": {
                                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "createdTime": 1613116718088,
                                "lastModifiedTime": 1613116718088
                            },
                            "uuid": "b82e310e-a519-4ee8-8aaf-550cccbe26b2",
                            "tenantId": "pb.amritsar",
                            "currentState": "71f17154-40b8-4595-903a-c8d93c124abe",
                            "action": "READY_FOR_DISPOSAL",
                            "nextState": "e217e14a-7d3a-41bc-ae31-7ab2dce26f02",
                            "roles": [
                                "FSM_DSO",
                                "FSM_EDITOR_EMP"
                            ],
                            "active": true
                        }
                    ]
                },
                {
                    "auditDetails": {
                        "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "createdTime": 1613116718088,
                        "lastModifiedTime": 1613116718088
                    },
                    "uuid": "e217e14a-7d3a-41bc-ae31-7ab2dce26f02",
                    "tenantId": "pb.amritsar",
                    "businessServiceId": "22c802e6-5354-43be-979a-8a653753459e",
                    "sla": null,
                    "state": "WAITING_FOR_DISPOSAL",
                    "applicationStatus": "WAITING_FOR_DISPOSAL",
                    "docUploadRequired": false,
                    "isStartState": true,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "auditDetails": {
                                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                                "createdTime": 1613116718088,
                                "lastModifiedTime": 1613116718088
                            },
                            "uuid": "c83445e8-c658-4a29-b69d-29f30a8be7ff",
                            "tenantId": "pb.amritsar",
                            "currentState": "e217e14a-7d3a-41bc-ae31-7ab2dce26f02",
                            "action": "DISPOSE",
                            "nextState": "0fec53d3-6940-44c9-8582-2a09bd1f413a",
                            "roles": [
                                "FSM_EMP_FSTPO"
                            ],
                            "active": true
                        },
						{
							"action": "DECLINEVEHICLE",
							"currentState": "e217e14a-7d3a-41bc-ae31-7ab2dce26f02",
							"nextState": "VEHICLE_DECLINED",
							  "roles": [
								"FSM_EMP_FSTPO"
							  ],
							"active": true 
						}
                    ]
                },
                {
                    "auditDetails": {
                        "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                        "createdTime": 1613116718088,
                        "lastModifiedTime": 1613116718088
                    },
                    "uuid": "0fec53d3-6940-44c9-8582-2a09bd1f413a",
                    "tenantId": "pb.amritsar",
                    "businessServiceId": "22c802e6-5354-43be-979a-8a653753459e",
                    "sla": null,
                    "state": "DISPOSED",
                    "applicationStatus": "DISPOSED",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": true,
                    "actions": null
                },
				{
				  "tenantId": "pb.amritsar",
				  "businessServiceId": "22c802e6-5354-43be-979a-8a653753459e",
				  "sla": null,
				  "state": "VEHICLE_DECLINED",
				  "applicationStatus": "VEHICLE_DECLINED",
				  "docUploadRequired": false,
				  "isStartState": false,
				  "isTerminateState": true,
				  "isStateUpdatable": true
				  "actions": null
				}
            ],
            "auditDetails": {
                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "createdTime": 1613116718088,
                "lastModifiedTime": 1613116718088
            }
        }
    ]

}

```

