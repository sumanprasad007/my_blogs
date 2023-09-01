---
title: "Monitoring Kubernetes with Prometheus 🚀"
datePublished: Fri Sep 01 2023 13:17:14 GMT+0000 (Coordinated Universal Time)
cuid: clm0mdez9000609l7g48v7psb
slug: monitoring-kubernetes-with-prometheus
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693571658596/e72c7746-15fa-4d97-9c92-cd60c22a5569.png
tags: kubernetes, developer, devops, prometheus, 90daysofdevops

---

# **Introduction:**

Prometheus, an open-source monitoring and alerting toolkit, has emerged as a powerful solution to keep an eye on your Kubernetes clusters. 📈

In this blog, we'll explore what Prometheus is, the problems it solves, its key features, and how to set it up to monitor a Kubernetes cluster running on EC2 servers inside a kubeadm cluster. 🌐

## **What Is Prometheus? 🤔**

**Prometheus** is an open-source monitoring and alerting toolkit initially developed at SoundCloud. It's designed to gather metrics from various systems, record them in a time series database, and provide a query language for exploring these metrics. 📊

## **Problems Prometheus Solves 🛠️**

Prometheus addresses several common monitoring challenges in a Kubernetes environment:

* **Dynamic Environment**: Kubernetes is known for its dynamic nature, with pods being created and destroyed continuously. Prometheus can automatically discover and monitor these changes.
    
* **Scalability**: As your Kubernetes cluster scales, Prometheus can scale with it, thanks to its simple, horizontally scalable architecture.
    
* **Multi-Dimensional Data**: Prometheus allows you to attach labels to metrics, making it easy to filter and aggregate data, even in complex, multi-service architectures.
    

## **Key Features of Prometheus 🌟**

### **1\. Data Scraping 🔄**

Prometheus scrapes (pulls) metrics from various sources, such as application endpoints, services, or even other Prometheus instances. This data is then stored in a time series database.

### **2\. Multi-Dimensional Data Model 📦**

Prometheus uses a powerful data model with labels that enable you to slice and dice metrics easily. This helps when troubleshooting issues or conducting root cause analysis.

### **3\. Flexible Query Language 🧮**

PromQL (Prometheus Query Language) provides expressive querying capabilities, allowing you to create custom dashboards and alerts.

### **4\. Alerting 🚨**

Prometheus can trigger alerts based on custom-defined conditions, helping you respond to issues proactively.

### **5\. Service Discovery 🌐**

Prometheus can automatically discover targets to scrape, making it suitable for dynamic environments like Kubernetes.

## **Setting Up Prometheus to Monitor a Kubernetes Cluster on EC2 🚀**

### **Prerequisites 🛠️**

* A running Kubernetes cluster managed by kubeadm on EC2 servers.
    
* `kubectl` installed and configured.
    
* `helm` (the Kubernetes package manager) installed.
    

### **Step 1: Deploy Prometheus using Helm 🎩**

```plaintext
# Add the Prometheus Helm chart repository
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

# Install Prometheus using Helm
helm install prometheus prometheus-community/prometheus
```

### **Step 2: Expose Prometheus 🌐**

By default, Prometheus runs as a ClusterIP service. To access it from outside the cluster, you can use a NodePort or an Ingress resource.

```plaintext
# Expose Prometheus via NodePort (for demonstration purposes)
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-nodeport
```

### **Step 3: Access Prometheus UI 🖥️**

You can now access Prometheus UI by finding the NodePort assigned to the service (replace `<nodeport>` with the actual port number):

```plaintext
# Get the NodePort assigned to Prometheus
kubectl get svc prometheus-nodeport

# Access Prometheus UI in your web browser
http://<ec2-instance-public-ip>:<nodeport>
```

### **Step 4: Start Monitoring 🚀**

You're all set! You can start writing custom PromQL queries, creating dashboards, and setting up alerts to monitor your Kubernetes cluster effectively.

### **Clean Up Prometheus Deployment**

```plaintext
# Delete the Prometheus release using Helm
helm uninstall prometheus

# Delete the Kubernetes service exposing Prometheus (NodePort)
kubectl delete svc prometheus-nodeport

# Ensure all Prometheus-related resources are deleted (e.g., pods, configmaps)
kubectl delete all -l release=prometheus
```

## **Conclusion 🎉**

Prometheus is a powerful monitoring solution that perfectly fits the dynamic and scalable nature of Kubernetes. It helps you gain insights into your cluster's performance and health, allowing you to proactively respond to issues.

By following the steps outlined in this blog, you can quickly set up Prometheus to monitor your Kubernetes cluster running on EC2 servers and start reaping the benefits of robust observability. Happy monitoring! 🚀🔍📊

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [https://linktr.ee/sumanprasad007](https://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]