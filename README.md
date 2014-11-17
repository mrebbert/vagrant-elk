vagrant-elk
===========

A Vagrant-based Environment for Logstash, Elasticsearch, Redis and Kibana with Ansible as Provisioner.

## Description

The primary goal of this smart project is to verify the configuration of the setup based on Logstash, Redis, Elasticsearch and Kibana as frontend and to get an enviroment to verify new logstash configurations for logfile parsings in nearly production enviroments.
The project includes a box (named as log-client) which act as a typical log client. Therein it has a logstash installed which act as log parser and shipper. Therfor it parses (actually only) /var/log/messages and transfers the log statements to the Redis instance on the logserver which is the log queue.

The second box (named as log-server) includes the redis installation as queue, a logstash instance as indexer, an elasticsearch instance and a kibana installation served by an apache webserver as frontend.
The indexer grabs the statements from the queue and writes it to the elasticsearch index.

I used to capsulate the single roles in the ansible playbook so you can use it as a quarry.

## Requirements
The only thing you need is a running ansible installation.
How to install Ansible on your system is described at the [Ansible documentation](http://docs.ansible.com/intro_installation.html).

## Quickstart

'vagrant up' starts both machines: log-server and log-client.

After the successful boot-up the Kibana-Frontend is reachable at the URL 
[https://192.168.2.120](https://192.168.2.120). <br />
The credentials are <br />
User: logger<br />
Password: logger

After accessing Kibana the first time, the elasticsearch index could be empty. To fill it up, you can force some log statements at the log client: <br />
``
vagrant ssh log-client
``
```
for i in $(seq 1 1000) ; do 
	logger "This is a test for logstash." ; 
done
```

##Components
_to be done_

##Ansible
_to be done_
