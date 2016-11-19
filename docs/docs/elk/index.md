### Health

```sh
curl -XGET http://localhost:9200/_cluster/health?pretty

```

### Shards

```sh
curl -XGET http://localhost:9200/_cat/shards

```

### Reroute shards

```sh
for shard in $(curl -XGET http://localhost:9200/_cat/shards | grep UNASSIGNED | awk '{print $2}'); do
    curl -XPOST 'localhost:9200/_cluster/reroute' -d '{
        "commands" : [ {
              "allocate" : {
                  "index" : "t37", 
                  "shard" : $shard, 
                  "node" : "datanode15", 
                  "allow_primary" : true
              }
            }
        ]
    }'
    sleep 5
done

NODE="YOUR NODE NAME"
IFS=$'\n'
for line in $(curl -s 'localhost:9200/_cat/shards' | fgrep UNASSIGNED); do
  INDEX=$(echo $line | (awk '{print $1}'))
  SHARD=$(echo $line | (awk '{print $2}'))

  curl -XPOST 'localhost:9200/_cluster/reroute' -d '{
     "commands": [
        {
            "allocate": {
                "index": "'$INDEX'",
                "shard": '$SHARD',
                "node": "'$NODE'",
                "allow_primary": true
          }
        }
    ]
  }'
done
```

### Delete index

```sh
curl -XDELETE 'http://localhost:9200/twitter/'
```

```sh
rm size.tmp
for i in {1..6};do ssh prod-elk$i.kyc.megafon.ru "du -sch /var/lib/elasticsearch/prod-elk/nodes/0/indices/*" >> size.tmp;done
cat size.tmp | gsort -h
```

GET /\_cat/shards

GET /\_flush/synced

GET /\_cluster/health

GET \_cluster/health?level=shards

PUT /\_cluster/settings 

{

 "transient" : {

 "cluster.routing.allocation.enable" : "all"

 }

}

put /logstash-2016.08.31/\_settings

{"index.routing.allocation.disable\_allocation": false}

# Mass index deletion
for index in $(curl -XGET esmaster:9200/_cat/indices | awk ‘/pattern/ {print $3}’); do curl -XDELETE esmaster:9200/$index?master_timeout=120s; done

# Optimize cluster -----------------------------
curl -XPUT ‘http://escluster:9200/_cluster/settings' -d ‘{
 “transient” : {
 “cluster.routing.allocation.cluster_concurrent_rebalance”: 20,
 “indices.recovery.concurrent_streams”: 20,
 “cluster.routing.allocation.node_initial_primaries_recoveries”: 20,
 “cluster.routing.allocation.node_concurrent_recoveries”: 20,
 “indices.recovery.max_bytes_per_sec”: “2048mb”,
 “cluster.routing.allocation.disk.threshold_enabled” : true,
 “cluster.routing.allocation.disk.watermark.low” : “90%”,
 “cluster.routing.allocation.disk.watermark.high” : “98%”,
 “cluster.routing.allocation.enable”: “primary”
 }
}’

# Then, once cluster become yellow
curl -XPUT ‘http://escluster:9200/_cluster/settings' -d ‘{
 “transient” : {
 “cluster.routing.allocation.enable”: “all”
 }
}’
# Optimize cluster -----------------------------

# Get info about cluster
curl -XGET https://escluster/_cat/nodes?v&h=host,r,d,hc,rc,fdc,l

# Sort by free disk space
curl -XGET https://escluster/_cat/nodes?h=host,r,d,hc,rc,fdc,l | sort -hrk 3

# Sort by heap capacity
curl -XGET https://escluster/_cat/nodes?h=host,r,d,hc,rc,fdc,l | sort -hrk 4

# Recovery information
curl -XGET https://escluster/_recovery?pretty&active_only



