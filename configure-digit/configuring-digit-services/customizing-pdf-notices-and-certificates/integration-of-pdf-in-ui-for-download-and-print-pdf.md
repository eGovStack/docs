# Integration Of PDF In UI For Download And Print PDF

## Overview <a id="Overview"></a>

The objective of PDF generation service is to bulk generate pdf as per requirement.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* All required data and format file path is added in the environment yml file
* pdf-service is up and running

## Key Functionalities <a id="Key-Functionalities"></a>

* Provide functionality to download and print PDF’s
* Provide functionality to download and print bulk PDF’s

## Deployment Details <a id="Deployment-Details"></a>

1. Create data config and format config for a PDF according to product requirement.
2. Add data config and format config files in PDF configuration
3. Add the file path of data and format config in the environment yml file
4. Deploy the latest version of pdf-service in a particular environment.

## Configuration Details <a id="Configuration-Details"></a>

For Configuration details please refer to the **Customizing PDF Receipts & Certificates** document in Reference Docs

## Integration <a id="Integration"></a>

### Integration Scope <a id="Integration-Scope"></a>

The PDF configuration can be used by any module which needs to show particular information in PDF format that can be printed/downloaded by the user.

### Integration Benefits <a id="Integration-Benefits"></a>

* Functionality to generate PDFs in bulk
* Avoid regeneration
* Support QR codes and Images
* Functionality to specify a maximum number of records to be written in one PDF
* Uploading generated PDF to filestore and return filestore id for easy access

### Steps to Integration <a id="Steps-to-Integration"></a>

The following are the steps for integrating TL certificate in UI.

In footer.js file which is present in /frontend/web/rainmaker/dev-packages/egov-tradelicence-dev/src/ui-config/screens/specs/tradelicence/applyResource , Create two object \(download and print object\) in footerReview function.

Example

```text
let tlCertificateDownloadObject = {
    label: { labelName: "TL Certificate", labelKey: "TL_CERTIFICATE" },
    link: () => {
      const { Licenses } = state.screenConfiguration.preparedFinalObject;
      downloadCertificateForm(Licenses);
    },
    leftIcon: "book"
  };
  let tlCertificatePrintObject = {
    label: { labelName: "TL Certificate", labelKey: "TL_CERTIFICATE" },
    link: () => {
      generateReceipt(state, dispatch, "certificate_print");
    },
    leftIcon: "book"
  };
```

In tlCertificateDownloadObject give the proper label name and key for the pdf. In the link function get the object whose mapping is required for PDF, in this case, we want a license object. Call the function downloadCertificateForm \(details about this function is described in the next step\). Add icon details which we want to use in UI to represent that option. The same thing for tlcertificatePrintObject only difference is we have to call generateReceipt function. Again create the same two object with similar content in downloadPrintContainer function.

Mention the function name “downloadCertificateForm“ and “generateReceipt“ in import , because the functions is define in /frontend/web/rainmaker/dev-packages/egov-tradelicence-dev/src/ui-config/screens/specs/utils/index.js and /frontend/web/rainmaker/dev-packages/egov-tradelicence-dev/src/ui-config/screens/specs/utils/receiptPDF.js

In index.js define the function which is responsible for calling the Create API of PDF service to create respective PDF. In that function, you have to mention the tenant ID and proper key value which is the same as the key mentioned in the data and format config. Also mentioned the URL : /pdf-service/v1/\_create and action as get and also call the function downloadReceiptFromFilestoreID which is responsible to call filestore service with filestoreid and return the URL for pdf.

**Example of function downloadCertificateForm**

```text
export const downloadCertificateForm = (Licenses) => {
  const queryStr = [
    { key: "key", value: "tlcertificate" },
    { key: "tenantId", value: "pb" }
  ]
  const DOWNLOADRECEIPT = {
    GET: {
      URL: "/pdf-service/v1/_create",
      ACTION: "_get",
    },
  };
  try {
    httpRequest("post", DOWNLOADRECEIPT.GET.URL, DOWNLOADRECEIPT.GET.ACTION, queryStr, { Licenses }, { 'Accept': 'application/json' }, { responseType: 'arraybuffer' })
      .then(res => {
        res.filestoreIds[0]
        if (res && res.filestoreIds && res.filestoreIds.length > 0) {
          res.filestoreIds.map(fileStoreId => {
            downloadReceiptFromFilestoreID(fileStoreId)
          })
        } else {
          console.log("Error In Acknowledgement form Download");
        }
      });
  } catch (exception) {
    alert('Some Error Occured while downloading Acknowledgement form!');
  }
}
```

