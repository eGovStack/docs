# Customizing PDF Receipts & Certificates

### Overview <a id="Overview"></a>

The objective of PDF generation service is to bulk generate pdf as per requirement. This document contains details about how to create the config files which are required to generate new pdf.

### Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior knowledge of JavaScript.
* Prior knowledge of Node.js platform.
* JSONPath for filtering required data from json objects.

### Key Functionalities <a id="Key-Functionalities"></a>

* Provide flexibility to customise the PDF as per the requirement.
* Supports localisation.
* Provide functionality to add an image, Qr Code in PDF.
* Provide functionality to call external service for creating PDF with external service response

### Deployment Details <a id="Deployment-Details"></a>

1. Create data config and format config for a PDF according to product requirement.
2. Add data config and format config files in PDF configuration
3. Add the file path of data and format config in the environment yml file
4. Deploy the latest version of pdf-service in a particular environment.

### Configuration Details <a id="Configuration-Details"></a>

**Config file:** A json config file which contains the configuration for pdf requirement. For any pdf requirements, we have to add two configs file to the service.

* **Format Config file:** This config file define the format of PDF. In format config, we define the UI structure ex: css, layout etc. for pdf as per PDFMake syntax of pdf. In PDF UI, the places where values are to be picked from the request body are written as “{{variableName}}” as per ‘mustache.js’ standard and are replaced by this templating engine. ex:[ ![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/configs/tree/master/pdf-service/format-config - Connect to preview](https://github.com/egovernments/configs/tree/master/pdf-service/format-config)
* **Data Config file:** This file contains a mapping to pick data from request body, external service call body if there is any and the variable which defines where this value is to be replaced in format by the templating engines \(mustache.js\). The variable which is declared in the format config file must be defined in the data config file. ex:[ ![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/configs/tree/master/pdf-service/data-config - Connect to preview](https://github.com/egovernments/configs/tree/master/pdf-service/data-config)

PDF generation service read these such files at start-up to support PDF generation for all configured module.

#### The data config file  contains the following aspects  <a id="The-data-config-file--contains-the-following-aspects-:"></a>

| **Attribute** | **Description** |
| :--- | :--- |
| key | The key for the pdf, it is used as a path parameter in URL to identify for which PDF has to generate. |
| baseKeyPath | The json path for the array object that we need to process.  |
| entityIdPath | The json path for the unique field which is stored in DB. And that unique ****field value is mapped to file-store id, so we can directly search the pdf which was created earlier with the unique field value and there will be no need to create PDF again. |
| Direct Mapping | In direct mapping, we define the variable whose value can be fetched from the array object which we extracted using baseKeyPath. |
| ExternalApi Mapping | The externalApi mapping is used only if there is a need for values from other service response. In externalApi mapping, API endpoint has to be set properly with the correct query parameter. |
| Derived mapping | In derived mapping, the estimation of variable characterized here is equivalent to the esteem acquired from the arithmetic operation between the direct mapping variable and externalApi mapping variable. |
| Qr code Config mapping | This mapping is used to draw QR codes in the PDFs. The text to be shown after scan can be a combination of static text and variables from direct and externalApi mappings. |

**Sample structure of variable definition in data config** 

```text
{
  “Variable”: “variable_name”,
  “Value”:{
      “path”: “$.propertyId”             -----> jsonpath to obtain value.
  }

}
```

```text
 {
  “Variable”: “variable_name”,
  “Value”:{
    “path”: “$.propertyId”             -----> jsonpath to obtain value or key to obtain value from localisation.
  },
  “type”:  “label”,                    -----> this field is used to mark this variable as label.       
  “localisation”:{
      “required”: “false”,             -----> if this field is true then  localisation is used for this variable and vice versa.
      “prefix”: “null”,                -----> prefix of the key which is declared in path field.
      “module”: “rainmaker-tl”         -----> the module from which localisation entry is fetched
  }
}
```

**Example to show date in PDF**

```text
{
  “Variable”: “variable_name”,
  “Value”:{
    “path”: “$.date”             -----> jsonpath to obtain epoch value of date
  },
  “type”: "date"                  -----> this field is used to mark this variable as date.       
  "format": "YYYY/MM/DD "
}
```

If the format field is not specified in date variable declaration then in PDF date is shown with the default format of DD/MM/YYYY. For more details refer this page [Unix-Timestamp](https://momentjs.com/docs/#/parsing/unix-timestamp-milliseconds/)

**Example of external API calling to MDMS service**

```text
“externalAPI”: [
    “path”: “http://egov-mdms-service:8080/egov-mdms-service/v1/_get”,
    “queryParam”: “moduleName=tenant&masterName=tenants&tenantId=pb&filter=%5B?(@.code=='{$.tenantId}')%5D”,
    “apiRequest”: null,
    “responseMapping”:[
      {
          “variable”: “address”,
          “value”: “$.MdmsRes.tenant.tenants[0].address”
      },
      {
          “variable”: “phoneNumber”,
          “value”: “$.MdmsRes.tenant.tenants[0].contactNumber”
      }
    ]
  ]
```

**Example of adding Qr Code**  
  
For adding Qr code there is separate mapping with the name “qrcodeConfig“ in data config. This mapping can use variables defined in “direct” and “external“ mappings along with the ****static text. The information on the QR Code scan will be defined as value. The variable defined in this mapping can directly be used in the ****format config as an image. ex:-

Data Config for Qr Code:

```text
"mappings": [
          {
            "direct": [
              {
                "variable": "propertyID",
                "value": {
                  "path": "$.consumerCode"
                }
              },
              {
                "variable": "tenantId",
                "value": {
                  "path": "$.tenantId"
                }
              },
              {
                "variable": "businessServiceCode",
                "value": {
                  "path": "$.businessService"
                }
              }
            ]
          },
          {
            "qrcodeConfig": [
              {
                "variable": "qrcodeimage",
                "value": "citizen/egov-common/pay?consumerCode={{propertyID}}&tenantId={{tenantId}}&businessService={{businessServiceCode}}"
              }
            ]
          }
        ]
```

#### The format config file  contains the following aspects  <a id="The-format-config-file--contains-the-following-aspects-:"></a>

| **Attribute** | **Description** |
| :--- | :--- |
| key | The key for the pdf, it is used as a path parameter in URL to identify the PDF that has to be generated. |
| Content | In this section, the view of pdf is set. What has to appear on pdf is declared here, it is just like creating a static HTML page. The variable which is defined in data config is declared here and place in position as per the requirement. We can also create a table here and set the variable as per requirement.  |
| Style | This section is used to style the component, set the alignment and many more. Basically, it's like a CSS to style the HTML page. |

**Example of adding footer in PDF \(adding page number in the footer\)**

```text
{
"key": "property-bill",
"config": {
"defaultStyle": {....},
"content": [....],
"style": {....},
"footer": "(function(currentPage, pageCount) { return currentPage.toString() + ' of ' + pageCount; })"
}
}
```

The position of page number in the footer is configurable. For more detail refer this document [Header and Footer](https://pdfmake.github.io/docs/document-definition-object/headers-footers/)

**Example of adding Qr Code**  
  
Format Config for Qr Code

```text
{
  "image": "{{qrcodeimage}}", ----> use declared variable in qrcodeConfig from dataconfig
  "width": 64,
  "height": 64
}
```

### Integration <a id="Integration"></a>

For Integration with UI, please refer to the links in Reference Docs 

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
| PDF Generation service technical documentation | [PDF Generation Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/717979679/PDF+Generation+Service)   |
|  Steps for Integration of PDF in UI for download and print PDF |  [Integration of PDF in UI for download and print PDF](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/720470017/Integration+of+PDF+in+UI+for+download+and+print+PDF) |
| API Swagger Documentation | [Swagger Documentation](https://app.swaggerhub.com/apis/eGovernment/pdf-service_ap_is/1.1.0) |

#### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
| _pdf-service/v1/\_create_ | [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |
|  _pdf-service/v1/\_createnosave_ |  [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |
| _pdf-service/v1/\_search_ | [https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad](https://www.getpostman.com/collections/5a9bfd6fd03f9f2a6fad) |

 _\(Note: All the API’s are in the same postman collection, therefore, the same link is added in each row\)_

