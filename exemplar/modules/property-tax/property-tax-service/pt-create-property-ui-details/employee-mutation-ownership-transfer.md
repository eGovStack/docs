# Employee - Mutation (Ownership Transfer)

**Objective:** To Provide employees with functionality to transfer Ownership of an active property.

## **Documents Required for Mutate Property Page**

When a property is in active status and has no dues to pay, the employee has the option to mutate a property on the Property Details page.

![](<../../../../../.gitbook/assets/image (211).png>)

The doc required page is shown if the property is paid for otherwise the user is redirected to the payment details page. It shows the employee the list of documents required in order to proceed with the form.

## **Mutate Property Form**

![](<../../../../../.gitbook/assets/image (229).png>)

Clicking on the Transfer of Ownership button on the required page redirects the employee to the Transfer of Ownership or Mutation form. Here the Transferor details are displayed and the employee can fill out the transferee details form.

## **Technical Documentation**

Mutation file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/PropertyMutation/index.js)

**MDMS Data Used**

Similar to the MDMS used in employee Property Create flow and the Mutation Documents flow. Mutation documents MDMS data file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/MutationDocuments.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/MutationDocuments.json)

**APIs Called:** `1property-services/property/_update`

When update API is called the documents are updated in accordance to the snippet below:-

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

Here `data.originalData` is the property before the update. The `data.documents` is the documents that were uploaded in the form, and `mutationDocs` is the MDMS response for Mutation Docs.

**Acknowledgement Screen**

If the Property Mutation is successful. then the employee is directed to the acknowledgement screen. The screen displays the Acknowledgement Id and the option to download a pdf copy of the acknowledgement containing property details.

![](<../../../../../.gitbook/assets/image (134).png>)

## **Role Action Mapping**

|                                      |           |               |
| ------------------------------------ | --------- | ------------- |
| **Url**                              | **Roles** | **Action Id** |
| `property-services/property/_update` | `PT-CEMP` | `1896`        |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
