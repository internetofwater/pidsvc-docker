# Persistent Identifier Service (PID Service)
This is a deployment system using docker for the PIDsvc https://www.seegrid.csiro.au/wiki/Siss/PIDService#Prerequisites

## Overview
Persistent Identifier Service (PID Service) enables resolution of persistent identifiers. The proposed solution is using an approach to intercept all incoming HTTP requests at the Apache HTTP web server level and pass it through to the PID Service dispatcher servlet that implements a logic to recognise a pattern of an incoming request and compare it with one of the patterns configured in the PID Service and stored in a persistent relational data store (e.g. PostgreSQL) and then performs a set of user-defined actions, such as, HTTP header manipulation, redirects, proxying requests, delegating resolution to another service, etc. It features extendable architecture for future improvements and supports multiple control interfaces - visual user interface (UI) as well as programmable API for remote user-less management of URI mapping rules.
Implementation has taken into account findings, requirements and observations discovered during technology review and prototype implementation phases that immediately preceded implementation of the PID Service:
https://www.seegrid.csiro.au/wiki/bin/view/SISS4BoM/PIDTechnologyReview
https://www.seegrid.csiro.au/wiki/bin/view/SISS4BoM/PIDPrototypeSolution

![Simple architecture](https://www.seegrid.csiro.au/wiki/pub/Siss/PIDServiceUserGuide/Core_Principle_Activity_Diagram.png)



# Deployment
This assumes a machine running Ubuntu 18.04 LTS with at least 10GB of disk space and 1.5GB of RAM

1. [Install Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
2. [Install Docker-Compose](https://docs.docker.com/compose/install/)
3. git clone [] to your Server (ubuntu 18.04 LTS)
4. docker-compose build
5. docker-compose up
6. Pidsvc is deployed at http://localhost:8095

## PostgreSQL Backup
Currently the db is mapped to the host directory /srv/OfW/data/PIDsvc which is backed up.  This directory will need to be created on the host machine before docker-compose can build the images properly

## Accessing the web interface for managing and implementing redirects
Current test deployment is at https://geoconnex.us/pidsvc


## Optional: Enable https

The most straightforward way to serve the PID service over https is to set up a reverse proxy that routes all https traffic coming through port 443 to the "backend service" running on the tomcat docker image on port 8095, and redirects all http traffic coming through port 80 to port 443. The simplest way to do this is with the [Caddy server](https://caddyserver.com/docs/), which by default provisions and renews free SSL certificates from [letsencrypt.org](letsencrypt.org).

### Caddy can be built from source using the Go language.

1. [Install Go](https://golang.org/doc/install)
2. git clone -b v2 "https://github.com/caddyserver/caddy.git"
3. cd caddy/cmd/caddy/

### Installing and configuring Caddy is simple once built
4. go build
5. [Manual Install caddy server for Linux](https://caddyserver.com/docs/install)
6. caddy reverse-proxy --from example.com --to localhost.IP.address:8095

## Optional: Security
1.
2.




