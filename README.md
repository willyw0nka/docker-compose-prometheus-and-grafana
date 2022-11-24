Prometheus-Grafana
========

A monitoring solution for Docker hosts and containers with [Prometheus](https://prometheus.io/), [Grafana](http://grafana.org/), [cAdvisor](https://github.com/google/cadvisor),
[NodeExporter](https://github.com/prometheus/node_exporter).  

This is a forked repository. So, you may want to visit the original repo at [stefanprodan
/
dockprom](https://github.com/stefanprodan/dockprom)

Additional info: [Docker - Prometheus and Grafana](https://bogotobogo.com/DevOps/Docker/Docker_Prometheus_Grafana.php)

## Install

### Create .env:
```
ADMIN_USER=admin  
ADMIN_PASSWORD=admin
```

### Clone this repository on your Docker host, cd into test directory and run compose up:

```
git clone https://github.com/willyw0nka/docker-compose-prometheus-and-grafana.git
cd docker-compose-prometheus-and-grafana
docker-compose up -d
```

## Prerequisites:

* Docker Engine	19.03.0+
* Docker Compose 1.27.0+

## Containers:

* Prometheus (metrics database) `http://<host-ip>:9090`
* Grafana (visualize metrics) `http://<host-ip>:3000`
* NodeExporter (host metrics collector)
* cAdvisor (containers metrics collector)

## Setup Grafana

Navigate to `http://<host-ip>:3000` and login with user ***admin*** password ***admin***. You can change the credentials in the compose file or by supplying the `ADMIN_USER` and `ADMIN_PASSWORD` environment variables via .env file on compose up. The config file can be added directly in grafana part like this
```
grafana:
  image: grafana/grafana:5.2.4
  env_file:
    - config

```
and the config file format should have this content
```
GF_SECURITY_ADMIN_USER=admin
GF_SECURITY_ADMIN_PASSWORD=changeme
GF_USERS_ALLOW_SIGN_UP=false
```
If you want to change the password, you have to remove this entry, otherwise the change will not take effect
```
- grafana_data:/var/lib/grafana
```

Grafana is preconfigured with dashboards and Prometheus as the default data source:

* Name: Prometheus
* Type: Prometheus
* Url: http://prometheus:9090
* Access: proxy

