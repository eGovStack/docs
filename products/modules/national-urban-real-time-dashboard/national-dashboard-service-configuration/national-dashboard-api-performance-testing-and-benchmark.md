# National Dashboard API Performance Testing and Benchmark

## Overview

Since we have around 600 wards in Punjab, we decided to make the national dashboard service robust enough to handle 600 requests simultaneously in a short time( preferably midnight when the employees ingest the day’s data ).

## Performance Testing Details

The national dashboard ingest service API underwent extensive stress testing. The service was tested for 25 concurrent threads (users) targeting 100 requests per minute with each request payload containing 30 records (the ingest API is a bulk API). The service passed all the tests with 0 percent error with a throughput of 21 requests per second with a total number of samples being 12671 in 10 minutes which roughly equals 21 requests per second.

The stress test ran with the following configuration and reliably persisted each and every record that was ingested -&#x20;

National-dashboard-ingest service -&#x20;

* Number of pods- 5
* Number of threads for each pod- 25
* Heap memory- 750 mb
* Producer linger time- 1 ms

National dashboard Kafka pipeline service -

* Number of pods- 3
* Number of threads for each pod- 10
* Heap memory- 512 mb
* Producer linger time- 1 ms

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
