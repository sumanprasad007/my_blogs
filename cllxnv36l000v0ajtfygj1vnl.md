---
title: "Mastering DaemonSets in Kubernetes: Ensuring Pods are Everywhere! 🚀"
datePublished: Wed Aug 30 2023 11:35:40 GMT+0000 (Coordinated Universal Time)
cuid: cllxnv36l000v0ajtfygj1vnl
slug: mastering-daemonsets-in-kubernetes-ensuring-pods-are-everywhere
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693395157541/38770c14-87ce-41fa-835f-e6ea4312ad60.png
tags: aws, kubernetes, developer, devops, 90daysofdevops

---

# **Introduction:**

Kubernetes is all about orchestrating containerized applications with elegance and precision. One essential tool in the Kubernetes arsenal is the DaemonSet. In this blog, we'll uncover the mysteries of DaemonSets, explore their features, set them up using YAML code, and dive into real-world use cases. Buckle up; we're in for a ride! 🎢

## **What Are DaemonSets, and Why Do We Need Them? 🤔**

**DaemonSets** are a resource type in Kubernetes that ensure that a copy of a pod runs on all (or some) nodes in a cluster. They're like the silent but diligent guardians of your cluster, making sure specific pods are present on every node. But why use them?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693331204392/f77988a1-b12e-4d5d-8aa6-e10692ecee88.png align="center")

### **🌟 Features of DaemonSets:**

Let's start by understanding what DaemonSets bring to the table:

1. **Pod Pervasiveness**: DaemonSets are your ticket to ensuring that essential pods run on every node in your cluster, such as monitoring agents or logging daemons.
    
2. **Easy Scaling**: They automatically add or remove pods as nodes are added to or removed from the cluster. No manual intervention needed!
    
3. **Node-Aware Scheduling**: DaemonSets schedule pods only on nodes that meet specific criteria. This enables you to run specialized pods on specific nodes.
    
4. **Rolling Updates**: When you need to update DaemonSet pods, Kubernetes handles it gracefully by rolling out new ones and terminating old ones.
    

## **Real-World Use Cases with DaemonSets 🌐**

Let's explore some real-world scenarios where DaemonSets shine:

### **Use Case 1: Log Aggregation 📊**

Imagine you have a logging solution like Fluentd or Filebeat. You want to ensure that these agents are running on every node to collect logs locally before sending them to a central system. DaemonSets make this a breeze!

### **Use Case 2: Monitoring 📈**

In the world of monitoring, Prometheus and Grafana are rock stars. DaemonSets help you deploy Prometheus Node Exporters or other monitoring agents on every node, ensuring that you gather metrics from every corner of your cluster.

### **Use Case 3: Security 🔐**

When it comes to security, you might want to deploy security scanners, such as Clair for vulnerability scanning. DaemonSets ensure that these scanners are active on every node, constantly checking for vulnerabilities.

### **Setting Up a DaemonSet Using YAML 🛠️**

Enough theory; let's get practical! To set up a DaemonSet, you'll need a YAML configuration file. Here's a simplified example:

```plaintext
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image:latest
```

In this YAML file:

* [`metadata.name`](http://metadata.name): Assign a name to your DaemonSet.
    
* `selector.matchLabels`: Specify the labels that nodes must have to run pods from this DaemonSet.
    
* `spec.template.spec.containers`: Define the pod's containers, images, and configurations.
    

Apply this YAML with `kubectl apply -f my-daemonset.yaml`, and your DaemonSet is ready to roll!

## **Conclusion 🎉**

DaemonSets are like the unsung heroes of Kubernetes, quietly ensuring that essential pods are running everywhere they should be. Armed with their features and YAML configurations, you can tackle real-world use cases with ease, making your Kubernetes cluster more robust and reliable.

So, the next time you need pods running everywhere in your Kubernetes cluster, remember the trusty DaemonSet. It's your reliable companion in the world of container orchestration! 🌐💪

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/oVJoN5Zc3Kw]