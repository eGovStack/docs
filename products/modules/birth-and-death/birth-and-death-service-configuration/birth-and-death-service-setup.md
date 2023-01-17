# Birth & Death Service Setup

This is the egov application, which helps and provides a digital interface, allowing employees/citizens for downloading Birth & Death Certificates. Employees can register both birth and death applications, and update and search where the citizen has an access to download the certificates. There are two processes while downloading the certificates citizen can download the certificate free for the first time and it will be charged for the next downloads so the citizen has to pay the amount and download the certificates.

The setup of the Application is as follows

### **Requirements**

* Knowledge of Java/J2EE(preferably Java 8 version)
* Knowledge of Spring Boot and spring-boot microservices.
* Knowledge of Git or any version control system.
* Knowledge of RESTful Web services.
* Knowledge of the Lombok library will helpful.
* knowledge of eGov-mdms service, eGov-persister, eGov-idgen, eGov-sms, eGov-email,eGov-user, eGov-localization, eGov-workflow-service will be helpful.

### **Functionality**

1. The BnD Module facilitates the citizen to search and download the certificate.
2. The BnD Module enables the counter employee to enter the details of Birth and Death using\
   the Registration form.
3. The BnD Module provides a facility to the counter employee to search the details of\
   registration and view the details of the registration.
4. The BnD Module provides a facility to anyone who has downloaded the certificate, to check\
   the correctness of the certificate by scanning the QR Code.

### **Setup & Usage** <a href="#setup-and-usage" id="setup-and-usage"></a>

The [**Application**](https://github.com/egovernments/municipal-services/tree/master) is present among the _**municipal services**_ group of applications available in the eGov-services git repository with the folder name [**birth-death-services**](https://github.com/egovernments/DIGIT-Dev/tree/master/municipal-services/birth-death-services).  The spring boot application needs the **Lombok\*** extension added to your IDE to load it. Once the application is up and running API requests can be posted to the URL and ids can be generated.&#x20;

* in the case of IntelliJ, the plugin can be installed directly, for eclipse the Lombok jar location has to be added in the eclipse.ini file in this format  javaagent:lombok.jar

### **API Information** <a href="#api-information" id="api-information"></a>

* Please refer to Swagger API for YAML file details. Link -[<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-OSS/birth-death.yml at master · egovernments/DIGIT-OSS](https://github.com/egovernments/DIGIT-OSS/blob/master/municipal-services/docs/birth-death/birth-death.yml)

_**Application.properties File Information:**_

kafka topics persister configs for eGov persister

* `persister.save.birth.topic=save-birth-topic`
* `persister.update.birth.topic=update-birth-topic`

_**URLs for the external API references:**_

* eGvo mdms :-> egov.mdms.host = [https://dev.digit.org](https://dev.digit.org/)/
* eGov -idGen :-> egov.idgen.host = [https://dev.digit.org](https://dev.digit.org/)/
* localization service :-> egov.localization.host = [https://dev.digit.org](https://dev.digit.org/)/
* idGen Id formats :->\
  egov.idgen.birthapplnum.name=birth\_cert.receipt.id\
  egov.idgen.birthapplnum.format=BR/CB/01/2022-0/063768\
  egov.idgen.deathapplnum.name=death\_cert.receipt.id\
  egov.idgen.deathapplnum.format=DT/CB/01/2022-0/063767

### **Configuration**

_**Mdms configuration**_**:**

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/BusinessService.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/BusinessService.json)

```
{
      "businessService": "Birth Certificate Fees",
      "code": "BIRTH_CERT",
      "collectionModesNotAllowed": ["DD", "POSTAL_ORDER"],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "isCitizen": true,
      "type": "Adhoc"
    },
    {
      "businessService": "Death Certificate Fees",
      "code": "DEATH_CERT",
      "collectionModesNotAllowed": ["DD", "POSTAL_ORDER"],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true,
      "isCitizen": true,
      "type": "Adhoc"
    }
```

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TaxHeadMaster.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/TaxHeadMaster.json)

```
{
    "category": "CHARGES",
    "service": "BIRTH_CERT",
    "name": "BIRTH_CERT_FEE",
    "code": "BIRTH_CERT_FEE",
    "isDebit": false,
    "isActualDemand": false,
    "order": "0",
    "isRequired": false,
    "isDiscountApplicable": false
  },
  {
    "category": "CHARGES",
    "service": "DEATH_CERT",
    "name": "DEATH_CERT_FEE",
    "code": "DEATH_CERT_FEE",
    "isDebit": false,
    "isActualDemand": false,
    "order": "0",
    "isRequired": false,
    "isDiscountApplicable": false
  }
```

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TaxPeriod.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/TaxPeriod.json)

```
 {
      "fromDate": 1554076800000,
      "toDate": 1901145600000,
      "periodCycle": "ANNUAL",
      "service": "BIRTH_CERT",
      "code": "BIRTHCERT",
      "financialYear": "2019-30"
    },
    {
      "fromDate": 1554076800000,
      "toDate": 1901145600000,
      "periodCycle": "ANNUAL",
      "service": "DEATH_CERT",
      "code": "DEATHCERT",
      "financialYear": "2019-30"
    }
```

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/GLCode.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/BillingService/GLCode.json)

```
{
	"tenantId": "pb",
	"moduleName": "BillingService",
	"GLCode": [
	{
		"code": "BIRTH_CERT",
		"glcode": null,
		"cb": "pb.amritsar"
	},
	{
		"code": "DEATH_CERT",
		"glcode": null,
		"cb": "pb.amritsar"
	}
	]
}
```

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/bdTemplate.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/bdTemplate.json)

