# Prescriptive-data-nginx-project
 construct a system which uses a load balancer to balance traffic between any number of nginx containers, which serve a static file containing the IP addresses of all of the currently connected nginx containers.
# HAProxy load balancer for Nginx servers using Docker
Above docker file creates a nginx cluster with level 4 tcp loadbalancer HA proxy. Docker-composer will deploy 3 containers two nginx webservers and 1 loadbalancer. Each webserver has its own Dockerfile. For haproxy we are using haproxytech/haproxy-ubuntu:latest as our base image.

## Technical details:
 - Docker network subnet is: 172.16.0.0/24
 - HAProxy load balancer IP address is: 172.16.0.2
 - Nginx web server 1 IP address: 172.16.0.10
 - Nginx web server 2 IP address: 172.16.0.20

To access the HAproxy stats page, Use 81 port with HaProxy ipaddress

# Installation Steps:

Install docker-ce first then docker compose up to build and start the containers

```````bash
    docker-compose up -d
```````

# Testing
To test the loadbalancing is working or not. curl to the loadbalacer ip and check for the output
```````bash
  curl http://172.16.0.2
```````
# Benchmark

Benchmark the web servers by sending a punch of requests directly:
`````````bash
ab -n 3000 -c 20 http://172.16.0.2/
`````````
