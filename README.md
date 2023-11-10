# ELKPi
ELK Stack on Raspberry Pi 4 8GB Homelab project

For this project, I'm creating an ELK Instance on a Raspberry Pi 4 as a home SIEM to monitor my network, endpoints, and network traffic. 

Following this article for a majority of the setup

https://logz.io/blog/elk-stack-raspberry-pi/

11/08/2023 

Initially, I tried using a Raspberry Pi OS distro for the project but found issues trying to install Elasticsearch.
I've since created a new instance with Ubuntu 22.04

11/09/2023

After setting up SSH to my Raspberry Pi for Headless operation, I've continued with my plan to get my elasticstack install completed

After initial download and configuration, I've run into an error with starting the service 

After running "systemctl start elasticsearch.service"

The Service fails to run, and displays Exit Code 1. 

After looking through the Elastic Log file, the Error is 

 fatal exception while booting Elasticsearch
java.lang.IllegalArgumentException: setting [cluster.initial_master_nodes] is not allowed when [discovery.type] is set to [single-node]

After commenting out that line, the service runs! Time to continue with trying to get everything running

New problem, when I try to Curl the service to test connectivity, it shows

{"error":{"root_cause":[{"type":"security_exception","reason":"unable to authenticate user [gav] for REST request [/]","header":{"WWW-Authenticate":["Basic realm=\"security\" charset=\"UTF-8\"","Bearer realm=\"security\"","ApiKey"]}}],"type":"security_exception","reason":"unable to authenticate user [gav] for REST request [/]","header":{"WWW-Authenticate":["Basic realm=\"security\" charset=\"UTF-8\"","Bearer realm=\"security\"","ApiKey"]}},"status":401}

Which looks to me like the security features are enabled, causing me to need to provide credentials(Which I haven't set up yet)

Created auto-gen password with 

./bin/elasticsearch-setup-passwords -u elastic




