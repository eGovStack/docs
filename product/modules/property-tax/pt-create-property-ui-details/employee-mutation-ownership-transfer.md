# Employee - Mutation (Ownership Transfer)

**Objective:** To Provide employees with functionality to transfer Ownership of an active property.

## **Documents Required for Mutate Property Page**

When a property is in Active status and has no dues to pay then Employee is given an option on the property details page to mutate a property.

![](<../../../../.gitbook/assets/image (211).png>)

The doc required page is shown if the property is paid for otherwise it is taken to the payment details page. It shows the employee the list of documents required in order to proceed with the form.

## **Mutate Property Form**

![](<../../../../.gitbook/assets/image (229).png>)

After clicking on the “Transfer of Ownership” button on the required page, the employee is redirected to the Transfer of Ownership or Mutation form. Here the Transferor details are displayed and Employee can fill the transferee details form.

## **Technical Documentation**

_The file for mutation can be found on:_

[![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/PropertyMutation/index.js)

**MDMS Data Used**

Similar to that in employee Property create along with Mutation Documents. Which can be found in:-

[![](https://github.com/fluidicon.png)egov-mdms-data/MutationDocuments.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/MutationDocuments.json)

**APIs Called:** `1property-services/property/_update`

\*\*When update API is called the documents are updated according to the snippet :-

```
 documents: [
          ...data.originalData?.documents.filter(
            (oldDoc) => !mutationDocs?.PropertyTax?.MutationDocuments.some((mut) => oldDoc.documentType.includes(mut.code))
          ),
          ...data.documents.documents.map((e) =>
            e.documentType.includes("OWNER.TRANSFERREASONDOCUMENT") ? { ...e, documentType: e.documentType.split(".")[2] } : e
          ),
        ],
```

Here `data.originalData` is the property before the update, while `data.documents` is the documents that were uploaded in the form, and `mutationDocs` is the MDMS response for Mutation Docs.

**Acknowledgement Screen**

If the Property Mutation is successful. then the employee is directed to this screen that shows the Acknowledgement Id and the option to download a pdf of the acknowledgement containing property details.

![](<../../../../.gitbook/assets/image (134).png>)

## **Role Actions**

|                                      |           |               |
| ------------------------------------ | --------- | ------------- |
| **Url**                              | **Roles** | **Action Id** |
| `property-services/property/_update` | `PT-CEMP` | `1896`        |
