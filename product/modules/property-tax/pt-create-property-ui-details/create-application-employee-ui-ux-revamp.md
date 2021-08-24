# Create Application - Employee UI/UX Revamp

**Objective:** To provide the employees involved in PT workflow, the functionalities to create a property Application in create workflow.

## **Create Application**

A counter employee can use create an application form, to register a citizen’s property.

![](../../../../.gitbook/assets/image%20%28190%29.png)

## **Technical Implementation**

_The file for create Application form for PT can be found in:-_

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/NewApplication/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/NewApplication/index.js)

_for creating an application employee enters all the details of the form manually, and Documents are uploaded based on the MDMS configuration found in the file:_

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/Documents.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/Documents.json)

**MDMS Data**

1. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/Floor.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/Floor.json)
2. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OccupancyType.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OccupancyType.json)
3. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OwnerShipCategory.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OwnerShipCategory.json)
4. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OwnerType.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/OwnerType.json)
5. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/PropertyType.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/PropertyType.json)
6. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/UsageCategory.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/UsageCategory.json)
7. [https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/SubOwnerShipCategory.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/SubOwnerShipCategory.json)

_The MDMS data for documents is similar to that found in :_

{% file src="../../../../.gitbook/assets/pt-mdms-configuration.pdf" caption="Property Tax MDMS Configuration" %}



\*\*with the noted addition of `formDataPath, formArrayAttrPath`, in `filterCondition` and `dropdownFilter` .

`formDataPath` path is the form path in form of an array of keys that requires to be followed to a new UI form to check the entered value. similar to `jsonPath` and `parentJsonpath` in old UI, While the `formArrayAttrPath` replaces the `arrayAttribute`.

_The use of the MDMS data within the component can be found in :_

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pageComponents/SelectDocuments.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pageComponents/SelectDocuments.js)

After adding all the valid documents and form values in the form, the user is allowed to submit the form

_which calls the property create API:_`1property-services/property/_create`

**Acknowledgement Screen**

If the Property creation is successful. then the employee is directed to this screen that shows Acknowledgement Id and the option to download a hardcopy of the acknowledgement containing property details.

![](../../../../.gitbook/assets/image%20%28137%29.png)

## **Role Mapping**

| **Url** | **ROLE** | **Action ID** |
| :--- | :--- | :--- |
| `property-services/property/_create` | `PT-CEMP` | `1895` |





