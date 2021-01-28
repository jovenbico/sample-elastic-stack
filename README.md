# Elastic Stack 
## Deploy a Multi-Node Elasticsearch Cluster
### 1. Install Elasticsearch with Debian Package on each node.

Import the Elastic GPG key
```
$ wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

Installing form the APT repository
```
$ sudo apt-get install apt-transport-https
$ echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
```

Install Elasticsearch:
```
$ sudo apt-get update && sudo apt-get install elasticsearch
```

Configure Elasticsearch to start on system boot:
```
$ sudo /bin/systemctl daemon-reload
$ sudo /bin/systemctl enable elasticsearch.service
```

### 2. Configure each node's elasticsearch.yml
```
$ sudo vim /etc/elasticsearch/elasticsearch.yml
```

Change the following line on elastic-master-1:
```
cluster.name: cluster-1
node.name: master-1
network.host: [_local_, _site_]
discovery.seed_hosts: ["172.16.2.10"] # elastic-master-1 private IP
cluster.initial_master_nodes: ["master-1"]
# add lines below
node.master: true
node.data: false
node.ingest: false
node.ml: false
```

Change the following line on elastic-data-1:
```
cluster.name: cluster-1
node.name: data-1
network.host: [_local_, _site_]
discovery.seed_hosts: ["172.16.2.10"] # elastic-master-1 private IP
cluster.initial_master_nodes: ["master-1"]
node.attr.temp: hot
# add lines below
node.master: false
node.data: true
node.ingest: true
node.ml: false
```

Change the following line on elastic-data-2:
```
cluster.name: cluster-1
node.name: data-2
network.host: [_local_, _site_]
discovery.seed_hosts: ["172.16.2.10"] # elastic-master-1 private IP
cluster.initial_master_nodes: ["master-1"]
node.attr.temp: warm
# add lines below
node.master: false
node.data: true
node.ingest: true
node.ml: false
```

### 3. Configure the heap of each node
```
$ sudo vim /etc/elasticsearch/jvm.options
```

Change the following line on elastic-master-1:
```
-Xms768m
-Xmx768m
```

Change the following line on elastic-data-1 and data-2:
```
-Xms2g
-Xmx2g
```

### 4. Start Elasticsearch on each node
```
$ sudo systemctl start elasticsearch
## Check the startup process:
$ sudo tail -f /var/log/elasticsearch/cluster-1.log
## Check the node configuration:
$ curl localhost:9200/_cat/nodes?v
```
