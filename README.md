vagrant-elk
===========

A Vagrant-based Environment for Logstash, Elasticsearch, Redis and Kibana with Ansible as Provisioner.

Start
-----
'vagrant up' starts two machines: log-server and log-client.

The log-server includes the Log-Indexer with Logstash and Elasticsearch, a Redis Instance for Queueing and Kibana configured on an Apache-Webserver.

The log-client is configured as Log-Shipper based on an Logstash Installation. It writes the Log-Data to the Redis-Instance at the log-server.

For example, the Syslog-File (/var/log/messages) is configured.

The Kibana-Frontend is reachable at the URL https://192.168.2.120.
The credentials are logger/logger.

---to be continued---


