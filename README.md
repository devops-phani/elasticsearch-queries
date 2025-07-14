# elasticsearch-queries

```
GET _cat/indices?v
```

```
GET _cat/shards?v
```

```
POST /_cluster/reroute 
{
    "commands": [
        {
            "move": {
                "index": "logstash-default-2024.01.07",
                "shard": 0,
                "from_node": "node1",
                "to_node": "node2"
            }
        }
    ]
}
```

```
GET _cluster/allocation/explain
```

```
GET /_nodes
```

```
PUT _cluster/settings
{
  "persistent": {
    "cluster.routing.allocation.enable": "all"
  }
}
```


```
GET _cat/nodes?v
```

```
GET /_cat/health
```

```
POST _flush/synced
```

```
PUT _cluster/settings
{
  "transient" : {
    "cluster.routing.allocation.exclude._ip" : "10.244.68.63"
  }
}
```

```
GET _cat/recovery?v&active_only=true
```

```
PUT _settings
{
  "index" : {
    "number_of_replicas" : 0
  }
}
```

```
PUT logstash-default-2024.01.08/_settings
{
  "index.routing.allocation.include._name": "node2"
}
```

```
POST _cluster/reroute?retry_failed
```

```
POST /_reindex
{
  "source": {
    "index": "logstash-2022.11.15"
  },
  "dest": {
    "index": "new-2022-nov-15"
  }
}
```

List indexes using curl

```
curl -k https://username:password@localhost:9200/_cat/indices?v
```
or

```
curl -k -u elastic:$ELASTIC_PASSWORD https://localhost:9200/_cat/indices?v
```

Delete multiple indexes using curl

Reference:

https://opster.com/guides/elasticsearch/operations/deleting-elasticsearch-indices-using-curl/

```
curl -k -X DELETE "https://username:password@localhost:9200/index1,index2"
```

or

```
curl -k -X DELETE -u elastic:$ELASTIC_PASSWORD "https:/localhost:9200/index1,index2"
```

Change the replicas using curl command

```
curl -k -XPUT 'https://user:password@localhost:9200/_settings' -H "Content-Type: application/json" -d '
{ "index" : { "number_of_replicas" : 0 } }'
```

or

```
curl -k -XPUT -u elastic:$ELASTIC_PASSWORD 'https://localhost:9200/_settings' -H "Content-Type: application/json" -d '
{ "index" : { "number_of_replicas" : 0 } }'
```

List the users

```
curl -k -X GET "https://user:password@localhost:9200/_security/user?pretty"
```

or

```
curl -k -X GET -u -u elastic:$ELASTIC_PASSWORD "https://localhost:9200/_security/user?pretty"
```

Here's a curl command to increase the parent circuit breaker limit in Elasticsearch using the _cluster/settings API:

```
curl -k -u elastic:$ELASTIC_PASSWORD https://localhost:9200/_cluster/settings -X PUT -H "Content-Type: application/json" -d '
{
  "persistent": {
    "indices.breaker.total.limit": "98%"
  }
}'
```

If you want the change to be temporary (until the next restart), use transient:

```
curl -k -u elastic:$ELASTIC_PASSWORD https://localhost:9200/_cluster/settings -X PUT -H "Content-Type: application/json" -d '
{
  "transient": {
    "indices.breaker.total.limit": "98%"
  }
}'
```
