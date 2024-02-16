# API Usages

Safety Data Lake uses Elasticsearch as a search engine and APIs.

## `Endpoint`

Primary
```
https://opendata.ul.org/api/es/_search
```


## `Authentication`
```
Type: Basic Auth
Username: reader
Password: reader
```

### Search all documents across several indices

General usage of the API follows the following syntax: https://opendata.ul.org/api/es/{index}/_search where {index} is the index name.

```
https://opendata.ul.org/api/es/ppe_fda_enforcement,ppe_cpsc_recall/_search
```
