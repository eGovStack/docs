# Encryption Service

## Overview <a href="#overview" id="overview"></a>

The Encryption Service is used to secure sensitive data that is being stored in the database.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8._
* Kafka server is up and running.

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

Encryption Service offers the following features :&#x20;

1. Encrypt - The service encrypts the data based on given input parameters and data to be encrypted. The encrypted data is mandatory for a string data type.
2. Decrypt - The decryption will happen solely based on the input data (any extra parameters are not required). The encrypted data has the identity of the key used at the time of encryption, the same key will be used for decryption.
3. Sign - Encryption Service can hash and sign the data which can be used as the unique identifier of the data. This can also be used for searching the given value from a datastore.
4. Verify - Based on the input sign and the claim, it can verify if the given sign is correct for the provided claim.
5. Rotate Key - Encryption Service supports changing the key used for encryption. The old key will still remain with the service which will be used to decrypt old data. All the new data will be encrypted by the new key.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Following are the properties in the application.properties file in egov-enc-service which are configurable.

| Property               | Default Value   | Remarks                                                                                                                     |
| ---------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `master-password`      | asd@#$@$!132123 | Master password for encryption/ decryption.                                                                                 |
| `master.salt`          | qweasdzx        | A salt is random data that is used as an additional input to a one-way function that hashes data, a password or passphrase. |
| `master.initialvector` | qweasdzxqwea    | An initialization vector is a fixed-size input to a cryptographic primitive.                                                |
| `size.key.symmetric`   | 256             | Default size of Symmetric key.                                                                                              |
| `size.key.asymmetric`  | 1024            | Default size of Asymmetric key.                                                                                             |
| `size.initialvector`   | 12              | Default size of Initial vector.                                                                                             |

## &#x20;Deployment Details

1. Deploy the latest version of the Encryption Service.
2. Add Role-Action mapping for APIs.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The Encryption service is used to encrypt sensitive data that needs to be stored in the database.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform encryption without having to re-write encryption logic every time in every service.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of encryption services, modules should be overwritten in the helm chart.
2. `/crypto/v1/_encrypt` __ should be added as an end point for encrypting input data in the system
3. `/crypto/v1/_decrypt` should be added as the decryption endpoint.
4. `/crypto/v1/_sign` should be added as the endpoint for providing a signature for a given value.
5. `/crypto/v1/_verify` should be added as the endpoint for verifying whether the signature for the provided value is correct.
6. `/crypto/v1/_rotatekey` should be added as an end point to deactivate the keys and generate new keys for a given tenant.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| **Title**                 | **Link**                                                                                                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/core-services/docs/enc-service-contract.yml#!/) |

### API List <a href="#api-list" id="api-list"></a>

a) `POST /crypto/v1/_encrypt`

Encrypts the given input value/s OR values of the object.

b) `POST /crypto/v1/_decrypt`

Decrypts the given input value/s OR values of the object.

c) `/crypto/v1/_sign`

Provide signature for a given value.

d) `POST /crypto/v1/_verify`

Check if the signature is correct for the provided value.

e) `POST /crypto/v1/_rotatekey`

Deactivate the keys for the given tenant and generate new keys. It will deactivate both symmetric and asymmetric keys for the provided tenant.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
