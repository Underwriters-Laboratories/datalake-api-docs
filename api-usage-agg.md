# Data Aggregation

The data aggregation API allow you to aggregate the data based on a search query. This example will give us the number of incidents that contains  "light" or "lights" keywords.

## `Request Body Search`
Request

```JSON
GET /ppe_cpsc_recall/_search
{
  "size": 0,
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
  },
  "aggs": {
    "data": {
      "date_histogram": {
        "field": "@timestamp",
        "calendar_interval": "year",
        "format": "yyyy",
        "min_doc_count": 0
      }
    }
  }
}
```

Response

```json
{
  "took": 1,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 153,
      "relation": "eq"
    },
    "max_score": null,
    "hits": []
  },
  "aggregations": {
    "data": {
      "buckets": [
        {
          "key_as_string": "2015",
          "key": 1420070400000,
          "doc_count": 40
        },
        {
          "key_as_string": "2016",
          "key": 1451606400000,
          "doc_count": 37
        },
        {
          "key_as_string": "2017",
          "key": 1483228800000,
          "doc_count": 29
        },
        {
          "key_as_string": "2018",
          "key": 1514764800000,
          "doc_count": 29
        },
        {
          "key_as_string": "2019",
          "key": 1546300800000,
          "doc_count": 18
        }
      ]
    }
  }
}
```

### `Data Aggregation By Terms`

We also can aggregate the data by terms. Here is an example:

```json
GET /ppe_cpsc_recall/_search
{
  "size": 0,
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
              "gte": "2010-01-01"
            }
          }
        }
      ]
    }
  },
  "aggs": {
    "data": {
        "terms": {
          "field": "RemedyOptions.Option.keyword"
        }
    }
  }
}
```

Reponse

```json
{
  "took" : 3,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 310,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "data" : {
      "doc_count_error_upper_bound" : 0,
      "sum_other_doc_count" : 0,
      "buckets" : [
        {
          "key" : "Refund",
          "doc_count" : 145
        },
        {
          "key" : "Replace",
          "doc_count" : 93
        },
        {
          "key" : "Repair",
          "doc_count" : 82
        },
        {
          "key" : "New Instructions",
          "doc_count" : 3
        },
        {
          "key" : "Dispose",
          "doc_count" : 2
        }
      ]
    }
  }
```

For more information:

- Aggregations https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html
- Date Histogram Aggregation https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-datehistogram-aggregation.html#search-aggregations-bucket-datehistogram-aggregation
