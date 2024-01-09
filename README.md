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
