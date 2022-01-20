# API Do's & Don'ts

APIs developed on digit follow certain conventions and principles. The aim of this document is to provide some do’s and don’ts while following those principles

* Always define the Yaml for your APIs as the first thing using Open API 3 Standard ([https://swagger.io/specification/](https://swagger.io/specification/))
* APIs path should be standardised as follows:
  * **/{service}/{entity}/{version}/\_create**: This endpoint should be used to create the entity
  * **/{service}/{entity}/{version}/\_update**: This endpoint should be used to edit an entity which is already existing
  * **/{service}/{entity}/{version}/\_search**: This endpoint should be used to provide search on the entity based on certain criteria
  * **/{service}/{entity}/{version}/\_count**: This endpoint should be provided to give a count of entities that match a given search criteria
* Always use POST for each of the endpoints
* Take most search parameters in the POST body only
* If query params for search need to be supported then make sure to have the same parameters in POST body also and POST body should take priority over query params
* Provide additional Details objects for **\_create** and **\_update** APIs so that custom requirements use these fields
* Each API should have a [**RequestInfo**](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L45) object in request body at the top level
* Each API should have a [**ResponseInfo**](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L154) object in response body at the top level
* Mandatory fields should be minimum for the APIs.
* minLength and maxLength should be defined for each attribute
* Read-only fields should be called out
* Use common models already available in the platform in your APIs. Ex -
  * [Address](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L228)
  * [User](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L96)(Citizen or Employee or Owner)
  * [Role](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L130)
  * [AuditDetails](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L270)
  * [ErrorRes](https://github.com/egovernments/core-services/blob/4e92620bd77fce183fdd66d3a8d9248f65561ada/docs/common-contract.yml#L213) (Response sent in case of errors)
  * TODO: Add all the models here
* For receiving files in an API, don’t use binary file data. Instead, accept the file store ids
* If there is only one file to be uploaded and no persistence is needed, and no additional json data is to be posted, you can consider using direct file upload instead of using filestore id

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
