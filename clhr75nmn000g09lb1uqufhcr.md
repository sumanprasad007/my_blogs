---
title: "Kubernetes Monitoring Using Prometheus & Grafana"
datePublished: Wed May 17 2023 04:22:33 GMT+0000 (Coordinated Universal Time)
cuid: clhr75nmn000g09lb1uqufhcr
slug: kubernetes-monitoring-using-prometheus-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684255993192/393e7e5d-0967-43db-93f1-e6cdd88abccd.png
tags: software-development, aws, developer, devops, beginners

---

## **📍 Introduction:**

Monitoring is a critical aspect of managing Kubernetes clusters, ensuring their stability and performance. In this blog post, we will explore how to monitor Kubernetes clusters using Prometheus and visualize the metrics using Grafana. We will provide step-by-step instructions, along with code snippets, to help you get started with monitoring your own Kubernetes environment.

## **📍 Prerequisites:**

Before we dive into the details, there are a few prerequisites that you should have in place:

1. Kubernetes Cluster: You will need a Kubernetes cluster to monitor. If you don't have one set up already, you can use Minikube, a lightweight Kubernetes distribution for local development and testing.
    
2. Helm: Helm is a package manager for Kubernetes that simplifies the deployment of applications and services. Install Helm on your system if you haven't done so already.
    

To install Minikube and Helm, follow the instructions provided in the links below:

