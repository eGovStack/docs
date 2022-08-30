# Birth & Death Service Configuration

**Objective:**

1. Register the Birth and death information of the citizen into the system.
2. To Correct any wrong information which is captured earlier.
3. To enable citizens to search and download their respective certificates.

## **Technical Details**

### **Birth Certificate - New Registration**

Both Birth and Death forms are quite similar.

MDMS details for hospitals:

Hospitals are configured at the city level.

```
{
    "tenantId": "pb.amritsar",
    "moduleDetails": [
        {
            "moduleName": "birth-death-service",
            "masterDetails": [
                {
                    "name": "hospitalList"
                }
            ]
        }
    ]
}
```

Birth registration file link: frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/birth-employee/newRegistration.js

Death registration file link: frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/death-employee/newRegistration.js

![](<../../../../.gitbook/assets/image (111).png>)

Filename: newRegistrationFooter.js

It contains the logic related to the validation of the form, submission, and API call details.

**APIs** **used -**

Birth - Create and Update API

* <mark style="background-color:blue;">birth-death-services/common/saveBirthImport</mark>
* <mark style="background-color:blue;">birth-death-services/common/updateBirthImport</mark>

Death - Create and Update API

* <mark style="background-color:blue;">birth-death-services/common/saveDeathImport</mark>
* <mark style="background-color:blue;">birth-death-services/common/updateDeathImport</mark>

**Search Certificate**

Search certificate is the same for both employee and citizen.

The employee has view option. Whereas citizens can download for free for the first time. Second time downloads the citizen have to Pay & Download.&#x20;

![](<../../../../.gitbook/assets/image (315).png>)

`BIRTH_APPLICATION_CREATOR` & `DEATH_APPLICATION_CREATOR` - the Birth Registration button is enabled on the search screen for this role.

Citizen View

![](<../../../../.gitbook/assets/image (75).png>)

API Details

<mark style="background-color:blue;">`birth-death-services/death/_search`</mark>

<mark style="background-color:blue;">`birth-death-services/birth/_search`</mark>

File Details -&#x20;

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/birth-common/getCertificate.js
```

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-bnd-dev/src/ui-config/screens/specs/death-common/getCertificate.js
```

Clicking on the **Pay and download** button **-** Generates demand for making a payment and after completing the payment it downloads the certificate automatically.

Auto download configuration file&#x20;

```
frontend/mono-ui/web/rainmaker/dev-packages/egov-common-dev/src/ui-config/screens/specs/egov-common/acknowledgement.js
```

`postPaymentSuccess` method enables the auto-download.\
\
Clicking on the **Download** button - searches for the filestore id and downloads the file.

* birth-death-services/birth/\_getfilestoreid?tenantId=\{{tenantid\}}\&consumerCode=\{{consumercode\}}
* birth-death-services/death/\_getfilestoreid?tenantId=\{{tenantid\}}\&consumerCode=\{{consumercode\}}

**My Applications**

* Citizen

Citizens can download certificates and receipts from the My Applications screen.

![](<../../../../.gitbook/assets/image (335).png>)

Download receipt MDMS configuration to fetch the Birth and death in business service dropdown file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">RAIN-6838 :: BND Download receipt config updated typt to adhoc · egovernments/egov-mdms-data@bc9efec](https://github.com/egovernments/egov-mdms-data/commit/bc9efec16a8c61e341e24be6a387939e36937675)

**How It Works Section**

The How It works section shows the configured pdf to help citizens download certificates. Similarly in other environments, the same file is added to the Asset folder.

Also in Global config file\
[https://qa.digit.org/egov-qa-assets/globalConfigs.js](https://qa.digit.org/egov-qa-assets/globalConfigs.js)\
`var assetS3Bucket = 'egov-qa-assets';`\
[egov-qa-assets/BDUserManual\_Citizen.pdf](https://s3.ap-south-1.amazonaws.com/egov-qa-assets/BDUserManual\_Citizen.pdf) is added and used to refer for downloading the file.

**Localization Module -** `rainmaker-bnd`

## **ROLE ACTION MAPPING**

| **API**                                       | **ROLES**                                                                   | **ACTION ID** |
| --------------------------------------------- | --------------------------------------------------------------------------- | ------------- |
| `egov-mdms-service/v1/_search`                |                                                                             | `954`         |
| `birth-death-services/death/_search`          | `BND_CEMP`, `CITIZEN`,`DEATH_APPLICATION_VIEWER`,`DEATH_APPLICATION_EDITOR` |               |
| `birth-death-services/birth/_search`          | `BND_CEMP`, `CITIZEN`,`BIRTH_APPLICATION_VIEWER`,`BIRTH_APPLICATION_EDITOR` |               |
| birth-death-services/birth/\_getfilestoreid   | `BND_CEMP`, `CITIZEN`                                                       |               |
| birth-death-services/death/\_getfilestoreid   | `BND_CEMP`, `CITIZEN`                                                       |               |
| birth-death-services/common/saveDeathImport   | `BND_CEMP`,`DEATH_APPLICATION_CREATOR`                                      |               |
| birth-death-services/common/updateDeathImport | `BND_CEMP`,`DEATH_APPLICATION_EDITOR`                                       |               |
| birth-death-services/common/saveBirthImport   | `BND_CEMP`,`BIRTH_APPLICATION_CREATOR`                                      |               |
| birth-death-services/common/updateBirthImport | `BND_CEMP`,`BIRTH_APPLICATION_EDITOR`                                       |               |

&#x20;[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
