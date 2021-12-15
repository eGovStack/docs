# Persister Configuration

Persister Service persists data in the database in a sync manner providing very low latency. The queries which have to be used to insert/update data in the database are written in yaml file. The values which have to be inserted are extracted from the json using jsonPaths defined in the same yaml configuration. Below is a sample configuration which inserts data in a couple of tables.

```
serviceMaps:
  serviceName: pgr-services
  mappings:
  - version: 1.0
    description: Persists pgr service request in tables
    fromTopic: save-pgr-request
    isTransaction: true
    queryMaps:

    - query: INSERT INTO eg_pgr_service_v2(id, tenantid,  additionaldetails, createdby, createdtime, lastmodifiedby, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?);
      basePath: service
      jsonMaps:
      - jsonPath: $.service.id

      - jsonPath: $.service.tenantId

      - jsonPath: $.service.additionalDetail
        type: JSON
        dbType: JSONB

      - jsonPath: $.service.auditDetails.createdBy

      - jsonPath: $.service.auditDetails.createdTime

      - jsonPath: $.service.auditDetails.lastModifiedBy

      - jsonPath: $.service.auditDetails.lastModifiedTime

    - query: INSERT INTO eg_pgr_address_v2(id, tenantid, parentid, doorno, plotno, buildingname, street, landmark, city, pincode) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
      basePath: service.address
      jsonMaps:
      - jsonPath: $.service.address.id

      - jsonPath: $.service.address.tenantId

      - jsonPath: $.service.id

      - jsonPath: $.service.address.doorNo

      - jsonPath: $.service.address.plotNo

      - jsonPath: $.service.address.buildingName

      - jsonPath: $.service.address.street

      - jsonPath: $.service.address.landmark

      - jsonPath: $.service.address.city

      - jsonPath: $.service.address.pincode


```

The above configuration is used to insert data published on the kafka topic save-pgr-request in the tables eg\_pgr\_service\_v2 and eg\_pgr\_address\_v2. Similarly, the configuration can be written to update data. Following is a sample configuration:

```
 - version: 1.0
    description: Updates pgr service request in tables
    fromTopic: update-pgr-request
    isTransaction: true
    queryMaps:

    - query: UPDATE eg_pgr_service_v2 SET servicecode=?,additionaldetails=?, lastmodifiedby=?, lastmodifiedtime=? WHERE id=?;
      basePath: service
      jsonMaps:
      - jsonPath: $.service.serviceCode

      - jsonPath: $.service.additionalDetail
        type: JSON
        dbType: JSONB

      - jsonPath: $.service.auditDetails.lastModifiedBy

      - jsonPath: $.service.auditDetails.lastModifiedTime

      - jsonPath: $.service.id


    - query: UPDATE eg_pgr_address_v2 SET doorno=?, plotno=?, buildingname=?, street=?, landmark=?, city=?, pincode=? WHERE id=?;
      basePath: service.address
      jsonMaps:

      - jsonPath: $.service.address.doorNo

      - jsonPath: $.service.address.plotNo

      - jsonPath: $.service.address.buildingName

      - jsonPath: $.service.address.street

      - jsonPath: $.service.address.landmark

      - jsonPath: $.service.address.city

      - jsonPath: $.service.address.pincode

      - jsonPath: $.service.address.id
```

The above configuration is used to update the data in tables. Similarly, the upsert operation can be done using ON CONFLICT() function in psql. Following table describe each field in the configuration.

|                   |                                                                  |
| ----------------- | ---------------------------------------------------------------- |
| **Variable Name** | **Description**                                                  |
| serviceName       | The module name to which the configuration belongs               |
| version           | Version of the config                                            |
| description       | Detailed description of the operations performed by the config   |
| fromTopic         | Kafka topic from which data has to be persisted in DB            |
| isTransaction     | Flag to enable/disable perform operations in Transaction fashion |
| query             | Prepared Statements to insert/update data in DB                  |
| basePath          | JsonPath of the object that has to be inserted/updated.          |
| jsonPath          | JsonPath of the fields that has to be inserted in table columns  |
| type              | Type of field                                                    |
| dbType            | DB Type of the column in which field is to be inserted           |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
