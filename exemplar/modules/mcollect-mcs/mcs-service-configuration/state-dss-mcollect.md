---
description: Technical Doc
---

# State DSS - mCollect

**mCollect Documentation**

\
DSS has two sides to it. One being the process in which the Data is pooled to ElasticSearch and the other being the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of Data Set, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this flow of process.&#x20;

This document explains the steps on how to define the configurations for Analytics Side Of DSS for W\&S.

**What is analytics?**

**Analytics :** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations.&#x20;

&#x20;

**Analytics Configurations:**\
Analytics contains multiple configurations. we need to add the changes related to mCollect in this dashboard-analytics.\
Here is the location : [![](https://github.com/fluidicon.png)configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)

\
Below is a list of configurations that need to be changed to run W\&S successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

#### **Description :** <a href="#description" id="description"></a>

**Chart API Configuration :**&#x20;

Each Visualization has its own properties. Each Visualization comes from different data sources (Sometimes it is a combination of different data sources)&#x20;

In order to configure each visualization and their properties, we have a Chart API Configuration Document.

In this, Visualization Code, which happens to be the key, will be having its properties configured as a part of configuration and are easily changeable.

&#x20;

Here is the sample ChartApiConfiguration.json data for the mCollect.

&#x20;

&#x20;

`1"mcTodaysCollection": { 2 "chartName": "DSS_TOTAL_COLLECTION_TODAY", 3 "queries": [ 4 { 5 "module": "COMMON", 6 "dateRefField": "", 7 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\"}", 8 "indexName": "dss-collection_v2", 9 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}],\"must\":[{\"range\":{\"dataObject.paymentDetails.receiptDate\":{\"gte\":\"now-1d\",\"lte\":\"now\"}}}] }},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}" 10 } 11 ], 12 "chartType": "metric", 13 "valueType": "Amount", 14 "drillChart": "none", 15 "documentType": "_doc", 16 "action": "", 17 "aggregationPaths": [ 18 "Todays Collection" 19 ], 20 "insight": {}, 21 "_comment": " " 22 }, 23 24 "mcTotalCollection": { 25 "chartName": "DSS_TOTAL_COLLECTION", 26 "queries": [ 27 { 28 "module": "COMMON", 29 "dateRefField": "dataObject.paymentDetails.receiptDate", 30 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\"}", 31 "indexName": "dss-collection_v2", 32 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}" 33 } 34 ], 35 "chartType": "metric", 36 "valueType": "Amount", 37 "drillChart": "none", 38 "documentType": "_doc", 39 "action": "", 40 "aggregationPaths": [ 41 "Total Collection" 42 ], 43 "insight": { 44 "chartResponseMap" : "mcTotalCollection", 45 "action" : "differenceOfNumbers", 46 "upwardIndicator" : "positive", 47 "downwardIndicator" : "negative", 48 "textMessage" : "$indicator$value% than last $insightInterval", 49 "colorCode" : "#228B22", 50 "insightInterval" : "year" 51 52 }, 53 "_comment": " " 54 }, 55 56 "mcCumulativeCollection": { 57 "chartName": "DSS_TOTAL_CUMULATIVE_COLLECTION", 58 "queries": [ 59 { 60 "module": "COMMON", 61 "dateRefField": "dataObject.paymentDetails.receiptDate", 62 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\r\n \"module\" : \"dataObject.paymentDetails.businessService.keyword\", \n\"tenantId\" : \"dataObject.tenantId\"}", 63 "indexName": "dss-collection_v2", 64 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 65 } 66 ], 67 "chartType": "line", 68 "valueType": "amount", 69 "action": "", 70 "drillChart": "none", 71 "documentType": "_doc", 72 "aggregationPaths": [ 73 "Collections" 74 ], 75 "isCumulative": true, 76 "interval": "month", 77 "insight": {}, 78 "_comment": " " 79 }, 80 "mcTargetAchieved": { 81 "chartName": "DSS_TARGET_ACHIEVED", 82 "queries": [ 83 { 84 "module": "COMMON", 85 "requestQueryMap": "{\r\n \"module\" : \"businessService.keyword\", \n\"tenantId\" : \"tenantIdForMunicipalCorporation\"}", 86 "dateRefField": "", 87 "indexName": "dss-target_v1", 88 "aggrQuery": "{\"aggs\":{\"Actual collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}" 89 }, 90 { 91 "module": "COMMON", 92 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\r\n \"district\" : \"dataObject.tenantData.city.districtCode\", \"module\" : \"dataObject.paymentDetails.businessService.keyword\", \n\"tenantId\" : \"dataObject.tenantId\"}", 93 "dateRefField": "dataObject.paymentDetails.receiptDate", 94 "indexName": "dss-collection_v2", 95 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Total Collection3\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}" 96 } 97 ], 98 "chartType": "metric", 99 "valueType": "percentage", 100 "drillChart": "none", 101 "documentType": "_doc", 102 "action": "percentage", 103 "aggregationPaths": [ 104 "Total Collection3", 105 "Actual collection" 106 ], 107 "insight": { 108 "chartResponseMap": "targetAchieved", 109 "action": "differenceOfNumbers", 110 "upwardIndicator": "positive", 111 "downwardIndicator": "negative", 112 "textMessage": "$indicator$value% than last $insightInterval", 113 "colorCode": "#228B22", 114 "insightInterval": "month" 115 }, 116 "_comment": " " 117 }, 118 119 "mcTotalCollectionCategoryWise": { 120 "chartName": "DSS_MC_COLLECTION_CATEGORY_WISE", 121 "queries": [ 122 { 123 "module": "COMMON", 124 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 125 "dateRefField": "dataObject.paymentDetails.receiptDate", 126 "indexName": "dss-collection_v2", 127 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"PT\",\"TL\"]}}]}},\"aggs\":{\"Business Service\":{\"terms\":{\"field\":\"dataObject.paymentDetails.businessService.keyword\",\"order\":{\"total\":\"desc\"}},\"aggs\":{\"total\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 128 } 129 ], 130 "chartType": "pie", 131 "valueType": "amount", 132 "action": "", 133 "documentType": "_doc", 134 "drillChart": "none", 135 "aggregationPaths": [ 136 "Business Service" 137 ], 138 "insight": {}, 139 "_comment": " " 140 }, 141 142 "mcCollectionByPaymentType": { 143 "chartName": "DSS_MC_COLLECTION_BY_PAYMENT_TYPE", 144 "queries": [ 145 { 146 "module": "COMMON", 147 "requestQueryMap": "{\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\"}", 148 "dateRefField": "dataObject.paymentDetails.receiptDate", 149 "indexName": "dss-collection_v2", 150 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Payment Mode\":{\"terms\":{\"field\":\"dataObject.paymentMode.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 151 } 152 ], 153 "chartType": "pie", 154 "valueType": "amount", 155 "action": "", 156 "documentType": "_doc", 157 "drillChart": "none", 158 "aggregationPaths": [ 159 "Payment Mode" 160 ], 161 "insight": {}, 162 "_comment": "" 163 }, 164 165 "totalmcDDRRevenue": { 166 "chartName": "DSS_MC_KEY_FY_INDICATORS", 167 "queries": [ 168 { 169 "module": "COMMON", 170 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 171 "dateRefField": "dataObject.paymentDetails.receiptDate", 172 "indexName": "dss-collection_v2", 173 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}" 174 }, 175 { 176 "module": "COMMON", 177 "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}", 178 "dateRefField": "", 179 "indexName": "dss-target_v1", 180 "aggrQuery": "{\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}" 181 } 182 ], 183 "isMdmsEnabled": true, 184 "filterKeys": [ 185 { 186 "key": "Business Service", 187 "column": "Business Service" 188 } 189 ], 190 "isPostResponseHandler": true, 191 "postAggregationTheory": "repsonseToDifferenceOfDates", 192 "chartType": "table", 193 "valueType": "number", 194 "drillChart": "totalmcBoundaryRevenue", 195 "documentType": "_doc", 196 "action": "", 197 "plotLabel": "Business Service", 198 "aggregationPaths": [ 199 "Total Collection", 200 "Transactions", 201 "Target Collection" 202 ], 203 "pathDataTypeMapping": [ 204 { 205 "Total Collection": "amount" 206 }, 207 { 208 "Transactions": "number" 209 }, 210 { 211 "Target Collection": "amount" 212 } 213 ], 214 "insight": {}, 215 "_comment": "" 216 }, 217 218 "totalmcBoundaryRevenue": { 219 "chartName": "DSS_MC_DEMAND_COLLECTION_BOUNDARY", 220 "queries": [ 221 { 222 "module": "COMMON", 223 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 224 "dateRefField": "dataObject.paymentDetails.receiptDate", 225 "indexName": "dss-collection_v2", 226 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"Business Service \":{\"terms\":{\"field\":\"dataObject.paymentDetails.businessService.keyword\",\"size\":2000,\"order\":{\"total\":\"asc\"}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}}}" 227 }, 228 { 229 "module": "COMMON", 230 "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}", 231 "dateRefField": "", 232 "indexName": "dss-target_v1", 233 "aggrQuery": "{\"aggs\":{\"Business Service \":{\"terms\":{\"field\":\"tenantIdForMunicipalCorporation.keyword\",\"size\":1000},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}" 234 } 235 ], 236 "filterKeys": [ 237 { 238 "key": "Business Service", 239 "column": "Business Service" 240 } 241 ], 242 "postAggregationTheory": "repsonseToDifferenceOfDates", 243 "chartType": "table", 244 "valueType": "number", 245 "drillChart": "totalmcBoundaryDrillDown", 246 "documentType": "_doc", 247 "action": "", 248 "plotLabel": "Business Service", 249 "aggregationPaths": [ 250 "Total Collection", 251 "Transactions", 252 "Target Collection" 253 ], 254 "pathDataTypeMapping": [ 255 { 256 "Total Collection": "amount" 257 }, 258 { 259 "Transactions": "number" 260 }, 261 { 262 "Target Collection": "amount" 263 } 264 ], 265 "insight": {}, 266 "_comment": "" 267 }, 268 269 "totalmcBoundaryDrillDown": { 270 "chartName": "DSS_MC_DEMAND_COLLECTION_BOUNDARYDDR", 271 "queries": [ 272 { 273 "module": "MC", 274 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 275 "dateRefField": "dataObject.paymentDetails.receiptDate", 276 "indexName": "dss-collection_v2", 277 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Business Service \":{\"terms\":{\"field\":\"dataObject.paymentDetails.businessService.keyword\",\"size\":200,\"order\":{\"Total Collection\":\"desc\"}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}}}" 278 } 279 ], 280 "postAggregationTheory": "repsonseToDifferenceOfDates", 281 "filterKeys": [ 282 {"key": "businessService", "column": "Business Service"} 283 ], 284 "chartType": "xtable", 285 "valueType": "number", 286 "drillChart": "none", 287 "documentType": "_doc", 288 "plotLabel": "Boundary", 289 "action": "", 290 291 "aggregationPaths": [ 292 "Total Collection", 293 "Transactions" 294 ], 295 "pathDataTypeMapping": [ 296 { 297 "Total Collection": "amount" 298 }, 299 { 300 "Transactions": "number" 301 } 302 ], 303 "insight": {}, 304 "_comment": "" 305 }, 306 "mcCollectionByStatus":{ 307 "chartName": "DSS_MC_COLLECTION_BY_STATUS", 308 "queries": [ 309 { 310 "module": "COMMON", 311 "requestQueryMap": "{\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\"}", 312 "dateRefField": "dataObject.paymentDetails.receiptDate", 313 "indexName": "dss-collection_v2", 314 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Payment Status\":{\"terms\":{\"field\":\"dataObject.paymentStatus.keyword\"},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 315 } 316 ], 317 "chartType": "pie", 318 "valueType": "amount", 319 "action": "", 320 "documentType": "_doc", 321 "drillChart": "none", 322 "aggregationPaths": [ 323 "Payment Status" 324 ], 325 "insight": { 326 }, 327 "_comment": " collection/amount by status" 328 }, 329 330 "mcReceiptsByStatus":{ 331 "chartName": "DSS_MC_RECEIPTS_BY_STATUS", 332 "queries": [ 333 { 334 "module": "COMMON", 335 "requestQueryMap": "{\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\"}", 336 "dateRefField": "dataObject.paymentDetails.receiptDate", 337 "indexName": "dss-collection_v2", 338 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Payment Status\":{\"terms\":{\"field\":\"dataObject.paymentStatus.keyword\"},\"aggs\":{\"Total Receipts\":{\"cardinality\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}}}}}}}}" 339 } 340 ], 341 "chartType": "pie", 342 "valueType": "number", 343 "action": "", 344 "documentType": "_doc", 345 "drillChart": "none", 346 "aggregationPaths": [ 347 "Payment Status" 348 ], 349 "insight": { 350 }, 351 "_comment": " Receipts count by status" 352 }, 353 354 "mcReceiptsByPaymentMode":{ 355 "chartName": "DSS_MC_RECEIPTS_BY_PAYMENTMODE", 356 "queries": [ 357 { 358 "module": "COMMON", 359 "requestQueryMap": "{\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\"}", 360 "dateRefField": "dataObject.paymentDetails.receiptDate", 361 "indexName": "dss-collection_v2", 362 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Payment Mode\":{\"terms\":{\"field\":\"dataObject.paymentMode.keyword\"},\"aggs\":{\"Total Receipts\":{\"cardinality\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}}}}}}}}" 363 } 364 ], 365 "chartType": "pie", 366 "valueType": "number", 367 "action": "", 368 "documentType": "_doc", 369 "drillChart": "none", 370 "aggregationPaths": [ 371 "Payment Mode" 372 ], 373 "insight": { 374 }, 375 "_comment": " Receipts count by payment mode" 376 }, 377 378 "mcMonthlyCollectionReport": { 379 "chartName": "DSS_MC_MONTHLY_REPORT", 380 "queries": [ 381 { 382 "module": "COMMON", 383 "dateRefField": "dataObject.paymentDetails.receiptDate", 384 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.Bill.billDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\" }", 385 "indexName": "dss-collection_v2", 386 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"month\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}},\"Receipts\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"month\"},\"aggs\":{\"Total Receipts\":{\"cardinality\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}}}} }}}}" 387 } 388 ], 389 "chartType": "line", 390 "valueType": "amount", 391 "action": "", 392 "drillChart": "none", 393 "documentType": "_doc", 394 "aggregationPaths": [ 395 "Collections", 396 "Receipts" 397 ], 398 "pathDataTypeMapping": [ 399 { 400 "Collections": "amount" 401 }, 402 { 403 "Receipts": "number" 404 } 405 ], 406 "isCumulative": false, 407 "interval": "month", 408 "insight": { 409 }, 410 "_comment": " " 411 }, 412 413 "mcChallanCountByStatus": { 414 "chartName": "DSS_MC_CHALLAN_COUNT_BY_STATUS", 415 "queries": [ 416 { 417 "module": "CHALLAN", 418 "dateRefField": "Data.taxPeriodFrom", 419 "requestQueryMap": "{\"module\" : \"Data.businessService\", \"tenantId\" : \"Data.tenantId\"}", 420 "indexName": "echallan-services", 421 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Status\":{\"terms\":{\"field\":\"Data.applicationStatus.keyword\"},\"aggs\":{\"Challan Count\":{\"cardinality\":{\"field\":\"Data.challanNo.keyword\"}}}}}}}}" 422 } 423 ], 424 "chartType": "pie", 425 "valueType": "number", 426 "action": "", 427 "drillChart": "none", 428 "documentType": "_doc", 429 "aggregationPaths": [ 430 "Status" 431 ], 432 "insight": { 433 }, 434 "_comment": " " 435 }, 436 437 "mcTotalChallans": { 438 "chartName": "DSS_MC_TOTAL_CHALLANS", 439 "queries": [ 440 { 441 "module": "CHALLAN", 442 "dateRefField": "Data.taxPeriodFrom", 443 "requestQueryMap": "{\"module\" : \"Data.businessService\", \"tenantId\" : \"Data.tenantId\"}", 444 "indexName": "echallan-services", 445 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Challans\":{\"value_count\":{\"field\":\"Data.challanNo.keyword\"}}}}}}" 446 } 447 ], 448 "chartType": "metric", 449 "valueType": "number", 450 "drillChart": "none", 451 "documentType": "_doc", 452 "action": "", 453 "aggregationPaths": [ 454 "Total Challans" 455 ], 456 "insight": { 457 "chartResponseMap" : "mcTotalChallans", 458 "action" : "differenceOfNumbers", 459 "upwardIndicator" : "positive", 460 "downwardIndicator" : "negative", 461 "textMessage" : "$indicator$value% than last $insightInterval", 462 "colorCode" : "#228B22", 463 "insightInterval" : "year" 464 }, 465 "_comment": " " 466 }, 467 468 "mcTotalReceipts": { 469 "chartName": "DSS_MC_TOTAL_RECEIPTS", 470 "queries": [ 471 { 472 "module": "COMMON", 473 "dateRefField": "dataObject.paymentDetails.receiptDate", 474 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.Bill.billDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 475 "indexName": "dss-collection_v2", 476 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}}]}},\"aggs\":{\"Total Receipts\":{\"value_count\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}}}}}}" 477 } 478 ], 479 "chartType": "metric", 480 "valueType": "number", 481 "drillChart": "none", 482 "documentType": "_doc", 483 "action": "", 484 "aggregationPaths": [ 485 "Total Receipts" 486 ], 487 "insight": { 488 "chartResponseMap" : "mcTotalReceipts", 489 "action" : "differenceOfNumbers", 490 "upwardIndicator" : "positive", 491 "downwardIndicator" : "negative", 492 "textMessage" : "$indicator$value% than last $insightInterval", 493 "colorCode" : "#228B22", 494 "insightInterval" : "year" 495 }, 496 "_comment": " " 497 }, 498 499 "mcTotalCategories": { 500 "chartName": "DSS_MC_TOTAL_CATEGORIES", 501 "queries": [ 502 { 503 "module": "COMMON", 504 "dateRefField": "dataObject.paymentDetails.receiptDate", 505 "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.Bill.billDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.cityDistrictCode\"}", 506 "indexName": "dss-collection_v2", 507 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Total Categories\":{\"cardinality\":{\"field\":\"dataObject.paymentDetails.businessService.keyword\"}}}}}}" 508 } 509 ], 510 "chartType": "metric", 511 "valueType": "number", 512 "drillChart": "none", 513 "documentType": "_doc", 514 "action": "", 515 "aggregationPaths": [ 516 "Total Categories" 517 ], 518 "insight": { 519 520 }, 521 "_comment": " " 522 }, 523 "mcReportByDDRv2": { 524 "chartName": "DSS_MC_REPORT_BY_TENANT", 525 "queries": [ 526 { 527 "module": "COMMON", 528 "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\"}", 529 "dateRefField": "dataObject.paymentDetails.receiptDate", 530 "indexName": "dss-collection_v2", 531 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Total_Receipts\":{\"value_count\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}},\"MC_TOTAL_COLLECTION\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}" 532 }, 533 534 { 535 "module": "CHALLAN", 536 "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\"}", 537 "dateRefField": "Data.taxPeriodFrom", 538 "indexName": "echallan-services", 539 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Total_Challans\":{\"value_count\":{\"field\":\"Data.challanNo.keyword\"}}}}}}" 540 } 541 ], 542 "isMdmsEnabled": true, 543 "filterKeys": [ 544 {"key": "tenantId", "column": "DDRs"} 545 ], 546 "chartType": "xtable", 547 "drillChart": "mcReportByTenant", 548 "plotLabel": "DDRs", 549 "aggregationPaths": [ 550 "MC_TOTAL_COLLECTION", 551 "Total_Challans", 552 "Total_Receipts" 553 ], 554 "pathDataTypeMapping": [ 555 { 556 "MC_TOTAL_COLLECTION": "amount" 557 }, 558 { 559 "Total_Challans": "number" 560 }, 561 { 562 "Total_Receipts": "number" 563 } 564 ], 565 566 "insight": { 567 }, 568 "_comment": "" 569 }, 570 571 "mcReportByTenant": { 572 "chartName": "DSS_MC_REPORT_BY_TENANT", 573 "queries": [ 574 { 575 "module": "COMMON", 576 "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\"}", 577 "dateRefField": "dataObject.paymentDetails.receiptDate", 578 "indexName": "dss-collection_v2", 579 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":1000}, \"aggs\":{\"Total_Receipts\":{\"value_count\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}},\"MC_TOTAL_COLLECTION\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 580 }, 581 582 { 583 "module": "CHALLAN", 584 "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\"}", 585 "dateRefField": "Data.taxPeriodFrom", 586 "indexName": "echallan-services", 587 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Total_Challans\":{\"value_count\":{\"field\":\"Data.challanNo.keyword\"}}}}}}}}" 588 } 589 ], 590 "filterKeys": [ 591 {"key": "tenantId", "column": "ULB"} 592 ], 593 "chartType": "xtable", 594 "drillChart": "mcReportByWard", 595 "plotLabel": "ULB", 596 "aggregationPaths": [ 597 "MC_TOTAL_COLLECTION", 598 "Total_Challans", 599 "Total_Receipts" 600 ], 601 "pathDataTypeMapping": [ 602 { 603 "MC_TOTAL_COLLECTION": "amount" 604 }, 605 { 606 "Total_Challans": "number" 607 }, 608 { 609 "Total_Receipts": "number" 610 } 611 ], 612 613 "insight": { 614 }, 615 "_comment": "" 616 }, 617 618 "mcReportByWard": { 619 "chartName": "DSS_MC_REPORT_BY_WARD", 620 "queries": [ 621 { 622 "module": "COMMON", 623 "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\" , \"ward\" : \"domainObject.ward.name.keyword\" }", 624 "dateRefField": "dataObject.paymentDetails.receiptDate", 625 "indexName": "dss-collection_v2", 626 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Wards\":{\"terms\":{\"field\":\"domainObject.ward.name.keyword\",\"size\":1000}, \"aggs\":{\"Total_Receipts\":{\"value_count\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}},\"MC_TOTAL_COLLECTION\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 627 }, 628 629 { 630 "module": "CHALLAN", 631 "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"ward\" : \"Data.ward.name.keyword\" }", 632 "dateRefField": "Data.taxPeriodFrom", 633 "indexName": "echallan-services", 634 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Wards\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":1000},\"aggs\":{\"Total_Challans\":{\"value_count\":{\"field\":\"Data.challanNo.keyword\"}}}}}}}}" 635 } 636 ], 637 "filterKeys": [ 638 {"key": "ward", "column": "Wards"} 639 ], 640 "chartType": "table", 641 "drillChart": "none", 642 "plotLabel": "Wards", 643 "aggregationPaths": [ 644 "MC_TOTAL_COLLECTION", 645 "Total_Challans", 646 "Total_Receipts" 647 ], 648 "pathDataTypeMapping": [ 649 { 650 "MC_TOTAL_COLLECTION": "amount" 651 }, 652 { 653 "Total_Challans": "number" 654 }, 655 { 656 "Total_Receipts": "number" 657 } 658 ], 659 660 "insight": { 661 }, 662 "_comment": "" 663 }, 664 665 666 667 "mcReportByCategoryv2": { 668 "chartName": "DSS_PGR_STATUS_BY_CATEGORY", 669 "queries": [ 670 { 671 "module": "COMMON", 672 "requestQueryMap": "{\"departmentId\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\" , \"ward\" : \"domainObject.ward.name.keyword\" , \"region\" : \"dataObject.tenantData.city.ddrName.keyword\" }", 673 "dateRefField": "dataObject.paymentDetails.receiptDate", 674 "indexName": "dss-collection_v2", 675 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"dataObject.tenantId.keyword\":[\"pb.testing\",\"pb\"]}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"TL\",\"PT\"]}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"dataObject.paymentDetails.businessService.keyword\",\"size\":1000}, \"aggs\":{\"Total_Receipts\":{\"value_count\":{\"field\":\"dataObject.paymentDetails.receiptNumber.keyword\"}},\"MC_TOTAL_COLLECTION\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}" 676 }, 677 { 678 "module": "CHALLAN", 679 "requestQueryMap": "{\"departmentId\" : \"Data.businessService.keyword\", \"tenantId\" : \"Data.tenantId.keyword\", \"ward\" : \"Data.ward.name.keyword\" }", 680 "dateRefField": "Data.taxPeriodFrom", 681 "indexName": "echallan-services", 682 "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.businessService.keyword\":[\"TL\",\"PT\"]}}]}}, \"aggs\":{\"Department\":{\"terms\":{\"field\":\"Data.businessService.keyword\",\"size\":1000}, \"aggs\":{\"Total_Challans\":{\"value_count\":{\"field\":\"Data.challanNo.keyword\"}}}}}}}}" 683 } 684 685 ], 686 "filterKeys": [ 687 {"key": "departmentId", "column": "Department"} 688 ], 689 "chartType": "xtable", 690 "drillChart": "none", 691 692 "documentType": "_doc", 693 "action": "", 694 "plotLabel": "Department", 695 "aggregationPaths": [ 696 "MC_TOTAL_COLLECTION", 697 "Total_Challans", 698 "Total_Receipts" 699 ], 700 "pathDataTypeMapping": [ 701 { 702 "MC_TOTAL_COLLECTION": "amount" 703 }, 704 { 705 "Total_Challans": "number" 706 }, 707 { 708 "Total_Receipts": "number" 709 } 710 ], 711 "insight": { 712 }, 713 "_comment":"" 714 },`

[Click here for complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:**

Master Dashboard Configuration is the main configuration which defines as which are the Dashboards which are to be painted on screen.&#x20;

It includes all the Visualizations, their groups, the charts which comes within them and even their dimensions as what should be their height and width.

&#x20;

`1{ 2 "name": "DSS_M_COLLECT_DASHBOARD", 3 "id": "mCollect", 4 "isActive": "", 5 "style": "linear", 6 "visualizations": [ 7 { 8 "row": 1, 9 "name": "DSS_REVENUE", 10 "vizArray": [ 11 { 12 "id": 311, 13 "name": "DSS_OVERVIEW", 14 "dimensions": { 15 "height": 350, 16 "width": 5 17 }, 18 "vizType": "metric-collection", 19 "label": "DSS_OVERVIEW", 20 "noUnit": true, 21 "isCollapsible": false, 22 "charts": [ 23 { 24 "id": "mcTodaysCollection", 25 "name": "DSS_TOTAL_COLLECTION_TODAY", 26 "code": "", 27 "chartType": "metric", 28 "filter": { 29 "title": "TODAY" 30 }, 31 "headers": [] 32 }, 33 { 34 "id": "mcTotalCollection", 35 "name": "DSS_TOTAL_COLLECTION", 36 "code": "", 37 "chartType": "metric", 38 "filter": "", 39 "headers": [] 40 }, 41 { 42 "id": "mcTotalChallans", 43 "name": "DSS_MC_TOTAL_CHALLANS", 44 "code": "", 45 "chartType": "metric", 46 "filter": "", 47 "headers": [] 48 }, 49 { 50 "id": "mcTotalReceipts", 51 "name": "DSS_MC_TOTAL_RECEIPTS", 52 "code": "", 53 "chartType": "metric", 54 "filter": "", 55 "headers": [] 56 }, 57 { 58 "id": "mcTotalCategories", 59 "name": "DSS_MC_TOTAL_CATEGORIES", 60 "code": "", 61 "chartType": "metric", 62 "filter": "", 63 "headers": [] 64 } 65 ] 66 }, 67 { 68 "id": 312, 69 "name": "Total Cumulative Collection", 70 "dimensions": { 71 "height": 350, 72 "width": 7 73 }, 74 "vizType": "chart", 75 "label": "", 76 "noUnit": true, 77 "isCollapsible": false, 78 "charts": [ 79 { 80 "id": "mcCumulativeCollection", 81 "name": "Monthly", 82 "code": "", 83 "chartType": "line", 84 "filter": "", 85 "headers": [] 86 } 87 ] 88 } 89 ] 90 }, 91 { 92 "row": 2, 93 "name": "DSS_REVENUE", 94 "vizArray": [ 95 96 { 97 "id": 234, 98 "name": "DSS_MC_RECEIPTS_BY_PAYMENTMODE", 99 "dimensions": { 100 "height": 250, 101 "width": 4 102 }, 103 "vizType": "chart", 104 "noUnit": false, 105 "isCollapsible": false, 106 "charts": [ 107 { 108 "id": "mcReceiptsByPaymentMode", 109 "name": "DSS_MC_RECEIPTS_BY_PAYMENTMODE", 110 "code": "", 111 "chartType": "donut", 112 "filter": "", 113 "headers": [] 114 } 115 ] 116 }, 117 { 118 "id": 323, 119 "name": "DSS_MC_COLLECTION_BY_PAYMENT_TYPE", 120 "dimensions": { 121 "height": 250, 122 "width": 4 123 }, 124 "vizType": "chart", 125 "label": "", 126 "noUnit": false, 127 "isCollapsible": false, 128 "charts": [ 129 { 130 "id": "mcCollectionByPaymentType", 131 "name": "DSS_MC_COLLECTION_BY_PAYMENT_TYPE", 132 "code": "", 133 "chartType": "donut", 134 "filter": "", 135 "headers": [] 136 } 137 ] 138 } 139 ] 140 }, 141 { 142 "row": 3, 143 "name": "DSS_REVENUE", 144 "vizArray": [ 145 146 { 147 "id": 235, 148 "name": "DSS_MC_CHALLAN_COUNT_BY_STATUS", 149 "dimensions": { 150 "height": 250, 151 "width": 4 152 }, 153 "vizType": "chart", 154 "noUnit": false, 155 "isCollapsible": false, 156 "charts": [ 157 { 158 "id": "mcChallanCountByStatus", 159 "name": "DSS_MC_CHALLAN_COUNT_BY_STATUS", 160 "code": "", 161 "chartType": "donut", 162 "filter": "", 163 "headers": [] 164 } 165 ] 166 }, 167 { 168 "id": 233, 169 "name": "DSS_MC_RECEIPTS_BY_STATUS", 170 "dimensions": { 171 "height": 250, 172 "width": 4 173 }, 174 "vizType": "chart", 175 "noUnit": false, 176 "isCollapsible": false, 177 "charts": [ 178 { 179 "id": "mcReceiptsByStatus", 180 "name": "DSS_MC_RECEIPTS_BY_STATUS", 181 "code": "", 182 "chartType": "donut", 183 "filter": "", 184 "headers": [] 185 } 186 ] 187 }, 188 { 189 "id": 232, 190 "name": "DSS_MC_COLLECTION_BY_STATUS", 191 "dimensions": { 192 "height": 250, 193 "width": 4 194 }, 195 "vizType": "chart", 196 "noUnit": false, 197 "isCollapsible": false, 198 "charts": [ 199 { 200 "id": "mcCollectionByStatus", 201 "name": "DSS_MC_COLLECTION_BY_STATUS", 202 "code": "", 203 "chartType": "donut", 204 "filter": "", 205 "headers": [] 206 } 207 ] 208 } 209 ] 210 }, 211 212 { 213 "row": 4, 214 "name": "DSS_REVENUE", 215 "vizArray": [ 216 217 { 218 "id": 123, 219 "name": "DSS_MC_COLLECTION_CATEGORY_WISE", 220 "dimensions": { 221 "height": 250, 222 "width": 4 223 }, 224 "vizType": "chart", 225 "noUnit": false, 226 "isCollapsible": false, 227 "charts": [ 228 { 229 "id": "mcTotalCollectionCategoryWise", 230 "name": "DSS_MC_COLLECTION_CATEGORY_WISE", 231 "code": "", 232 "chartType": "horizontalBar", 233 "filter": "", 234 "headers": [] 235 } 236 ] 237 }, 238 { 239 "id": 124, 240 "name": "DSS_MC_MONTHLY_REPORT", 241 "dimensions": { 242 "height": 250, 243 "width": 4 244 }, 245 "vizType": "chart", 246 "noUnit": false, 247 "isCollapsible": false, 248 "charts": [ 249 { 250 "id": "mcMonthlyCollectionReport", 251 "name": "DSS_MC_MONTHLY_REPORT", 252 "code": "", 253 "chartType": "bar", 254 "filter": "", 255 "headers": [] 256 } 257 ] 258 } 259 ] 260 }, 261 { 262 "row": 5, 263 "name": "DSS_REVENUE", 264 "vizArray": [ 265 266 { 267 "id": 236, 268 "name": "DSS_MC_REPORT_BY_TENANT", 269 "dimensions": { 270 "height": 250, 271 "width": 4 272 }, 273 "vizType": "chart", 274 "noUnit": false, 275 "isCollapsible": false, 276 "charts": [ 277 { 278 "id": "mcReportByDDRv2", 279 "name": "DSS_MC_REPORT_BY_TENANT", 280 "code": "", 281 "chartType": "table", 282 "filter": "", 283 "headers": [], 284 "tabName": "Region" 285 }, 286 { 287 "id": "mcReportByCategoryv2", 288 "name": "DSS_MC_REPORT_BY_CATEGORY", 289 "code": "", 290 "chartType": "table", 291 "filter": "", 292 "headers": [], 293 "tabName": "Category" 294 } 295 ] 296 } 297 ] 298 } 299 ] 300 }`

[Click here for complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration:**

Master Dashboard Configuration which was explained earlier hold the list of Dashboards which are available.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration&#x20;

In this, each Role is mapped against the Dashboard which they are authorised to see.

This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client side, this configuration was just used to enable the Dashboards for viewing.&#x20;

&#x20;

`1{ 2 "_comment": "Holds mapping for each role with and its associated dashboards", 3 "roles" : [ 4 { 5 "_comment":"This role is super role which can access all the available dashboards: [other/new roles are suppose to be added]", 6 "roleId": 6, 7 "roleName" : "Admin", 8 "isSuper" : "", 9 "orgId": "", 10 "dashboards": [ 11 12 { 13 "name": "Misc Collect", 14 "id": "mCollect" 15 } 16 ] 17 }, 18 { 19 "_comment":"This role is super role which can access all the available dashboards: [other/new roles are suppose to be added]", 20 "roleId": 7, 21 "roleName" : "Commissioner", 22 "isSuper" : "", 23 "orgId": "", 24 "dashboards": [ 25 26 { 27 "id": "ulb-mCollect" 28 } 29 ] 30 } 31 32 ] 33}`

[Click here for complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS Configuration to be added:**

_common-masters/uiCommonConstants.json_

&#x20;

`1"ws": { 2 "routePath": "/dashboard/ws", 3 "isOrigin": true 4 }, 5"ulb-ws": { 6 "routePath": "/dashboard/ulb-ws", 7 "isOrigin": true 8 }`

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonConstants.json)

roleaction.json

&#x20;

`1{ 2 "rolecode": "STADMIN", 3 "actionid": {{PlaceHolder1}}, 4 "actioncode": "", 5 "tenantId": "pb" 6 } 7 8 9 { 10 "rolecode": "STADMIN", 11 "actionid": {{PlaceHolder2}}, 12 "actioncode": "", 13 "tenantId": "pb" 14 }, 15 { 16 "rolecode": "EMPLOYEE", 17 "actionid": {{PlaceHolder2}}, 18 "actioncode": "", 19 "tenantId": "pb" 20 }, 21 { 22 "rolecode": "UC_EMP", 23 "actionid": {{PlaceHolder2}}, 24 "actioncode": "", 25 "tenantId": "pb" 26 },`

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json

&#x20;

`1{ 2 "id": {{PlaceHolder1}}, 3 "name": "Dashboard mCollect", 4 "url": "/dashboard-analytics/dashboard/getDashboardConfig/mCollect", 5 "parentModule": "", 6 "displayName": "DSS", 7 "orderNumber": 0, 8 "enabled": false, 9 "serviceCode": "DSS", 10 "code": "null", 11 "path": "" 12}, 13{ 14 "id": {{PlaceHolder2}}, 15 "name": "Dashboard mCollect", 16 "url": "url", 17 "displayName": "mCollect", 18 "orderNumber": 11, 19 "parentModule": "dss-dashboard", 20 "enabled": true, 21 "serviceCode": "DSS", 22 "code": "null", 23 "path": "Dashboard.Mcollect", 24 "navigationURL": "/digit-ui/employee/dss/dashboard/mCollect", 25 "leftIcon": "places:business-center", 26 "rightIcon": "" 27}, 28{ 29 "id": {{PlaceHolder3}}, 30 "name": "DSS Dashboard Charts", 31 "url": "/dashboard-analytics/dashboard/getChartV2", 32 "parentModule": "", 33 "displayName": "DSS", 34 "orderNumber": 0, 35 "enabled": false, 36 "serviceCode": "DSS", 37 "code": "null", 38 "path": "" 39}`

[Click here for complete configurations](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

mCollect-DSS Consists of multiple graphs which represent the data of W\&S. Each graph has its own configuration which will describe the chart and its type.

DSS Consists of following charts in mCollect:

* Overview
* Total Cumulative Collection
* Receipts by Payment Mode
* Collection By Payment Mode
* Challan Count by Status
* Receipts Count By Status
* Collection By Status
* Top Categories Collections
* Monthly Collections
* Collection Report

**Overview:**

Overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection :** This represents the today’s collection amount for mCollect
* &#x20;**Total Collection :** This represents the total collection amount for mCollect
* **Total Challans** : This represents the total number of challans created.
* **Total Receipts** : This represents the total number of receipts.
* **Total Categories** : Number of categories against which miscellaneous collections have been made.

![](blob:https://digit-discuss.atlassian.net/e3e29f37-b0d4-41b2-98ef-a6ee968c6aeb#media-blob-url=true\&id=8183764e-4d61-4858-8577-ca8a802d4c63\&collection=contentId-2064547843\&contextId=2064547843\&height=521\&width=527\&alt=)

#### **Total Cumulative Collection:** <a href="#total-cumulative-collection" id="total-cumulative-collection"></a>

This Graph contains the mCollect collection amount information in the monthly base as a cumulative line graph. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](blob:https://digit-discuss.atlassian.net/0652cd63-9f48-4588-a91a-c008677d018e#media-blob-url=true\&id=4c0ab18f-6db2-4d8e-8fac-54a0334b991e\&collection=contentId-2064547843\&contextId=2064547843\&height=494\&width=1043\&alt=)

#### **Receipts by Payment Mode** <a href="#receipts-by-payment-mode" id="receipts-by-payment-mode"></a>

This graph represents the number of receipts according to the payment mode used.

![](blob:https://digit-discuss.atlassian.net/62a26b71-2bbd-4b7d-9a66-0d9b76743656#media-blob-url=true\&id=b78efc32-4693-4a22-b8be-6a5c1879c019\&collection=contentId-2064547843\&contextId=2064547843\&height=448\&width=796\&alt=)

**Collection by Payment Mode**

This graph represents the total collection according to the payment mode used.

![](blob:https://digit-discuss.atlassian.net/c0edfb33-05f7-4912-9314-e4920cdae5ec#media-blob-url=true\&id=85cab412-aa56-462b-8d2e-b196525414b9\&collection=contentId-2064547843\&contextId=2064547843\&height=449\&width=779\&alt=)

**Challan Count By Status**

This graph shows the total number of challans according to status

![](blob:https://digit-discuss.atlassian.net/9456652b-16d8-40ec-a8b9-dfa781737727#media-blob-url=true\&id=62fcb02e-641c-46ce-9aa3-8930d54ba278\&collection=contentId-2064547843\&contextId=2064547843\&height=466\&width=530\&alt=)

**Receipts Count by Status**

This graph shows the total number of receipts according to status

![](blob:https://digit-discuss.atlassian.net/0b870e06-5b9f-436f-960d-7d8d0b06fd6a#media-blob-url=true\&id=a8f9ff39-5664-465c-b9b4-750dc0127d8f\&collection=contentId-2064547843\&contextId=2064547843\&height=404\&width=502\&alt=)

**Collection by Status**

This graph shows the total collection according to status

![](blob:https://digit-discuss.atlassian.net/a3305863-77e9-4221-b48d-d3e8243f0a04#media-blob-url=true\&id=fbf5666c-88bb-4bc6-b253-33ef4bfc3736\&collection=contentId-2064547843\&contextId=2064547843\&height=480\&width=520\&alt=)

**Top Categories Collection**

This graph shows the category wise collection for all the categories in a descending order.

![](blob:https://digit-discuss.atlassian.net/e8667127-76a2-4e62-b583-097f534ae40f#media-blob-url=true\&id=315c9b1e-c8f4-4517-a0cb-4d9f8df1bd5f\&collection=contentId-2064547843\&contextId=2064547843\&height=436\&width=792\&alt=)

**Monthly Collections**

This shows the monthly break-up of total collections and total number of receipts.

![](blob:https://digit-discuss.atlassian.net/cf69d879-fa12-46b6-a30b-8559eead7002#media-blob-url=true\&id=835e56c1-b5a7-4f49-bc3f-c14900e9c4d0\&collection=contentId-2064547843\&contextId=2064547843\&height=466\&width=795\&alt=)

#### **Collection Report:** <a href="#collection-report" id="collection-report"></a>

This tabular chart representation graph shows multiple mCollect information like Total Challans, Total Collection and total number of receipts. And this table shows the data in district level and also has the drill down chart for each district to ulb and from ulb to ward level data for the same.

_**xtable**_ type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

![](blob:https://digit-discuss.atlassian.net/66653452-7b68-43a9-8011-64037866a4ce#media-blob-url=true\&id=ffe778e8-503f-4843-986a-1e708a3281e3\&collection=contentId-2064547843\&contextId=2064547843\&height=614\&width=1625\&alt=)

On click of any district name will enter into drill down charts, which will represents that specific District data.

![](blob:https://digit-discuss.atlassian.net/fd0bdf03-95d1-45c8-8f12-1cfaed3ffb2f#media-blob-url=true\&id=4e6c81c7-b6e8-48c8-8578-90bff83dd0a8\&collection=contentId-2064547843\&contextId=2064547843\&height=420\&width=1627\&alt=)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](blob:https://digit-discuss.atlassian.net/601e6403-8b19-4ed8-a862-321f9cd13d43#media-blob-url=true\&id=c16b74ac-ccbc-4ec6-8a3e-afb5ed9c02ce\&collection=contentId-2064547843\&contextId=2064547843\&height=449\&width=1603\&alt=)

#### Common Properties available: <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest) :** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName :** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by Client Side.

**queries :** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module :** The module / domain level, on which the query should be applied on.

**queries.indexName :** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery :** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap :** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField :** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

&#x20;

**chartType :** As there are different types of visualizations, this field defines what is the type of chart / visualization that this data should be used to represent.&#x20;

**Chart types available are**:

**metric** - this represents the aggregated amount/value for records filter by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance wise.

**table** - represents a form of plots and value with headers as grouped on and list of its key, values pairs.&#x20;

**xtable -** represents a advanced feature of table, it has addition capabilities for dynamic adding header values.

&#x20;

**valueType :** In any case of data, the values which are sent to plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from amount from percentage, this field is used to indicate the type of value that this Visualization will be sending.

&#x20;

**action :** Some of the visualizations are not just aggregation on data source. There might be some cases where we have to do a post aggregation computation.

**documentType :** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart :** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill downs.

**aggregationPaths :** All the queries will be having Aggregation names in it. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in it.

**insights :** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment :** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;
