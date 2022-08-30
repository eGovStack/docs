# Fuzzy Search

Procedure to integrate elastic search for Fuzzy search with any of the eGov modules.

**Creating the index as per the requirement**

1. The elastic index has to be used for fuzzy search due to performance enhancement and when PII fields are involved which cannot be accessed in DB directly to apply fuzzy logic.
2. When PII data are involved those fields shouldn’t be returned by the elastic search but only can be used to apply the filter. To enable this that particular field should be indexed but not stored.

eg -

```
{
  "mappings": {
    "general": {
      "_source": {
        "excludes": [
          "name"
        ]
      },
      "properties": {
        "id": {
          "type": "text"
        },
        "dob": {
          "type": "date"
        },
        "name": {
          "type": "text"
        }
      }
    }
  }
}
```

In the above example, when data is posted, all the fields will be stored, but the index will never return the excluded source fields when searched.

**Querying an index**

```
curl --location --request GET 'localhost:9200/_search?pretty' \

--header 'Content-Type: application/json' \
--data-raw '{
    "query": {
        "fuzzy": {
            "name": {
                "value": "ki"
            }
        }
    }
}'
```

This is a simple request, there are [additional parameters](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html) that can be used to enhance the fuzzy search.

```
curl -X GET "localhost:9200/_search?pretty" -H 'Content-Type: application/json' -d'
{
  "query": {
    "fuzzy": {
      "name": {
        "value": "ki",
        "fuzziness": "AUTO",
        "max_expansions": 50,
        "prefix_length": 0,
        "transpositions": true
      }
    }
  }
}
'
```

**Elastic Integration with code**

1. Add the elasticsearch host from the eGov cluster.
2. Divide the search params between the ones that will be sent to elastic and others to DB (search to elastic should be made only if the fuzzy fields are present in search request)
3. The result of the elastic search should be only the required primary-Id of the entity(property-id, trade license-id, etc..)
4. Then the resulting ids should be used in the normal search as it is.

Please refer to the following [commit](https://github.com/egovernments/municipal-services/commit/9917276346b6a0136a9afef87c1b93e2f4ec5746) for the integration

**Application Properties**

Properties need to add for integration

```
#Elastic search properties

elasticsearch.host=http://localhost:9200/
elasticsearch.search.endpoint=/_search
property.es.index=property-services
pt.search.name.fuziness=2
pt.search.doorno.fuziness=2
pt.search.oldpropertyid.fuziness=2
pt.fuzzy.searh.is.wildcard=true
```

The indices need to be reindexed for the fuzzy search to work if changes are done in the index. particularly in the case of protected fields being indexed but not to be returned in the search.

**Reindexing for PT**: [Refer here](https://docs.google.com/document/d/1WKFB4Dbb0kmOFZBfPm5HnA290i\_CEvIinsL22V59CU4/edit)
