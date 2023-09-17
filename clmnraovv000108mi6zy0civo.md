---
title: "🚀 Installing Grafana, Loki, and Promtail on Debian/Ubuntu 🐧"
datePublished: Sun Sep 17 2023 17:53:47 GMT+0000 (Coordinated Universal Time)
cuid: clmnraovv000108mi6zy0civo
slug: installing-grafana-loki-and-promtail-on-debianubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694973174311/9f974b1d-6159-4a34-b4d6-0b85e96bd85b.gif
tags: aws, developer, devops, 90daysofdevops, trainwithshubham

---

# **Introduction:**

Are you ready to elevate your observability game? In this guide, we'll walk you through the process of installing Grafana, along with its potent companions, Loki and Promtail, on your Debian or Ubuntu system. 📊📈

## **Installing Grafana 📈**

First things first, let's get Grafana up and running.

```plaintext
# Update and install prerequisites
sudo apt-get update
sudo apt-get install -y apt-transport-https software-properties-common wget

# Fetch the Grafana GPG key
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

# Add the Grafana repository for the stable release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

# Update the list of available packages
sudo apt-get update

# Install the latest OSS release of Grafana
sudo apt-get install -y grafana
```

To start the Grafana Server:

```plaintext
sudo systemctl start grafana-server
```

## **Installing Loki and Promtail with Docker 🐳**

Now, let's bring Loki and Promtail into the mix for powerful log aggregation and analysis.

### **1\. Download Loki Config 📝**

```plaintext
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

### **2\. Run Loki Docker Container 🏗️**

```plaintext
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```

### **3\. Download Promtail Config 📜**

```plaintext
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

### **4\. Run Promtail Docker Container 🏗️**

```plaintext
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```

Now, you've got Grafana, Loki, and Promtail up and running, ready to help you gain valuable insights from your logs and metrics. 🚀🔍

Don't forget to access the Grafana web interface and configure data sources and dashboards for a comprehensive observability experience. Enjoy exploring your data! 🌟✨

## **Accessing Grafana Web Interface 🌐**

With Grafana installed, you can access its intuitive web interface to create dashboards and visualize your data. Open your web browser and navigate to:

```plaintext
http://your_server_ip_or_domain:3000
```

* You'll be greeted with the Grafana login page.
    
* The default login credentials are:
    
    * **Username:** admin
        
    * **Password:** admin
        
* Upon logging in, you'll be prompted to change the password for added security.
    

## **Adding Data Sources 📊**

Before you can start creating dashboards, you need to add data sources. Grafana can connect to various data sources, including Prometheus, which we installed earlier.

1. Click on the gear icon (⚙️) in the left sidebar to open the "Configuration" menu.
    
2. Select "Data Sources."
    
3. Click on the "Add data source" button.
    
4. Choose "Prometheus" from the list.
    
5. Configure the Prometheus data source:
    
    * **Name**: Give it a name, e.g., "My Prometheus."
        
    * **HTTP**: Set the URL to your Prometheus server, typically [`http://localhost:9090`](http://localhost:9090) if running locally.
        
    * Click "Save & Test" to ensure the connection is successful.
        

## **Creating Dashboards 📈**

Now, let's create your first Grafana dashboard to visualize metrics from Prometheus and logs from Loki.

1. In the Grafana interface, click on the "+" icon in the left sidebar, and then select "Dashboard."
    
2. Click on "Add new panel."
    
3. In the "Query" section, choose your data source (e.g., "My Prometheus").
    
4. You can start building your query to fetch the metrics you want to visualize. Grafana provides a user-friendly query builder and a wide range of visualization options.
    
5. Customize your panel as needed, including titles, axes, and legends.
    
6. To add Loki logs to your dashboard, you can create a separate panel by selecting "Logs" as the visualization type and choosing your Loki data source.
    
7. Once you've configured your panel, click "Apply."
    
8. To save your dashboard, click on the disk icon (💾) at the top and give it a name.
    
9. You can also create additional panels and organize them into rows for a comprehensive overview.
    

## **Conclusion 🎉**

Congratulations! You've successfully set up Grafana, Loki, and Promtail on your Debian or Ubuntu server. You're now equipped with a powerful observability stack to monitor, visualize, and analyze your system's metrics and logs.

Explore Grafana's extensive customization options to create informative dashboards tailored to your specific needs. Dive into the world of observability, uncover insights, and stay on top of your system's performance. Happy monitoring! 🚀🔍