* **Click here to 👉** [**Install Minikube**](https://minikube.sigs.k8s.io/docs/start/)
    
* **Click here to 👉** [**Install Helm**](https://helm.sh/docs/intro/install/)
    

## **🔹 Importance of Monitoring Kubernetes Clusters:**

Monitoring your Kubernetes cluster is crucial for the following reasons:

1. **Issue Identification and Troubleshooting:** With real-time monitoring, you can quickly identify and address issues such as application crashes, resource bottlenecks, and network problems. Monitoring allows you to troubleshoot problems before they escalate and impact your users.
    
2. **Performance Optimization and Capacity Planning:** By monitoring the performance of your applications and infrastructure over time, you can identify opportunities to optimize performance and capacity. Understanding resource consumption and usage patterns enables informed decisions about scaling your infrastructure and improving application efficiency.
    
3. **Ensuring High Availability:** Kubernetes is designed to provide high availability for applications, but this requires careful monitoring and management. By monitoring your cluster and setting up alerts, you can ensure that your applications remain available even in the event of failures or unexpected events.
    
4. **Security and Compliance:** Monitoring your Kubernetes cluster helps identify potential security risks and ensures compliance with regulations and policies. By tracking access logs and other security-related metrics, you can quickly detect and respond to potential security threats.
    

## **🔹 Using Prometheus for Monitoring:**

Prometheus is an open-source monitoring and alerting system that collects and stores metrics about software systems and infrastructure. It provides a powerful query language, a flexible data model, and integrations with other tools. Prometheus allows you to monitor metrics such as CPU usage, memory usage, network traffic, and application-specific metrics.

Here's why Prometheus is a popular choice for Kubernetes monitoring:

1. **Open-Source:** Prometheus is free to use and has a large community of contributors. You can benefit from ongoing development, bug fixes, and feature enhancements without relying on a commercial monitoring solution.
    
2. **Native Kubernetes Support:** Prometheus seamlessly integrates with Kubernetes. It is easy to deploy and provides pre-configured Kubernetes dashboards. It supports auto-discovery of Kubernetes services and pods, simplifying setup and configuration.
    
3. **Powerful Query Language:** Prometheus offers a powerful query language that allows easy retrieval and analysis of metrics data. This empowers you to create custom dashboards, alerts, and troubleshoot issues efficiently.
    
4. **Scalability:** Prometheus is designed to scale and handle large and complex Kubernetes environments. It supports multi-node architectures and can process large volumes of data without significant performance degradation.
    
5. **Integrations:** Prometheus integrates with various tools, including Grafana for data visualization, Alertmanager for alerting, and the Kubernetes API server for metadata discovery.
    

## **🔹 Prometheus Architecture:**

![](https://camo.githubusercontent.com/2cb8b2d19c897fef44f30b6a0c8ba5d0c6ea7ffde700cdd84d3c053ad0406815/68747470733a2f2f70726f6d6574686575732e696f2f6173736574732f6172636869746563747572652e706e67 align="left")

## **🔹 What is Grafana?**

Grafana is a widely-used open-source data visualization and analytics platform that enables the creation of custom dashboards and visualizations based on various data sources. Grafana is particularly well-suited for real-time monitoring and analysis of metrics and logs, making it an ideal tool for monitoring systems and applications, including Kubernetes environments.

Here's why Grafana stands out as a powerful visualization tool:

1. **Data Source Support:** Grafana supports a wide range of data sources, including databases, time-series databases, and other data storage systems. This flexibility allows you to gather data from multiple sources and consolidate it into meaningful visualizations.
    
2. **Query Language and Analysis:** Grafana provides a robust query language that facilitates retrieving and analyzing data from various sources. With this query language, you can extract specific metrics, apply transformations, and aggregate data to create comprehensive visual representations.
    
3. **Customizable Dashboards:** Grafana empowers users to create highly customizable dashboards that display data in a visually appealing and intuitive manner. You can arrange graphs, charts, tables, and other visual elements to build a dashboard that meets your specific monitoring needs.
    
4. **Alerting and Notifications:** Grafana includes built-in alerting capabilities, enabling you to set up thresholds and triggers to receive notifications when metrics breach defined thresholds. This feature ensures that you are promptly notified of critical issues in your Kubernetes cluster.
    
5. **Extensibility:** Grafana supports a vast ecosystem of plugins and integrations, allowing you to extend its functionality and integrate with popular monitoring and logging tools such as Prometheus, Elasticsearch, and InfluxDB. This extensibility enables seamless integration with your existing monitoring stack.
    

By combining Prometheus and Grafana, you can leverage the monitoring capabilities of Prometheus to collect and store metrics, while utilizing Grafana's visualization features to gain valuable insights from that data.

In the upcoming sections, we will walk you through the process of setting up Prometheus and Grafana for monitoring your Kubernetes cluster, providing detailed instructions and code snippets to help you follow along. Stay tuned!

\*Note: The next sections will contain detailed instructions and code snippets for setting up Prometheus and Grafana for monitoring Kubernetes clusters.

**Setting Up Prometheus and Grafana for Monitoring Kubernetes Clusters**

In this section, we will guide you through the process of setting up Prometheus and Grafana to monitor your Kubernetes cluster. We will cover the installation of Prometheus, configuring Kubernetes scraping, and integrating Grafana for visualizing the metrics.

## **🔹 Installing Prometheus:**

To install Prometheus, follow these steps:

* Step 1: Added the Prometheus, Updated it and created namespace:
    
    ```plaintext
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    
    helm repo update
    
    kubectl create namespace prometheus
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684257862514/16cb5af7-3184-4894-afac-62ebbefbff4b.png align="center")
    
* Step 2: Apply the Prometheus Helm chart to the namespace:
    
    ```plaintext
    helm install prometheus prometheus-community/kube-prometheus-stack -n prometheus
    ```
    
* Step 3: Verify that the Prometheus components are successfully deployed:
    
    ```plaintext
    kubectl get pods -n prometheus
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684258003975/6379fb09-d556-4aee-a537-71dadaf4321e.png align="center")
    
* Step 4: Checking all the services using
    
    ```plaintext
    kubectl get svc -A
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684258585149/764880b6-10d7-4863-a870-6293695fea37.png align="center")
    
* **Configuring Kubernetes Scraping:**
    

To configure Prometheus to scrape metrics from your Kubernetes cluster, you need to set up service discovery and specify the targets to scrape.

* Step 1: Open the Prometheus configuration file for editing:
    
    ```plaintext
    kubectl edit configmap prometheus-server -n prometheus
    ```
    
* Step 2: Add the following configuration under the `prometheus.yml` section to enable Kubernetes service discovery and scraping:
    
    ```plaintext
    scrape_configs:
    - job_name: 'kubernetes-apiservers'
      kubernetes_sd_configs:
      - role: endpoints
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
        action: keep
        regex: default;kubernetes;https
    ```
    
* Step 3: Save and exit the configuration file.
    

## **🔹 Integrating Grafana for Visualization:**

Now, let's integrate Grafana with Prometheus to visualize the collected metrics.

* Step 1: Install Grafana using Helm:
    
    ```plaintext
    helm repo add grafana https://grafana.github.io/helm-charts
    
    
    helm repo update
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684259406823/d421c24c-843d-4b60-8b82-0dac4975a8e1.png align="center")
    
* Expose Grafana Services
    
    ```plaintext
    kubectl expose service grafana — type=NodePort — target-port=3000 — name=grafana-ext
    ```
    
* Step 2: Retrieve the Grafana admin password:
    
    ```plaintext
    kubectl get secret --namespace prometheus grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
    ```
    
* Step 3: Port-forward the Grafana service to access the Grafana web interface locally:
    
    ```plaintext
    kubectl port-forward service/grafana -n prometheus 3000:80
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684257802406/611df05b-44aa-47cd-a5db-f0b8a96d45a0.png align="center")
    
* Step 4: Open your web browser and navigate to [`http://localhost:3000`](http://localhost:3000). Log in with the admin username (default: `admin`) and the password obtained in Step 2.
    
* Step 5: Configure a data source in Grafana:
    
    * Click on the "Configuration" (gear) icon in the left sidebar.
        
    * Select "Data Sources" and click on the "Add data source" button.
        
    * Choose Prometheus as the data source type.
        
    * Set the URL to [`http://prometheus-server.prometheus.svc.cluster.local`](http://prometheus-server.prometheus.svc.cluster.local).
        
    * Click "Save & Test" to verify the connection to Prometheus.
        
* Step 6: Import pre-built Kubernetes dashboards in Grafana:
    
    * Click on the "+" icon in the left sidebar and select "Import".
        
    * Enter the dashboard ID for the desired Kubernetes dashboard (e.g., `6417`, `11195`, or `11623`).
        
    * Configure the data source to use Prometheus.
        

Click "Import" to import the dashboard and view the metrics.

Congratulations! You have successfully set up Prometheus and Grafana for monitoring your Kubernetes cluster. You can now explore the pre-built Kubernetes dashboards in Grafana, customize them according to your needs, and visualize the metrics collected by Prometheus.

## **📍 Conclusion:**

Monitoring your Kubernetes cluster is crucial for ensuring the health, performance, and security of your applications and infrastructure. By leveraging tools like Prometheus and Grafana, you can collect, store, analyze, and visualize metrics from your Kubernetes environment. Prometheus provides a powerful monitoring and alerting system, while Grafana offers flexible and customizable data visualization capabilities.

In this blog post, we covered the importance of monitoring Kubernetes clusters and why Prometheus and Grafana are popular choices for this task. We provided step-by-step instructions, along with code snippets, to guide you through the process of setting up Prometheus and Grafana for monitoring your Kubernetes cluster. By following these instructions, you can gain valuable insights into the health and performance of your Kubernetes environment and take proactive measures to optimize and troubleshoot issues. Remember, monitoring is an ongoing process, and it is essential to regularly review and fine-tune your monitoring setup as your applications and infrastructure evolve. Stay vigilant, keep an eye on your metrics, and leverage the power of Prometheus and Grafana to ensure the smooth operation of your Kubernetes cluster.

Happy monitoring!

## **🔹 Additional Resources:**

* [**Prometheus Documentation**](https://prometheus.io/docs/)
    
* [**Grafana Documentation**](https://grafana.com/docs/)
    
* [**Kubernetes Documentation**](https://kubernetes.io/docs/)
    
* [**Prometheus Operator**](https://github.com/prometheus-operator/prometheus-operator)
    
* [**Grafana Dashboards**](https://grafana.com/grafana/dashboards)
    

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684256136175/44305bb4-89c4-49f0-98aa-b16c3db06727.png align="center")