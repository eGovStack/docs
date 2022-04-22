# Document Uploader Service

## Overview <a href="#overview" id="overview"></a>

Document uploader is used by ULB employees to upload documents that will then be visible to the citizens. In an effort to increase the engagement of citizens with mSeva platform, mSeva is providing this service to enable the citizens to view important documents related to their ULB such as acts, circulars, citizen charters etc.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of SpringBoot.
3. Prior Knowledge of PostgresSQL.
4. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
5. Prior Knowledge of JSONQuery in Postgres. (Similar to PostgresSQL with a few aggregate functions.)

## Key Functionalities & Configurations <a href="#key-functionalities-and-configurations" id="key-functionalities-and-configurations"></a>

Employees can perform all four operations i.e. creating, searching, updating and deleting the documents whereas the citizens can only search for the created documents. For creating documents in a particular ULB, the document category that needs to be provided in the create API cURL has to be present in the document category MDMS file for the tenantId for which the document is getting uploaded.&#x20;

A sample MDMS document category configuration file can be viewed here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/DocumentUploader.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DocumentUploader/DocumentUploader.json)

In this MDMS configuration file, ULB keys can be added and the allowed category types can be added in categoryList key.

Once a document is created in any ULB, the following attributes can be updated for that document -&#x20;

1. ULB
2. Document name
3. Document category
4. Links
5. Attachments

Upon deleting any document, that document is soft-deleted from the records i.e. that document’s active field is set to false.

## API Details <a href="#api-details" id="api-details"></a>

1. /egov-document-uploader/egov-du/document/\_create - Takes RequestInfo and DocumentEntity in request body. Document entity has all the parameters related to the document being inserted.
2. /egov-document-uploader/egov-du/document/\_update - Allows editing of attributes related to an already existing document. Searches document based on its uuid and updates attributes.
3. /egov-document-uploader/egov-du/document/\_search - Allows searching existing documents in the database. Takes search parameters in the url and RequestInfo in request body.
4. /egov-document-uploader/egov-du/document/\_delete - Soft deletes an existing document from the database i.e. it makes the document inactive. It takes the DocumentEntity that needs to be deleted in the request body along with RequestInfo object.

Detailed API payloads for interacting with document service for all the four endpoints can be found in the following collection -

[https://www.getpostman.com/collections/09392689c9a73347662e](https://www.getpostman.com/collections/09392689c9a73347662e)

### Swagger Documentation <a href="#swagger-documentation" id="swagger-documentation"></a>

Link to the swagger documentation can be found below -

[![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/egov-document-uploader-contract.yml)



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
