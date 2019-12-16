# Elastic Stack 

## Installation  

### Import Key  

Download and install the public signing key:  

```
$ sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

### Install RPM repository  

Create a file called elasticsearch.repo in the /etc/yum.repos.d/ directory for RedHat based distributions

```
[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
#baseurl=https://artifacts.elastic.co/packages/oss-7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

### Install  ELK  
```
sudo yum install elasticsearch
sudo yum install logstash
sudo yum install kibana
```

### Start services  
```
sudo service elasticsearch start
sudo service logstash start
sudo service kibana start
```
### Open firewall
https://www.thegeekdiary.com/how-to-open-a-ports-in-centos-rhel-7/  
```
sudo firewall-cmd --zone=public --add-port=9200/tcp --permanent
sudo firewall-cmd --zone=public --add-port=5601/tcp --permanent
sudo firewall-cmd --reload
```

### Check services  
```
# elasticsearch
curl -X GET "localhost:9200/?pretty"

# kibana
curl -X GET "localhost:5601/app/kibana"
```
