# Search APIs
Here is a basic match query that searches for the string “light” and "bulb" in all the fields. The API allows you to execute a search query and get back search hits that match the query.

## `Request Body Search`

Request

```json
GET /ppe_eu_rapex,ppe_cpsc_recall/_search
{
  "query": {
    "query_string": { "query": "light AND bulb" }
  }
}
```

Response

```json
{
  "took" : 21,
  "timed_out" : false,
  "_shards" : {
    "total" : 2,
    "successful" : 2,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 164,
      "relation" : "eq"
    },
    "max_score" : 15.494345,
    "hits" : [
      {
        "_index" : "ppe_cpsc_recall",
        "_type" : "_doc",
        "_id" : "6513",
        "_score" : 15.494345,
        "_source" : {
          "@timestamp" : "2015-09-10T00:00:00",
          "URL" : "https://www.cpsc.gov/Recalls/2015/Philips-Recalls-Halogen-Bulbs",
          "Importers" : [
            {
              "CompanyID" : "0",
              "Name" : "Philips Lighting North America Corporation, of Somerset, N.J."
            }
          ],
          "RecallDate" : "2015-09-10T00:00:00",
          "Image_list" : [
            "https://www.cpsc.gov/s3fs-public/Recall.2015.15242.1.jpg",
            "https://www.cpsc.gov/s3fs-public/Recall.2015.15242.2.jpg",
            "https://www.cpsc.gov/s3fs-public/Recall.2015.15242.3.jpg",
            "https://www.cpsc.gov/s3fs-public/Recall.2015.15242.5.jpg"
          ],
          "ManufacturerCountries" : [
            {
              "Country" : "China"
            }
          ]
          ...
          ...
        }
      }
    ]
}
```

Here is an example using boolean logics:

Request

```JSON
GET /ppe_cpsc_recall/_search
{
  "size": 5,
  "query": {
    "bool": {
      "must": [
        {
          "query_string": {
            "query": "light OR lights"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "@timestamp": {
              "gte": "2015-01-01"
            }
          }
        }
      ]
    }
  }
}
```

For more information:

- Request Search Body https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-body.html
- Query String Query https://www.elastic.co/guide/en/elasticsearch/reference/7.2/query-dsl-query-string-query.html
