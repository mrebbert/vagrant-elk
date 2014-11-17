vagrant-elk
===========

A Vagrant-based Environment for Logstash, Elasticsearch, Redis and Kibana with Ansible as Provisioner.

## Description

The primary goal of this smart project is to verify the configuration of a loganalytic environment based on the popular Elasticsearch ELK Stack (Elasticsearch, Logstash, Kibana as frontend and Redis) and to get an enviroment to verify new logstash configurations for logfile parsings in nearly production enviroments.
The project includes a box (named as log-client) which act as a typical log client. Therein it has a logstash installed which act as log parser and shipper. Therfor it parses (actually only) /var/log/messages and transfers the log statements to the Redis instance on the logserver which is the log queue.

The second box (named as log-server) includes the redis installation as queue, a logstash instance as indexer, an elasticsearch instance and a kibana installation served by an apache webserver as frontend.
The indexer grabs the statements from the queue and writes it to the elasticsearch index. To maintain the elasticsearch index, curator is additionally installed.

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
``:
```
for i in $(seq 1 1000) ; do 
	logger "This is a test for logstash." ; 
done
```

##Components
### Log-Server
#### Kibana
_to be done_
#### Elasticsearch
_to be done_
#### Logstash (Indexer)
_to be done_
#### Redis
_to be done_
#### Curator
_to be done_

### Log-Client
#### Logstash (Shipper)
_to be done_

##Ansible
### group_vars
_to be done_
### host_vars
_to be done_
### roles
_to be done_
#### common		
#### httpd
#### kibana
#### redis
#### curator
#### indexer	
#### logstash
#### shipper
#### elasticsearch
#### java	
#### queue
#### store
