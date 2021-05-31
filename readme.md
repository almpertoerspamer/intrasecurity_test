
![](https://github.com/almpertoerspamer/intrasecurity_test/blob/main/architecture.png)

# Deployment steps:

docker pull blacktop/zeek
docker pull blacktop/zeek:elastic

**In a local directory clone docker-zeek.git:**
```
$ git clone --depth 1 https://github.com/blacktop/docker-zeek.git

$ cd docker-zeek
```
**Modify docker-compose.elastic.yml:**
```
change kibana enviroment:
      - xpack.reporting.enabled=true
      - xpack.security.enabled=false
```
**Add your pcap file inside pcap folder**

 change the corresponding name inside docker-compose.elastic.yml at zeek->command domain.

**Run:**
```
$ docker-compose -f docker-compose.elastic.yml up -d kibana
```
**wait 2 minutes for "kibana service" to start**
```
$ docker-compose -f docker-compose.elastic.yml up -d filebeat

$ docker-compose -f docker-compose.elastic.yml up zeek
```
**wait 2 minutes while for filebeat service to consume all the logs**

# Visualize data in Kibana 
Go to: 
http://localhost:5601/app/kibana 

From the kibana browser navigate to: Dashboards->Zeek Overview Dashboard.

In the calendar icon select a time period related to the pcap file used.

To download pcap filles go to:
https://www.netresec.com/?page=pcapfiles

To check pcaps before deployment in kibana, apackets module can be used:
https://apackets.com/upload


