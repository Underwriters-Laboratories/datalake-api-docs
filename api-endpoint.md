# API Usages

Safety Data Lake uses Elasticsearch as a search engine and APIs.

## `Endpoint`

```
https://opendata.ul.org/api/es/_search
```

## `Authentication`
```
Username: reader
Password: reader
```
```
Type: Basic Auth
example: https://reader:reader@opendata.ul.org/api/es/_search
```

### Search all documents across several indices

General usage of the API follows the following syntax: https://opendata.ul.org/api/es/{index}/_search where {index} is the index name.

```
https://opendata.ul.org/api/es/ppe_eu_rapex,ppe_cpsc_recall/_search
```
