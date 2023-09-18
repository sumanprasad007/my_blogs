---
title: "Monitoring Containers with Prometheus and cAdvisor 🐳📊"
datePublished: Mon Sep 18 2023 04:30:10 GMT+0000 (Coordinated Universal Time)
cuid: clmoe12m5000u09mk8j2d7zp3
slug: monitoring-containers-with-prometheus-and-cadvisor
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694974264516/38d6db8a-6ce8-40ad-8fc6-fa6d28e07647.gif
tags: web-development, developer, devops, 90daysofdevops, trainwithshubham

---

# Introduction:

In the world of containerized applications, monitoring and gathering performance data is essential to ensure the reliability and efficiency of your services. **cAdvisor**, short for Container Advisor, is a powerful tool that allows you to analyze and expose resource usage and performance data from running containers. This article will guide you through setting up a monitoring stack using **Prometheus**, cAdvisor, and Grafana to help you gain insights into your containerized applications. 🚀

## What is cAdvisor? 🧐

cAdvisor is a container monitoring tool developed by Google. It provides real-time information about resource usage, performance metrics, and container statistics. One of its significant advantages is that it exposes metrics in a format compatible with **Prometheus**, a popular open-source monitoring and alerting toolkit. 📈

### Setting Up Prometheus 🛠️

To get started with Prometheus, follow these steps:

* **Download the Prometheus Configuration File** 📥:
    
* ```plaintext
        wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
    ```
    
* **Install Prometheus Using Docker** 🐋:
    
    Run Prometheus in a Docker container, using the configuration file you downloaded:
    
* ```plaintext
        docker run -d --name=prometheus -p 9090:9090 -v <PATH_TO_prometheus.yml_FILE>:/etc/prometheus/prometheus.yml prom/prometheus --config.file=/etc/prometheus/prometheus.yml
    ```
    

### Adding cAdvisor as a Target 🎯

To start collecting metrics from cAdvisor, add it as a scrape target in your Prometheus configuration. Edit the `prometheus.yml` file you downloaded earlier and append the following configuration:

```plaintext
scrape_configs:
- job_name: cadvisor
  scrape_interval: 5s
  static_configs:
  - targets:
    - cadvisor:8080
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694974820264/d00b4ff5-5680-45af-ba15-4f8ff087793a.png align="center")

### Using Docker Compose 🐳🤝

For a more streamlined setup, you can use Docker Compose. Create a `docker-compose.yaml` file with the following content:

```plaintext
version: '3.2'
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
    - 9090:9090
    command:
    - --config.file=/etc/prometheus/prometheus.yml
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    depends_on:
    - cadvisor
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:rw
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    depends_on:
    - redis
  redis:
    image: redis:latest
    container_name: redis
    ports:
    - 6379:6379
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694974836137/6e203257-52a0-408c-900e-3191a0403096.png align="center")

Run Prometheus and cAdvisor with Docker Compose:

```plaintext
docker-compose up -d
```

You can check the status of the containers using:

```plaintext
docker-compose ps
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694974907721/c4504e16-4902-44f0-ac23-0cbdd2c89bb8.png align="center")

### Visualizing Metrics with Grafana 📊📈

To visualize the collected metrics, you can use **Grafana**, a popular open-source dashboard and visualization platform.

#### Installing Grafana on Debian or Ubuntu 📊🐧

1. Install the required dependencies:
    

* ```plaintext
        sudo apt-get install -y apt-transport-https
        sudo apt-get install -y software-properties-common wget
    ```
    
* Add the Grafana GPG key and repository:
    

```plaintext
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```

For the stable release, add:

```plaintext
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

Or for the beta release, add:

* ```plaintext
        echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
    ```
    
* Update the package list:
    
* ```plaintext
        sudo apt-get update
    ```
    
* Install Grafana:
    
* ```plaintext
        sudo apt-get install grafana
    ```
    
* Start Grafana:
    
* ```plaintext
       sudo /bin/systemctl start grafana-server
    ```
    

Now, you can access Grafana at [`http://localhost:3000`](http://localhost:3000) and set up dashboards to visualize the metrics collected by Prometheus from cAdvisor.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694974769071/51146d04-1873-4784-94f9-a96aab5c1aa2.png align="center")

## Conclusion 🎉

By setting up Prometheus with cAdvisor and Grafana, you have created a robust container monitoring stack. You can now effectively monitor the resource usage and performance metrics of your containerized applications, helping you to make data-driven decisions and ensure the health and performance of your services. Happy monitoring! 🚀🐳📈