```
{
	"tenantId": "pb",
	"moduleName": "common-masters",
	"bdTemplate": [
		{
			"template": "bd-bihar",
			"code": "pb.danapur"
		},
		{
			"template": "bd-delhi",
			"code": "pb.delhi"
		},
		{
			"template": "bd-gujarat",
			"code": "pb.ahmedabad"
		},
		{
			"template": "bd-haryana",
			"code": "pb.ambala"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.bakloh"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.dagshai"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.dalhousie"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.jutogh"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.kasauli"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.khasyol"
		},
		{
			"template": "bd-himachalpradesh",
			"code": "pb.subathu"
		},
		{
			"template": "bd-badamibagh",
			"code": "pb.badamibagh"
		},
		{
			"template": "bd-jammu",
			"code": "pb.jammu"
		},
		{
			"template": "bd-jharkhand",
			"code": "pb.ramgarh"
		},
		{
			"template": "bd-karnataka",
			"code": "pb.belgaum"
		},
		{
			"template": "bd-kerala",
			"code": "pb.cannanore"
		},
		{
			"template": "bd-madhyapradesh",
			"code": "pb.jabalpur"
		},
		{
			"template": "bd-madhyapradesh",
			"code": "pb.mhow"
		},
		{
			"template": "bd-madhyapradesh",
			"code": "pb.pachmarhi"
		},
		{
			"template": "bd-madhyapradesh",
			"code": "pb.morar"
		},
		{
			"template": "bd-madhyapradesh",
			"code": "pb.saugor"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.ahmednagar"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.aurangabad"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.dehuroad"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.deolali"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.kamptee"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.kirkee"
		},
		{
			"template": "bd-maharashtra",
			"code": "pb.pune"
		},
		{
			"template": "bd-meghalaya",
			"code": "pb.shillong"
		},
		{
			"template": "bd-punjab",
			"code": "pb.amritsar"
		},
		{
			"template": "bd-punjab",
			"code": "pb.ferozepur"
		},
		{
			"template": "bd-punjab",
			"code": "pb.jalandhar"
		},
		{
			"template": "bd-rajasthan",
			"code": "pb.ajmer"
		},
		{
			"template": "bd-rajasthan",
			"code": "pb.nasirabad"
		},
		{
			"template": "bd-tamilnadu",
			"code": "pb.stm"
		},
		{
			"template": "bd-tamilnadu",
			"code": "pb.wellington"
		},
		{
			"template": "bd-telangana",
			"code": "pb.secunderabad"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.agra"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.allahabad"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.babina"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.bareilly"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.jhansi"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.kanpur"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.lucknow"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.faizabad"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.fatehgarh"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.mathura"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.meerut"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.shahjahanpur"
		},
		{
			"template": "bd-uttarpradesh",
			"code": "pb.varanasi"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.almora"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.chakrata"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.clementtown"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.dehradun"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.landour"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.lansdowne"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.nainital"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.ranikhet"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.roorkee"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.almora"
		},
		{
			"template": "bd-uttarakhand",
			"code": "pb.testing"
		},
		{
			"template": "bd-westbengal",
			"code": "pb.barrackpore"
		},
		{
			"template": "bd-jalapahar",
			"code": "pb.jalapahar"
		},
		{
			"template": "bd-lebong",
			"code": "pb.lebong"
		}
	]
}
```

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/IdFormat.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/IdFormat.json)

