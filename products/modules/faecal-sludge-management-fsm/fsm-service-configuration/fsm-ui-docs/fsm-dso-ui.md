# FSM DSO UI

## **Complete Request** <a href="#complete-request" id="complete-request"></a>

Fetching data from the MDMS

![](<../../../../../.gitbook/assets/image (6) (1).png>)

## Customizing Fields In A Form <a href="#customizing-fields-in-a-form" id="customizing-fields-in-a-form"></a>

The config can be found at CompleteApplication.js

**File Path:** _frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pages/employee/ApplicationDetails/config/CompleteApplication.js_

```
{
          label: "ES_NEW_APPLICATION_PROPERTY_TYPE",
          isMandatory: true,
          type: "component",
          route: "property-type",
          key: "propertyType",
          component: "SelectPropertyType",
          texts: {
            headerCaption: "",
            header: "CS_FILE_APPLICATION_PROPERTY_LABEL",
            cardText: "CS_FILE_APPLICATION_PROPERTY_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
          },
          nextStep: "property-subtype",
        },
        {
          label: "ES_NEW_APPLICATION_PROPERTY_SUB-TYPE",
          isMandatory: true,
          type: "component",
          route: "property-subtype",
          key: "subtype",
          component: "SelectPropertySubtype",
          texts: {
            headerCaption: "",
            header: "CS_FILE_APPLICATION_PROPERTY_SUBTYPE_LABEL",
            cardText: "CS_FILE_APPLICATION_PROPERTY_SUBTYPE_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
          },
          nextStep: "map",
        },
        {
          label: "ES_NEW_APPLICATION_PIT_TYPE",
          isMandatory: false,
          type: "component",
          route: "pit-type",
          key: "pitType",
          component: "SelectPitType",
          texts: {
            header: "CS_FILE_PROPERTY_PIT_TYPE",
            cardText: "CS_FILE_PROPERTY_PIT_TYPE_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
            skipText: "CORE_COMMON_SKIP_CONTINUE",
          },
          nextStep: "tank-size",
        },
        {
          route: "tank-size",
          component: "SelectTankSize",
          isMandatory: false,
          texts: {
            headerCaption: "",
            header: "CS_FILE_APPLICATION_PIT_SEPTIC_TANK_SIZE_TITLE",
            cardText: "CS_FILE_APPLICATION_PIT_SEPTIC_TANK_SIZE_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
          },
          type: "component",
          key: "pitDetail",
          nextStep: null,
          label: "ES_NEW_APPLICATION_PIT_DIMENSION",
        },
```

## Upload Pit Photo Button  <a href="#upload-pit-photo-button" id="upload-pit-photo-button"></a>

UploadPitPhoto.js molecule is available within the __ molecules folder in react-components.

**File Path:** _frontend/micro-ui/web/micro-ui-internals/packages/react-components/src/molecules/UploadPitPhoto.js_

Saving Image fileId in FSM service

```
const uploadImage = useCallback(async () => {
        if (uploadedImagesIds === null || uploadedImagesIds.length < 3) {
            const response = await Digit.UploadServices.Filestorage("FSM", image, props.tenantId);
            setUploadedImagesIds(addUploadedImageIds(response));
        } else {
            console.log("disabled")
        }
    }, [addUploadedImageIds, image]);
```

## Filter Component On DSO Inbox Screen <a href="#filter-component-in-dso-inbox-screen" id="filter-component-in-dso-inbox-screen"></a>

The link for the MDMS changes made is given below.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/RoleStatusMapping.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/DIGIT-UI/RoleStatusMapping.json)

&#x20;RoleStatusMappping.json

```
  {
            "userRole": "FSM_DSO",
            "statuses": [
                "DSO_INPROGRESS",
                "PENDING_DSO_APPROVAL",
                "COMPLETED",
            ],
            "zeroCheck": true,
            "fixed": false
        },
```

## Schedule Action For Post Pay In DSO <a href="#schedule-action-for-post-pay-in-dso" id="schedule-action-for-post-pay-in-dso"></a>

![](<../../../../../.gitbook/assets/image (17) (1) (1).png>)

Schedule Action is added for post-pay applications where DSOs can schedule the trip by entering the number of trips.

Code snippet for schedule window:

```
 case "SCHEDULE":
      case "ES_FSM_SCHEDULE":
        setFormValve(true);
        return setConfig(
          configScheduleDso({
            t,
            rejectMenu: Reason?.DeclineReason,
            setReason: setDeclineReason,
            reason: declineReason,
            applicationCreatedTime: applicationData?.auditDetails?.createdTime,
            vehicle,
            vehicleCapacity: applicationData?.vehicleCapacity,
            action,
            noOfTrips: applicationData?.noOfTrips
          })
        );
```

![](<../../../../../.gitbook/assets/image (10) (2).png>)

ScheduleDso.js is the file responsible for the schedule window pop up.&#x20;

**File path:** _**frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pages/employee/ApplicationDetails/config/ScheduleDso.js**_

_****_
