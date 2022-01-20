# FileStore Service

## Overview <a href="#overview" id="overview"></a>

An eGov core application that handles uploading different kinds of files to servers including images and different document types.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE
2. Prior Knowledge of Spring Boot
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc
4. Prior knowledge of AWS and Azure

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The filestore application takes in a request object which contains an image/document or any kind of file and stores them in a disk/AWS/azure. Depending upon the configurations, additional implementations can be written for the app interface to interact with any other remote storage.

The requested file to be uploaded is taken in form of a multi-part file then saved to the storage and a uuid is returned as a unique identifier for that resource. This is used to fetch the documents later.

In the case of images, the application creates three more additional copies of the file in the likes of large, medium and small for the usage of thumbnails or low-quality images in the case of mobile applications.

The search API takes the uuid, tenantid as mandatory url params and a few optional parameters and returns the presigned url of the files from the server. In the case of images, a single string containing multiple urls separated by commas is returned representing different sizes of images stored.

### Setup And Configuration <a href="#setup-and-configuration" id="setup-and-configuration"></a>

The **Application** is present among the core group of applications available in the eGov-services git repository.  The spring boot application needs **lombok** extension added in your ide to load it. Once the application is up and running API requests can be posted to the URL and ids can be generated.&#x20;

&#x20;In case of intellij, the plugin can be installed directly, for eclipse the lombok jar location has to be added in eclipse.ini file in this format **-javaagent:lombok.jar**.

For the API information please refer to the swagger yaml \
GOTO : [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io)   and click on file -> import url\
Then add the raw url of the API doc in the pop up\
\---> add url here&#x20;

In case the url is unavailable, please go to the [docs folder](https://github.com/egovernments/egov-services/tree/master/docs) of egov-services git repo and find the yaml for egov-filestore.

The application needs at least one type of storage available for it to store the files. It can be either file storage, AWS S3 or azure. More storage types can be added by extending the application interface too.

To work any of the file storage there are some application properties that need to be configured.

**DiskStorage**

The mount path of the disk should be provided in the following variable to save files in the disc. **file.storage.mount.path=path.**

Following are the variables that needs to be populated based on the aws/azure account you are integrating with.

**How to enable Minio SDC**

minio.url=[http://minio](http://minio).backbone:9000(Minio server end point)

isS3Enabled=true(Should be true)

aws.secretkey={minio\_secretkey}

aws.key={minio\_accesskey}

fixed.bucketname=egov-rainmaker(Minio bucket name)

minio.source=minio

**How to enable AWS S3**

minio.url=[https://s3.amazonaws.com](https://s3.amazonaws.com)

isS3Enabled=true(Should be true)

aws.secretkey={s3\_secretkey}

aws.key={s3\_accesskey}

fixed.bucketname=egov-rainmaker(S3 bucket name)

minio.source=minio

**AZURE**

**isAzureStorageEnabled** - informing the application whether Azure is available or not

**azure.defaultEndpointsProtocol -** type of protocol **https**

**azure.accountName -** name of the user account&#x20;

**azure.accountKey -** secret key of the user account

**NFS**&#x20;

**isnfsstorageenabled**-informing the application whether NFS is available or not \<True/False>

**file.storage.mount.path** - \<NFS location, example /filestore>

**source.disk -** diskStorage - name of storage

**disk.storage.host.url**=\<Main Domain URL>

\
**Allowed formats to be uploaded**

\# the default format of the allowed file formats goes in a set bracket with string inside it - {"jpg","png"} - please follow the same.

_**allowed.formats.map**_={jpg:{'image/jpg','image/jpeg'},jpeg:{'image/jpeg','image/jpg'},png:{'image/png'},pdf:{'application/pdf'},odt:{'application/vnd.oasis.opendocument.text'},ods:{'application/vnd.oasis.opendocument.spreadsheet'},docx:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},doc:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},dxf:{'text/plain'},csv:{'text/plain'},txt:{'text/plain'},xlsx:{'application/x-tika-ooxml','application/x-tika-msoffice'},xls:{'application/x-tika-ooxml','application/x-tika-msoffice'}}

The key in the map is the visible extension of the file types, the values on the right in curly braces are the respective tika types of the file. these values can be found on the tika website or by passing the file through the tika functions.

### Available features <a href="#available-features" id="available-features"></a>

1. **Upload**\
   POST API to save the files on the server
2. **Search Files**\
   GET API to retrieve file based only on id and tenantid
3. **Search URLs** \
   GET API  to retrieve pre-signed urls for a given array of ids

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of Filestore Service
2. Add Role-Action mapping for APIs

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The filestore service is used to upload and store documents that citizens add while availing services from ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform file upload independently without having to add file upload specific logic in each module.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of filestore modules should be overwritten in the helm chart.
2. `/filestore/v1/files` __ should be added as the endpoint for uploading the file in the system
3. `/filestore/v1/files/url` should be added as the search endpoint. This method handles all requests to search existing files depending on different search criteria

### Postman Collection <a href="#postman-collection" id="postman-collection"></a>

{% embed url="https://www.getpostman.com/collections/1b448834735adf1acc4a" %}

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