```
{
      "format": "BR/CB/[cb.name]/[fy:yyyy]/[SEQ_EGOV_COMMON]",
      "idname": "birth_cert.receipt.id"
    },
    {
      "format": "DT/CB/[cb.name]/[fy:yyyy]/[SEQ_EGOV_COMMON]",
      "idname": "death_cert.receipt.id"
    }
```

#### Access MDMS Config <a href="#access-mdms-config" id="access-mdms-config"></a>

**Action Test : URL Actions adding**

[action-test.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

```
{
      "id": 2277,
      "name": "BirthRecordsCountReport",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReport/_get",
      "displayName": "BirthRecordsCountReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2278,
      "name": "BirthRecordsCountReport",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReport/metadata/_get",
      "displayName": "BirthRecordsCountReport",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2279,
      "name": "BirthRecordsCountReport",
      "url": "url",
      "displayName": "Birth Records Count",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthRecordsCountReport",
      "navigationURL": "report/rainmaker-bnd/BirthRecordsCountReport",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2280,
      "name": "DeathRecordsCountReport",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReport/_get",
      "displayName": "DeathRecordsCountReport",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2281,
      "name": "DeathRecordsCountReport",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReport/metadata/_get",
      "displayName": "DeathRecordsCountReport",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2282,
      "name": "DeathRecordsCountReport",
      "url": "url",
      "displayName": "Death Records Count",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.DeathRecordsCountReport",
      "navigationURL": "report/rainmaker-bnd/DeathRecordsCountReport",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2283,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReportCBLevel/_get",
      "displayName": "BirthRecordsCountReportCBLevel",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2284,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/BirthRecordsCountReportCBLevel/metadata/_get",
      "displayName": "BirthRecordsCountReportCBLevel",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2285,
      "name": "BirthRecordsCountReportCBLevel",
      "url": "url",
      "displayName": "Birth Records Count CBLevel",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthRecordsCountReportCBLevel",
      "navigationURL": "report/rainmaker-bnd/BirthRecordsCountReportCBLevel",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2286,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReportCBLevel/_get",
      "displayName": "DeathRecordsCountReportCBLevel",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2287,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "/report/rainmaker-bnd/DeathRecordsCountReportCBLevel/metadata/_get",
      "displayName": "DeathRecordsCountReportCBLevel",
      "orderNumber": 2,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2288,
      "name": "DeathRecordsCountReportCBLevel",
      "url": "url",
      "displayName": "Death Records Count CBLevel",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.DeathRecordsCountReportCBLevel",
      "navigationURL": "report/rainmaker-bnd/DeathRecordsCountReportCBLevel",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2289,
      "name": "BirthAndDeathCertificatePayment",
      "url": "/report/rainmaker-bnd/BirthAndDeathCertificatePayment/metadata/_get",
      "displayName": "Birth-Death Payment Report",
      "orderNumber": 3,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2290,
      "name": "BirthAndDeathCertificatePayment",
      "url": "url",
      "displayName": "BnD Paid and Downloaded Records",
      "orderNumber": 9,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "bnd",
      "code": "null",
      "path": "cbbnd.BirthAndDeathCertificatePayment",
      "navigationURL": "report/rainmaker-bnd/BirthAndDeathCertificatePayment",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },
    {
      "id": 2291,
      "name": "Birth-Death : Birth Save Report",
      "url": "/birth-death-services/common/saveBirthImport",
      "displayName": "Birth Save",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2292,
      "name": "Birth-Death : Death Save Report",
      "url": "/birth-death-services/common/saveDeathImport",
      "displayName": "Death Save",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2293,
      "name": "Birth-Death : Birth Search Report",
      "url": "/birth-death-services/birth/_search",
      "displayName": "Birth Search",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2294,
      "name": "Birth-Death : Death Search Report",
      "url": "/birth-death-services/death/_search",
      "displayName": "Death Search",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2295,
      "name": "Birth-Death : Birth Update Report",
      "url": "/birth-death-services/common/updateBirthImport",
      "displayName": "Birth Update Report",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2296,
      "name": "Birth-Death : Death Update Report",
      "url": "/birth-death-services/common/updateDeathImport",
      "displayName": "Death Update Report",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2297,
      "name": "Dashboard Birth and Death",
      "url": "url",
      "displayName": "Birth and Death",
      "orderNumber": 4,
      "parentModule": "dss-dashboard",
      "enabled": true,
      "serviceCode": "DSS",
      "code": "null",
      "path": "Dashboard.Birth and Death",
      "navigationURL": "/digit-ui/employee/dss/dashboard/birth-death",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    },
    {
      "id": 2298,
      "name": "DSS Dashboard Config Birth and Death",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/birth-death",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
    },
    {
      "id": 2299,
      "name": "Death New Registration",
      "url": "death-employee/newRegistration",
      "parentModule": "",
      "displayName": "Death New Registration",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2300,
      "name": "Birth New Registration",
      "url": "birth-employee/newRegistration",
      "parentModule": "",
      "displayName": "Birth New Registration",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "leftIcon": "custom:library-books",
      "path": ""
    },
    {
      "id": 2301,
      "name": "Birth : My Applications",
      "url": "birth-citizen/myApplications",
      "parentModule": "",
      "displayName": "My Applications",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2302,
      "name": "Death : My Applications",
      "url": "death-citizen/myApplications",
      "parentModule": "",
      "displayName": "My Applications",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2303,
      "name": "Birth : Home",
      "url": "birth-citizen/home",
      "parentModule": "",
      "displayName": "Home",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2304,
      "name": "Death : Home",
      "url": "death-citizen/home",
      "parentModule": "",
      "displayName": "Home",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2305,
      "name": "Birth New Registration",
      "url": "url",
      "displayName": "Birth New Registration",
      "orderNumber": 4,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": "birth-certificate.new-registration",
      "navigationURL": "birth-employee/newRegistration",
      "leftIcon": "custom:library-books",
      "rightIcon": ""
    },
    {
      "id": 2306,
      "name": "Death New Registration",
      "url": "url",
      "displayName": "Death New Registration",
      "orderNumber": 4,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": "death-certificate.new-registration",
      "navigationURL": "death-employee/newRegistration",
      "leftIcon": "custom:library-books",
      "rightIcon": ""
    },
    {
      "id": 2307,
      "name": "Birth Search Certificate",
      "url": "url",
      "displayName": "Birth Search Certificate",
      "orderNumber": 4,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": "birth-certificate.search-certificate",
      "navigationURL": "birth-common/getCertificate",
      "leftIcon": "custom:library-books",
      "rightIcon": ""
    },
    {
      "id": 2308,
      "name": "Death Search Certificate",
      "url": "url",
      "displayName": "Death Search Certificate",
      "orderNumber": 4,
      "parentModule": "rainmaker-bnd",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": "death-certificate.search-certificate",
      "navigationURL": "death-common/getCertificate",
      "leftIcon": "custom:library-books",
      "rightIcon": ""
    },
    {
      "id": 2309,
      "name": "Birth Download",
      "url": "/birth-death-services/birth/_download",
      "displayName": "Download",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2310,
      "name": "Death Download",
      "url": "/birth-death-services/death/_download",
      "displayName": "Download",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2311,
      "name": "Birth View Certificate",
      "url": "/birth-death-services/birth/_viewfullCertData",
      "displayName": "View Certificate",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2312,
      "name": "Death View Certificate",
      "url": "/birth-death-services/death/_viewfullCertData",
      "displayName": "View Certificate",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2313,
      "name": "Get Hospitals",
      "url": "/birth-death-services/common/getHospitals",
      "displayName": "Get Hospitals",
      "orderNumber": 0,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "Birth-Death",
      "code": "null",
      "path": ""
    },
    {
      "id": 2314,
      "name": "Get file store id for consumer code",
      "url": "/birth-death-services/birth/_getfilestoreid",
      "parentModule": "",
      "displayName": "Get file store id for consumer code",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2315,
      "name": "my requests",
      "url": "/birth-death-services/birth/_searchApplications",
      "parentModule": "",
      "displayName": "my requests",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2316,
      "name": "rainmaker-citizen-birth",
      "url": "card",
      "displayName": "Birth",
      "orderNumber": 8,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "",
      "code": "",
      "path": "",
      "navigationURL": "birth-citizen/home",
      "leftIcon": "custom:library-books",
      "rightIcon": "",
      "queryParams": ""
    },

    {
      "id": 2317,
      "name": "death Search",
      "url": "/birth-death-services/death/_search",
      "parentModule": "",
      "displayName": "death Search",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2318,
      "name": "Download death Cert",
      "url": "/birth-death-services/death/_download",
      "parentModule": "",
      "displayName": "Download death Cert",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2319,
      "name": "Get file store id for consumer code",
      "url": "/birth-death-services/death/_getfilestoreid",
      "parentModule": "",
      "displayName": "Get file store id for consumer code",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2320,
      "name": "my requests",
      "url": "/birth-death-services/death/_searchApplications",
      "parentModule": "",
      "displayName": "my requests",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2321,
      "name": "rainmaker-citizen-death",
      "url": "card",
      "displayName": "death",
      "orderNumber": 8,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "",
      "code": "",
      "path": "",
      "navigationURL": "death-citizen/home",
      "leftIcon": "custom:library-books",
      "rightIcon": "",
      "queryParams": ""
    },
    {
      "id": 2322,
      "name": "View Certificate data",
      "url": "/birth-death-services/birth/_viewCertData",
      "parentModule": "",
      "displayName": "View Certificate data",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2323,
      "name": "Check Declaration",
      "url": "/birth-death-services/common/checkDeclaration",
      "parentModule": "",
      "displayName": "Check Declaration",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2324,
      "name": "Update Declaration",
      "url": "/birth-death-services/common/updateDeclaration",
      "parentModule": "",
      "displayName": "Update Declaration",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2325,
      "name": "BirthAndDeathCertificatePayment",
      "url": "/report/rainmaker-bnd/BirthAndDeathCertificatePayment/_get",
      "displayName": "Birth-Death Payment Report",
      "orderNumber": 3,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "report",
      "code": "null",
      "path": ""
    },
    {
      "id": 2326,
      "name": "PT Payment search",
      "url": "/collection-services/payments/BIRTH_CERT/_search",
      "displayName": "PT Payment search",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": false,
      "serviceCode": "",
      "code": "null",
      "path": ""
    },
    {
      "id": 2327,
      "name": "PT Payment search",
      "url": "/collection-services/payments/DEATH_CERT/_search",
      "displayName": "PT Payment search",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": false,
      "serviceCode": "",
      "code": "null",
      "path": ""
    },
    {
      "id": 2328,
      "name": "BND receipt search",
      "url": "/egov-pdf/download/BIRTHDEATH/birth-certificate",
      "displayName": "BND receipt search",
      "orderNumber": 3,
      "enabled": false,
      "serviceCode": "egov-pdf",
      "code": "null",
      "path": ""
    },
    {
      "id": 2329,
      "name": "BND receipt search",
      "url": "/egov-pdf/download/BIRTHDEATH/death-certificate",
      "displayName": "BND receipt search",
      "orderNumber": 3,
      "enabled": false,
      "serviceCode": "egov-pdf",
      "code": "null",
      "path": ""
    },
    {
      "id": 2333,
      "name": "BND how it works",
      "url": "/filestore/v1/files/static",
      "displayName": "BND how it works",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "birth-death-services",
      "code": "null",
      "path": ""
    },
    {
      "id": 2334,
      "name": "rainmaker-employee-birth",
      "url": "card",
      "displayName": "Birth",
      "orderNumber": 8,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "",
      "code": "",
      "path": "",
      "navigationURL": "birth-common/getCertificate",
      "leftIcon": "custom:library-books",
      "rightIcon": "",
      "queryParams": ""
    },
    {
      "id": 2335,
      "name": "rainmaker-employee-death",
      "url": "card",
      "displayName": "death",
      "orderNumber": 8,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "",
      "code": "",
      "path": "",
      "navigationURL": "death-common/getCertificate",
      "leftIcon": "custom:library-books",
      "rightIcon": "",
      "queryParams": ""
    },
    {
      "id": 2336,
      "name": "NSS Dashboard Config bnd",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/nss-bnd",
      "parentModule": "",
      "displayName": "NSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "NSS",
      "code": "null",
      "path": ""
    }
```

**Access to the Roles for the above Actions**

[roleacton.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

```
{
      "rolecode": "BND_CEMP",
      "actionid": 2294,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2294,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2294,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2295,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2295,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2295,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2296,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2296,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2296,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2297,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2297,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2298,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "EMPLOYEE",
      "actionid": 2298,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2298,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2299,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2300,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2301,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2301,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2302,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2302,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2303,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2303,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2303,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2303,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2304,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2304,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2305,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2306,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2307,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2307,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2308,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2308,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2309,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2309,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2310,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2310,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2311,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2311,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2312,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2312,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2313,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2313,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2314,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2314,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2315,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2315,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2316,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2317,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2317,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2318,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2318,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2319,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2319,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2320,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2320,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2321,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2322,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2322,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2323,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2323,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2324,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2324,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2325,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2325,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2326,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2326,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2327,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2327,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2328,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2328,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 2329,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 2329,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 1886,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BND_CEMP",
      "actionid": 1889,
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "BND_CEMP",
      "actionid": 1890,
      "actioncode": "",
      "tenantId": "pb"
    },
```

Birth and Death Roles

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/roles.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ROLES/roles.json)

```
{
      "code": "BND_CEMP",
      "name": "Birth and Death User",
      "description": "Birth and Death User"
    },
    {
      "code": "DASHBOARD_REPORT_VIEWER",
      "name": "Birth and Death Dashboard User",
      "description": "Birth and Death Dashboard User"
    },
    {
      "code": "BIRTH_APPLICATION_CREATOR",
      "name": "Birth Application Creator",
      "description": "Birth User that can only create new applications"
    },
    {
      "code": "DEATH_APPLICATION_CREATOR",
      "name": "Death Application Creator",
      "description": "Death User that can only create new applications"
    },
    {
      "code": "BIRTH_APPLICATION_VIEWER",
      "name": "Birth Application Viewer",
      "description": "Birth User that can only search and view applications"
    },
    {
      "code": "DEATH_APPLICATION_VIEWER",
      "name": "Death Application Viewer",
      "description": "Death User that can only search and view applications"
    },
    {
      "code": "BIRTH_REPORT_VIEWER",
      "name": "Birth Report Viewer",
      "description": "Birth and Death User that can view tabular reports"
    },
    {
      "code": "DEATH_REPORT_VIEWER",
      "name": "Death Report Viewer",
      "description": "Death User that can view tabular reports"
    },
    {
      "code": "BIRTH_APPLICATION_EDITOR",
      "name": "Birth Application Editor",
      "description": "Birth User that can edit existing applications"
    },
    {
      "code": "DEATH_APPLICATION_EDITOR",
      "name": "DEATH Application Editor",
      "description": "Death User that can edit existing applications"
    }
```

#### _**Persister configuration**_**:** <a href="#persister-configuration" id="persister-configuration"></a>

[BND Persister YAML](https://github.com/egovernments/configs/blob/DEV/egov-persister/birth-death.yml)

### Indexer Configuration <a href="#indexer-configuration" id="indexer-configuration"></a>

[Birth Indexer YAML](https://github.com/egovernments/configs/blob/DEV/egov-indexer/rainmaker-birth-indexer.yml)

[Death Indexer YAML](https://github.com/egovernments/configs/blob/DEV/egov-indexer/rainmaker-death-indexer.yml)

### Database Schema <a href="#database-schema" id="database-schema"></a>

![](<../../../../.gitbook/assets/image (230).png>)

### Postman Links <a href="#postman-links" id="postman-links"></a>

{% embed url="https://www.getpostman.com/collections/a6622af87bd5346d11fc" %}

