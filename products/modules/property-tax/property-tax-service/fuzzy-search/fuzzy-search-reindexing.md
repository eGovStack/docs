# Fuzzy Search Reindexing

**Step 1**

Get the current mapping of the pt index using the \_mapping API

```
GET /property-services/_mapping
```

**Step 2**

Add the following json mappings in the existing mappings (parallel to properties key):

```
"_source": {
        "excludes": [
          "Data.street",
          "Data.doorNo",
          "Data.ownerNames"
        ]
      }
```

Sample QA final mapping for reference is attached at the end.

**Step 3**

Recreate property-services-enriched with the new mapping.

**Step 4**

Update the indexer configuration, add the following 3 fields `ownerNames`, `doorNo`, `street` in custom mapping as added below in sample configuration:

[https://github.com/egovernments/configs/blob/qa/egov-indexer/property-services.yml](https://github.com/egovernments/configs/blob/qa/egov-indexer/property-services.yml)

_\*\* If search has to be enabled only on names of only ACTIVE user, configure indexer jsonPath accordingly. Use_ `$.owners[*][?(@.status=='ACTIVE')].name` _instead in the config_

**Step 5**

Restart indexer

**Step 6**

Trigger reindexing

#### Steps followed for Reindexing on QA env <a href="#steps-followed-for-reindexing-on-qa-env" id="steps-followed-for-reindexing-on-qa-env"></a>

1. Recreated property-services-enriched index with the new mapping
2. Created kafka connector
3. Hit the legacy index api
4. Once data is indexed in property-services-enriched, verify that all the data is indexed
5. After validating the data, drop the property-services index and use alias to point `property-services` to `property-services-enriched`

```
POST /_aliases
{
  "actions": [
    {
      "add": {
        "index": "property-services-enriched",
        "alias": "property-services"
      }
    }
  ]
}
```

Sample mappings from QA env:

```
{
  "mappings": {
    "general": {
      "_source": {
        "excludes": [
          "Data.street",
          "Data.doorNo",
          "Data.ownerNames"
        ]
      },
      "properties" : {
          "Data" : {
            "properties" : {
              "@timestamp" : {
                "type" : "date"
              },
              "accountId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "acknowldgementNumber" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "auditDetails" : {
                "properties" : {
                  "createdBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "createdTime" : {
                    "type" : "long"
                  },
                  "lastModifiedBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "lastModifiedTime" : {
                    "type" : "long"
                  }
                }
              },
              "channel" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "creationReason" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "history" : {
                "properties" : {
                  "action" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "assigner" : {
                    "properties" : {
                      "emailId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "id" : {
                        "type" : "long"
                      },
                      "mobileNumber" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "roles" : {
                        "properties" : {
                          "code" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "tenantId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "type" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "userName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "assignes" : {
                    "properties" : {
                      "emailId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "id" : {
                        "type" : "long"
                      },
                      "mobileNumber" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "roles" : {
                        "properties" : {
                          "code" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "tenantId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "type" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "userName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "auditDetails" : {
                    "properties" : {
                      "createdBy" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "createdTime" : {
                        "type" : "long"
                      },
                      "lastModifiedBy" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "lastModifiedTime" : {
                        "type" : "long"
                      }
                    }
                  },
                  "businessId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "businessService" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "businesssServiceSla" : {
                    "type" : "long"
                  },
                  "comment" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "documents" : {
                    "properties" : {
                      "auditDetails" : {
                        "properties" : {
                          "createdBy" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "createdTime" : {
                            "type" : "long"
                          },
                          "lastModifiedBy" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "lastModifiedTime" : {
                            "type" : "long"
                          }
                        }
                      },
                      "documentType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "fileStoreId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "id" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "id" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "moduleName" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "nextActions" : {
                    "properties" : {
                      "action" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "currentState" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "nextState" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "roles" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "previousStatus" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "rating" : {
                    "type" : "long"
                  },
                  "state" : {
                    "properties" : {
                      "actions" : {
                        "properties" : {
                          "action" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "currentState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "nextState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "roles" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "tenantId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "uuid" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          }
                        }
                      },
                      "applicationStatus" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "businessServiceId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "docUploadRequired" : {
                        "type" : "boolean"
                      },
                      "isStartState" : {
                        "type" : "boolean"
                      },
                      "isTerminateState" : {
                        "type" : "boolean"
                      },
                      "sla" : {
                        "type" : "long"
                      },
                      "state" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "stateSla" : {
                    "type" : "long"
                  },
                  "tenantId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "id" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "landArea" : {
                "type" : "long"
              },
              "noOfFloors" : {
                "type" : "long"
              },
              "oldPropertyId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "owners" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "ownershipCategory" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "propertyId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "propertyType" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "source" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "status" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "superBuiltUpArea" : {
                "type" : "long"
              },
              "tenantData" : {
                "properties" : {
                  "OfficeTimings" : {
                    "properties" : {
                      "Mon - Fri" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "Sat" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "address" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "city" : {
                    "properties" : {
                      "code" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "ddrName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtTenantCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "latitude" : {
                        "type" : "float"
                      },
                      "localName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "longitude" : {
                        "type" : "float"
                      },
                      "municipalityName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "regionCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "regionName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "ulbGrade" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  },
                  "code" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "contactNumber" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "description" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "domainUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "emailId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "facebookUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "helpLineNumber" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "imageId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "logoId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "name" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "pdfContactDetails" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "pdfHeader" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "pincode" : {
                    "type" : "long"
                  },
                  "twitterUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "type" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "tenantId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "units" : {
                "properties" : {
                  "active" : {
                    "type" : "boolean"
                  },
                  "arv" : {
                    "type" : "long"
                  },
                  "constructionDetail" : {
                    "properties" : {
                      "builtUpArea" : {
                        "type" : "float"
                      },
                      "carpetArea" : {
                        "type" : "long"
                      },
                      "constructionDate" : {
                        "type" : "long"
                      },
                      "constructionType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "plinthArea" : {
                        "type" : "long"
                      },
                      "superBuiltUpArea" : {
                        "type" : "long"
                      }
                    }
                  },
                  "floorNo" : {
                    "type" : "long"
                  },
                  "id" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "occupancyDate" : {
                    "type" : "long"
                  },
                  "occupancyType" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "tenantId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "unitType" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "usageCategory" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "usageCategory" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "ward" : {
                "properties" : {
                  "boundaryNum" : {
                    "type" : "long"
                  },
                  "children" : {
                    "properties" : {
                      "area" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "boundaryNum" : {
                        "type" : "long"
                      },
                      "code" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "label" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "pincode" : {
                        "type" : "long"
                      }
                    }
                  },
                  "code" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "label" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "name" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "workflow" : {
                "properties" : {
                  "action" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "assignes" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "state" : {
                    "properties" : {
                      "actions" : {
                        "properties" : {
                          "action" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "auditDetails" : {
                            "properties" : {
                              "createdBy" : {
                                "type" : "text",
                                "fields" : {
                                  "keyword" : {
                                    "type" : "keyword",
                                    "ignore_above" : 256
                                  }
                                }
                              },
                              "createdTime" : {
                                "type" : "long"
                              },
                              "lastModifiedBy" : {
                                "type" : "text",
                                "fields" : {
                                  "keyword" : {
                                    "type" : "keyword",
                                    "ignore_above" : 256
                                  }
                                }
                              },
                              "lastModifiedTime" : {
                                "type" : "long"
                              }
                            }
                          },
                          "currentState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "nextState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "roles" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "tenantId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "uuid" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          }
                        }
                      },
                      "applicationStatus" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "auditDetails" : {
                        "properties" : {
                          "createdBy" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "createdTime" : {
                            "type" : "long"
                          },
                          "lastModifiedBy" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "lastModifiedTime" : {
                            "type" : "long"
                          }
                        }
                      },
                      "businessServiceId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "docUploadRequired" : {
                        "type" : "boolean"
                      },
                      "isStartState" : {
                        "type" : "boolean"
                      },
                      "isStateUpdatable" : {
                        "type" : "boolean"
                      },
                      "isTerminateState" : {
                        "type" : "boolean"
                      },
                      "sla" : {
                        "type" : "long"
                      },
                      "state" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "tenantId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
    }
  }
}
```
