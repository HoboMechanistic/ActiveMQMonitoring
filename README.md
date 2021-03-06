# ActiveMQMonitoring

Some simple python scripts I wrote to monitor ActiveMQ consumers and queues using jolokai.
The Nagios script should be pretty plug and play, only requires the queue URL to be passed in as an arg, which is normally in the form of:

http://<HOST>:<PORT>/api/jolokia/read/org.apache.activemq:type=Broker,brokerName=localhost,destinationName=<QUEUE_NAME>,destinationType=Queue
 
For the non-nagios script I felt fancy and use the neat python config api I just learnt about. This way we can check many queues in one script run.
Wait time in min here allows you to set the amount of time to wait between the first check and the second before doing a comparison.
Example config template:
```
 	[Queue]
 	Queue1 = http://<HOST>:<PORT>/api/jolokia/read/org.apache.activemq:type=Broker,brokerName=localhost,destinationName=<QUEUE_NAME_ONE>,destinationType=Queue
 	Queue2 = http://<HOST>:<PORT>/api/jolokia/read/org.apache.activemq:type=Broker,brokerName=localhost,destinationName=<QUEUE_NAME_TWO>,destinationType=Queue
  ...
 	[AuthUser]
 	User = username
 	Pass = password
 	[WaitTime]
        InMin = 10
``` 

The jolokaiLogStash.conf was part of a local containerized ELK stack, used as a proof of concept. It uses Kibana to visualize queue size changes from ActiveMQ over time. The conf contains the regex I used to grab the queue size from the json.
