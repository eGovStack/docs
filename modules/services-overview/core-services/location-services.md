# Location Services

## Overview

A core application which provides location details of the tenant for which the services are being provided.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Java 8
* PSQL server is running and database is created
* Knowledge of egov-mdms service
* egov-mdms service is running and all the required mdms master are loaded in it

## Key Functionalities

* The location information is also known as boundary data of ULB
* Boundary data can be of different hierarchies ADMIN, ELECTION hierarchy which is defined by the Administrators, Revenue hierarchy defined by the Revenue department.
* The election hierarchy has the locations divided into several types like zone, election ward, block, street and locality. The Revenue hierarchy has the locations divided into a zone, ward, block and locality.
* The model which defines the localities like zone, ward and etc is boundary object which contains information like name, lat, long, parent or children boundary if any. The boundaries come under each other in a hierarchy like a zone contains wards, ward contains blocks, a block contains locality. The order in which the boundaries are contained in each other will differ based on the tenants.

| **Environment Variables** | **Description** |
| :--- | :--- |
| egov.services.egov\_mdms.hostname | Host name for MDMS service. |
| egov.services.egov\_mdms.searchpath | MDMS Search URL. |
| egov.service.egov.mdms.moduleName | MDMS module which contain boundary master. |
| egov.service.egov.mdms.masterName | MDMS master file which contain boundary detail. |

## Deployment Details

1. Add/Update the mdms master file which contain boundary data of ULB’s.
2. Add Role-Action mapping for egov-location API’s.
3. Deploy/Redeploy the latest version of egov-mdms service.
4. Fill the above environment variables in egov-location with proper values.
5. Deploy the latest version of egov-location service.

## Configuration Details

The boundary data has been moved to mdms from the master tables in DB. The location service fetches the JSON from mdms and parses it to the structure of boundary object as mentioned above. A sample master would look like below.

```text
{
  "tenantId": "pg.cityA",
   "moduleName": "egov-location",
  "TenantBoundary": [
  {
      "hierarchyType": {
              "code": "ADMIN",
              "name": "ADMIN"
      },
       "boundary": {
                "id": 1,
                "boundaryNum": 1,
                "name": "CityA",
                "localname": "CityA",
                "longitude": null,
                "latitude": null,
                "label": "City",
                "code": "pg.cityA",
                "children": []
        }

    }
 ]
}
```

| **Attribute Name** | **Description** |
| :--- | :--- |
| tenantId | The tenantId \(ULB code\) for which the boundary data configuration is defined. |
| moduleName | The name of the module where TenantBoundary master is present. |
| TenantBoundary.hierarchyType.code | Unique code of the hierarchy type. |
| TenantBoundary.hierarchyType.name | Unique name of the hierarchy type. |
| TenantBoundary.boundary.id | Id of boundary defined for particular hierarchy. |
| boundaryNum | Sequence number of boundary attribute defined for the particular hierarchy. |
| name | Name of the boundary like Block 1 or Zone 1 or City name. |
| localname | Local name of the boundary. |
| longitude | Longitude of the boundary. |
| latitude | Latitude of the boundary. |
| label | Label of the boundary. |
| code | Code of the boundary. |
| children | Details of its sub-boundaries. |

## Integration

### Integration Scope

The egov-location API’s can be used by any module which needs to store the location details of the tenant.

### Integration Benefits

* Get the boundary details based on boundary type and hierarchy type within the tenant boundary structure.
* Get the geographical boundaries by providing appropriate GeoJson.
* Get the tenant list in the given latitude and longitude.

### Steps to Integration

1. To integrate, host of egov-location should be overwritten in helm chart.
2. /boundarys/\_search should be added as the search endpoint for searching boundary details based on tenant Id, Boundary Type, Hierarchy Type etc.
3. /geography/\_search should be added as the search endpoint .This method handles all requests related to geographical boundaries by providing appropriate GeoJson and other associated data based on tenantId or lat/long etc.
4. /tenant/\_search should be added as the search endpoint. This method tries to resolve a given lat, long to a corresponding tenant, provided there exists a mapping between the reverse geocoded city to tenant.
5. The MDMS Tenant boundary master file should be loaded in MDMS service.

## Reference Docs

### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| Local setup | [ https://github.com/egovernments/core-services/blob/669c94194911ada92b6cb3c87e5fad7a7478cc6a/egov-location/LOCALSETUP.md](https://github.com/egovernments/core-services/blob/669c94194911ada92b6cb3c87e5fad7a7478cc6a/egov-location/LOCALSETUP.md) |

### API List

|  | **Link** |
| :--- | :--- |
| /boundarys/\_search | [https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman\_collection.json](https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman_collection.json) |
| /geography/\_search | [https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman\_collection.json](https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman_collection.json) |
| /tenant/\_search | [https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman\_collection.json](https://github.com/egovernments/core-services/blob/master/egov-location/postman/BoundaryNewVersion11Endpoint.postman_collection.json) |

Please refer to the [Swagger API contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-location/contracts/v11-0-0.yml#!/) for egov-location service to understand the structure of APIs and to have a visualisation of all internal APIs.

