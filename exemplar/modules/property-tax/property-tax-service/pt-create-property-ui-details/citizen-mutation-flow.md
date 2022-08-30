# Citizen Mutation Flow

**Objective:** To provide citizens with the functionality to apply for Ownership Transfer for an active property.

The Transfer of Ownership Option is provided to citizens on the home screen in the citizen App, under property Tax card.

![](<../../../../../.gitbook/assets/image (196) (1).png>)

Upon clicking on “Transfer Property Ownership/Mutation” link, users are taken to property search page just like in case of “search & Pay” option, where he can search for the property he wants to search the property for.

![](<../../../../../.gitbook/assets/image (210).png>)

After searching the property the user is shown the property details for the properties based on the search criteria. With Total Dues on top of the card.

![](<../../../../../.gitbook/assets/image (245).png>)

If there are dues owed on the property (unpaid taxes), then users are shown a popup stating that the citizen has to clear his dues first. with a proceed to pay button that takes citizens to the common pay page, just like in the case of Search & Pay.

![](<../../../../../.gitbook/assets/image (167).png>)

In case of dues cleared the citizen is taken to the Docs required Page, just like in the case of Employee Mutation, where he is shown the list of docs he is supposed to have in order to be able to transfer the property.

![](<../../../../../.gitbook/assets/image (208).png>)

on this page after clicking on Transfer of Ownership, the citizen is made to go through the Ownership Transfer flow where he fills in the Ownership details and Mutation Details. After completing the flow citizen is shown with the success screen with his application number and the option to download his acknowledgement as a pdf.

![](<../../../../../.gitbook/assets/image (201).png>)

## **Technical Details**

Code link for citizen mutation: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/citizen/Mutate/index.js)

**MDMS data**

The MDMS data is the same as in the case of employee Mutation Screen.

**API used**

The citizen mutation calls the `property-services/property/_update` API to update the property status after that the application is gone through the Employee workflow to complete the transfer.

When Update API is called the documents are updated for the property according to the following snippet:-

```
        documents: [
          ...originalProperty.documents.map((oldDoc) => {
            if (mutationDocs?.PropertyTax?.MutationDocuments.some((mut) => oldDoc.documentType.includes(mut.code))) {
              return { ...oldDoc, status: "INACTIVE" };
            } else return oldDoc;
          }),
          ...newDocs,
        ],
```

Here `originalProperty` is the property data before mutation, and `mutationDocs` is the MDMS response for Mutation Docs.

## **Role Action Mapping**

|                                      |           |               |
| ------------------------------------ | --------- | ------------- |
| **Url**                              | **Roles** | **Action Id** |
| `property-services/property/_update` | `CITIZEN` | `1896`        |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
