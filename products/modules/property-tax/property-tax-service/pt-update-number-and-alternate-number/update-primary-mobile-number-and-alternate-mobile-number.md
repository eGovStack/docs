# Update Primary Mobile Number & Alternate Mobile Number

## **Overview**&#x20;

The update feature in property services provides a facility to update the owner’s primary mobile number (referred to as ‘mobile number’ hereafter). The already existing update API is used with some enhancements to implement this feature. Also, a facility has been provided to add an alternate mobile number for every owner of the property. This can be done using the newly created addAlternateNumber API. The alternate number can also be updated using this API.

## **Pre-requisites**

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of Git
* Prior knowledge of the demand-based systems.
* Following services should be up and running:
  * user MDMS
  * Persister
  * Location
  * Localization
  * Id-Gen
  * Billing-service
  * URL-shortener

## **Key Functionality**

Enables user to update property owner’s mobile number and to add/update the alternate mobile number.

## **Configuration Details**  <a href="#configuration-details" id="configuration-details"></a>

### **Workflow config**

All the property information (except the owner’s mobile number/ alternate number) should be the same as the information from the search result. The owner’s primary mobile number has to be necessarily different from the existing one.

The Creation Reason in the property should be sent as **UPDATE** for the request to be considered as an update request. Also, the property has to be in **ACTIVE** status.\
\
For adding/updating alternate numbers, modify the **alternateMobileNumber** field in the Property.

Sample request for updating primary mobile number or adding/updating alternate number.