E**xample of function generateReceipt**

```text
const generateReceipt = async (state, dispatch, type) => {
//  console.log("Transformed Data--",transformedData);
  pdfMakeCustom.vfs = pdfFonts.vfs;
  pdfMakeCustom.fonts = {
    Camby:{
            normal: 'Cambay-Regular.ttf',
            bold: 'Cambay-Regular.ttf',
            italics: 'Cambay-Regular.ttf',
            bolditalics: 'Cambay-Regular.ttf'
    },

  };
  let data1 = _.get(
    state.screenConfiguration.preparedFinalObject,
    "applicationDataForReceipt",
    {}
  );
  let data2 = _.get(
    state.screenConfiguration.preparedFinalObject,
    "receiptDataForReceipt",
    {}
  );
  let data3 = _.get(
    state.screenConfiguration.preparedFinalObject,
    "mdmsDataForReceipt",
    {}
  );
  let data4 = _.get(
    state.screenConfiguration.preparedFinalObject,
    "userDataForReceipt",
    {}
  );
  let data5 = _.get(
    state.screenConfiguration.preparedFinalObject.Licenses[0].tradeLicenseDetail,
    "address",
    {}
  );

  let ulbLogo = _.get(
    state.screenConfiguration.preparedFinalObject,
    "base64UlbLogo",
    ""
  );
  if (_.isEmpty(data1)) {
    console.log("Error in application data");
    return;
  } else if (_.isEmpty(data2)) {
    console.log("Error in receipt data");
    return;
  } else if (_.isEmpty(data3)) {
    console.log("Error in mdms data");
    return;
  } else if (_.isEmpty(data4)) {
    console.log("Error in auditor user data");
    return;
  } else if (_.isEmpty(ulbLogo)) {
    console.log("Error in image data");
    return;
  }
  let transformedData = {
    ...data1,
    ...data2,
    ...data3,
    ...data4,
    actualAddress:data5
  };
  switch (type) {
    case "certificate_download":

      let certificate_data = getCertificateData(transformedData, ulbLogo);
      certificate_data &&
     //  pdfMakeCustom.createPdf(certificate_data).download("tl_certificate.pdf");
      pdfMakeCustom.createPdf(certificate_data).open();
      break;
    case "certificate_print":
      certificate_data = getCertificateData(transformedData, ulbLogo);
      certificate_data && pdfMakeCustom.createPdf(certificate_data).print();
      break;
    case "receipt_download":
      let receipt_data = getReceiptData(transformedData, ulbLogo);

      receipt_data &&
     //   pdfMakeCustom.createPdf(receipt_data).download("tl_receipt.pdf");
        pdfMakeCustom.createPdf(receipt_data).open();
      break;
    case "receipt_print":
      receipt_data = getReceiptData(transformedData, ulbLogo);
      receipt_data && pdfMakeCustom.createPdf(receipt_data).print();
      break;
    default:
      break;
  }
};
```

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| PDF Generation service technical documentation | [PDF Generation Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/717979679/PDF+Generation+Service) |
| Customizing PDF Receipts & Certificates | [Customizing PDF Receipts & Certificates](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/720306189) |
| API Swagger Documentation | [Swagger Documentation](https://app.swaggerhub.com/apis/eGovernment/pdf-service_ap_is/1.1.0) |

### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
| _pdf-service/v1/\_create_ | [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |
| _pdf-service/v1/\_createnosave_ | [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |
| _pdf-service/v1/\_search_ | [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |

_\(Note: All the API’s are in the same postman collection therefore the same link is added in each row\)_

\_\_

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

