The  Intra-domain  Security  module  receives  network  traffic  data  as  input  and  produces  network events  and  alerts  about  potential  failures  or  security  threats. 

The solution integrates existing open-source tools and build on best practices from state of the practice to enforce intra-domain security, thus indirectly contributing to the 5GZORRO security story-line by shielding the intra-domain trust .

A Zeek platform is employed as a network security monitoring tool. 
The platform monitors various virtual TAPS and produce live (real-time) traffic data which are then aggregated and analysed within Elasticsearch platform. Finally data is send to Kibana for visualization.

![](https://github.com/almpertoerspamer/intrasecurity_test/blob/main/architecture.png)

# Deployment steps:
```
$ docker pull blacktop/zeek
$ docker pull blacktop/zeek:elastic
```
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
**# Add your pcap file inside pcap folder**

**# Change the corresponding name inside docker-compose.elastic.yml at zeek->command domain.

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


