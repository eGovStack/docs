# FSM FSTPO UI

## FSTP Inbox Changes <a href="#fstp-inbox-changes" id="fstp-inbox-changes"></a>

1. _**Search by Application Number**_: We have added a search by application number field where FSTPO can search the vehicle trip detail by application number.
2. **Application No & Status column:** New Application No column and Status column are added to the Inbox table so that FSTPO can see the application number and status of the trip.

![](<../../../../../.gitbook/assets/image (422).png>)

### Technical Implementation Details

Code snippets to add the application search field inside the search fields object:

```
    {
      label: t("ES_SEARCH_APPLICATION_APPLICATION_NO"),
      name: "refernceNos",
    },
```

Code snippets to fetch the application number:

```
 const { isLoading: applicationLoading, isError, data: applicationData, error } = Digit.Hooks.fsm.useSearch(
    tenantId,
    { applicationNos: searchParams?.refernceNos, uuid: userInfo.uuid },
    { staleTime: Infinity }
  );
```

## Trip Number In FSTPO Details <a href="#trip-no-in-fstpo-details" id="trip-no-in-fstpo-details"></a>

![](<../../../../../.gitbook/assets/image (20).png>)

We have added the Trip No. field on the fstp-operator-details page so that the FSTPO can access the ongoing trip of the application number.

### Technical Implementation Details

Code snippet to check the current Trip:

```
  useEffect(() => {
    filterVehicle?.length == 0 ? setCurrentTrip(1) : setCurrentTrip((tripNo - filterVehicle?.length) + 1)
  }, [tripNo, filterVehicle, totalvehicle, totalsuccess, isSuccess]);

```

Code snippet to render the trip number field:

```
{!isSearchLoading && !isIdle && tripDetails && currentTrip ?
              <Row
                key={t("ES_VEHICLE_TRIP_NO")}
                label={`${t("ES_VEHICLE_TRIP_NO")} * `}
                text={
                  <div>
                    <Dropdown
                      disable
                      selected={{ "name": `${currentTrip} of ${tripDetails[0]?.noOfTrips}` }}
                      t={t}
                      optionKey="name"
                      style={{ maxWidth: '200px' }} />
                  </div>
                }
              >
              </Row> : null}
```