```
{
  "RequestInfo": {
        "apiId": "Rainmaker",
        "authToken": "08876469-a3e7-41c7-8031-218405fee62e",
        "access_token":"dee3f319-5593-4cf9-b74b-4771860445f9",
        "userInfo": {
            "id": 12085,
            "uuid": "abfe724b-a93e-4edd-b084-82ecbe22a192",
            "userName": "qaroo",
            "name": "QARoo",
            "mobileNumber": "6939358368",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                
                {
                    "name": "PT Counter Employee",
                    "code": "PT_CEMP",
                    "tenantId": "pb.amritsar"
                },
                
                {
                    "name": "PT Field Inspector",
                    "code": "PT_FIELD_INSPECTOR",
                    "tenantId": "pb.amritsar"
                },
                
                {
                    "name": "PT Doc Verifier",
                    "code": "PT_DOC_VERIFIER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Employee",
                    "code": "EMPLOYEE",
                    "tenantId": "pb.amritsar"
                },
                
                {
                    "name": "PT Counter Approver",
                    "code": "PT_APPROVER",
                    "tenantId": "pb.amritsar"
                },
                {
                    "name": "Super User",
                    "code": "SUPERUSER",
                    "tenantId": "pb.amritsar"
                }
                
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        }
    },
  "Property":  {
            "id": "b9e8fecd-5527-4283-b0fd-9019da696c25",
            "propertyId": "PB-PT-2021-09-01-020993",
            "surveyId": null,
            "linkedProperties": null,
            "tenantId": "pb.amritsar",
            "accountId": "11b0e02b-0145-4de2-bc42-c97b96264807",
            "oldPropertyId": null,
            "status": "ACTIVE",
            "address": {
                "tenantId": "pb.amritsar",
                "doorNo": null,
                "plotNo": null,
                "id": "8c567955-a6d6-4e97-8ba2-9e0675229893",
                "landmark": null,
                "city": "Amritsar",
                "district": null,
                "region": null,
                "state": null,
                "country": null,
                "pincode": null,
                "buildingName": null,
                "street": null,
                "locality": {
                    "code": "SUN04",
                    "name": "Ajit Nagar - Area1",
                    "label": "Locality",
                    "latitude": "31.63089",
                    "longitude": "74.871552",
                    "area": "Area1",
                    "children": [],
                    "materializedPath": null
                },
                "geoLocation": {
                    "latitude": 0.0,
                    "longitude": 0.0
                },
                "additionalDetails": null
            },
            "acknowldgementNumber": "PB-AC-2021-09-01-020523",
            "propertyType": "BUILTUP.INDEPENDENTPROPERTY",
            "ownershipCategory": "INDIVIDUAL.SINGLEOWNER",
            "owners": [
                {
                    "id": null,
                    "uuid": "188fe338-5116-4ba7-96f5-d8b3c86466d0",
                    "userName": "3dc9ed9b-a72f-41c8-a30e-618964ccd2dd",
                    "password": null,
                    "salutation": null,
                    "name": "Rohit",
                    "gender": null,
                    "mobileNumber": "7391904467",
                    "emailId": null,
                    "altContactNumber": null,
                    "pan": null,
                    "aadhaarNumber": null,
                    "permanentAddress": null,
                    "permanentCity": null,
                    "permanentPinCode": null,
                    "correspondenceCity": null,
                    "correspondencePinCode": null,
                    "correspondenceAddress": null,
                    "active": true,
                    "dob": null,
                    "pwdExpiryDate": 1626617402000,
                    "locale": null,
                    "type": "CITIZEN",
                    "signature": null,
                    "accountLocked": false,
                    "roles": [
                        {
                            "id": null,
                            "name": "Citizen",
                            "code": "CITIZEN",
                            "tenantId": "pb"
                        }
                    ],
                    "fatherOrHusbandName": null,
                    "bloodGroup": null,
                    "identificationMark": null,
                    "photo": null,
                    "createdBy": "24226",
                    "createdDate": 1630534079000,
                    "lastModifiedBy": "1",
                    "lastModifiedDate": 1634086148000,
                    "tenantId": "pb",
                    "alternatemobilenumber": "9619367055",
                    "ownerInfoUuid": "f375b888-e400-4007-8e0a-5338a6aa2794",
                    "isPrimaryOwner": null,
                    "ownerShipPercentage": null,
                    "ownerType": "NONE",
                    "institutionId": null,
                    "status": "ACTIVE",
                    "documents": null,
                    "relationship": "FATHER"
                }
            ],
            "alternateMobileNumberDetails": null,
            "institution": null,
            "creationReason": "UPDATE",
            "usageCategory": "NONRESIDENTIAL.COMMERCIAL",
            "noOfFloors": 1,
            "landArea": 1234.0,
            "superBuiltUpArea": null,
            "source": "MUNICIPAL_RECORDS",
            "channel": "CFC_COUNTER",
            "documents": null,
            "units": [
                {
                    "id": "c82b31b4-5761-41c2-b472-782f34670520",
                    "tenantId": null,
                    "floorNo": 0,
                    "unitType": "ACRESTAURANT",
                    "usageCategory": "NONRESIDENTIAL.COMMERCIAL.FOODJOINTS.ACRESTAURANT",
                    "occupancyType": "SELFOCCUPIED",
                    "active": true,
                    "occupancyDate": 0,
                    "constructionDetail": {
                        "carpetArea": null,
                        "builtUpArea": 136.67,
                        "plinthArea": null,
                        "superBuiltUpArea": null,
                        "constructionType": null,
                        "constructionDate": null,
                        "dimensions": null
                    },
                    "additionalDetails": null,
                    "auditDetails": null,
                    "arv": null
                }
            ],
            "additionalDetails": null,
            "auditDetails": {
                "createdBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "lastModifiedBy": "11b0e02b-0145-4de2-bc42-c97b96264807",
                "createdTime": 1630514279281,
                "lastModifiedTime": 1630514279281
            },
            "workflow": null,
            "AlternateUpdated": false
        }
}
```

Configs:

| **name**           | **value**                | **description** |
| ------------------ | ------------------------ | --------------- |
| kafka update topic | update-property-registry |                 |

### **Notification Configs**

```
        {
            "code": "PT_UPDATE_ALTERNATE_NUMBER",
            "message": "Dear {ownername}, Your request to register an alternate mobile number in property record has been processed and the mobile number {alternatenumber} has been registered as alternate mobile no.",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_UPDATE_OWNER_NUMBER",
            "message": "Dear {ownername}, Your request to update of mobile number in property record has been processed and the mobile number has been changed from {oldmobilenumber} to {newmobilenumber}.",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        }
```

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The update service belongs to the property service itself and provides the same ease of access for the functionality.

#### Steps to Integration (updating primary number): <a href="#steps-to-integration-updating-primary-number" id="steps-to-integration-updating-primary-number"></a>

* Pick a property id that is already created in the system.
* call the property/update API by changing the owner’s mobile number.

**Steps to Integration (updating alternate number):**

* Pick a property id that is already created in the system.
* call the property/addAlternateNumber API by adding/changing the owner’s alternate number.

**Reference Docs: -** For additional details **** please refer to the property document [Property Services | Doc-Links](../#reference-docs)



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
