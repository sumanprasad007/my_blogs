---
title: "🚀 Step-by-Step Guide to Installing and Configuring Ingress on Minikube Cluster"
datePublished: Thu Aug 10 2023 12:53:02 GMT+0000 (Coordinated Universal Time)
cuid: cll55tjih000c0al4eu0ph3db
slug: step-by-step-guide-to-installing-and-configuring-ingress-on-minikube-cluster
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691603443001/96663ac8-02d4-42b4-85ae-08d81c22fd64.png
tags: linux, kubernetes, developer, devops, 90daysofdevops

---

## 📍 Introduction:

In the world of Kubernetes, managing and controlling traffic between services is crucial. 🌐 Ingress controllers play a vital role in achieving this by acting as the entry point for external traffic to reach services within the cluster. In this guide, we'll walk you through the process of installing and configuring an Ingress controller on a Minikube cluster, focusing on setting up rules for the Kubernetes Dashboard. By the end of this tutorial, you'll have a clear understanding of how to leverage Ingress to efficiently manage traffic in your Kubernetes environment.

### 🔧 Step 1: Installing the Ingress Controller

To begin, we need to enable the Ingress addon on our Minikube cluster. Open your terminal and run the following command:

```bash
minikube addons enable ingress
```

This command will ensure that the Ingress controller is up and running on your Minikube cluster, ready to handle incoming traffic.

### 📝 Step 2: Setting Up Controller Rules for Kubernetes Dashboard

Now, let's set up the Ingress rules specifically for the Kubernetes Dashboard. Create a YAML file named `dashboard-ingress.yaml` and define the necessary rules. You can use a text editor of your choice to create this file. Here's an example of what the contents might look like:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: dashboard-ingress
  namespace: kubernetes-dashboard
spec:
  rules:
    - host: dashboard.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: kubernetes-dashboard
                port:
                  number: 80
```

Apply the Ingress configuration using the following command:

```bash
kubectl apply -f dashboard-ingress.yaml
```

To verify that the Ingress has been successfully applied, run:

```bash
kubectl get ingress -n kubernetes-dashboard
```

### 🔍 Step 3: Monitoring the Ingress

To monitor the Ingress and obtain the IP address associated with it, run the following command:

```bash
kubectl get ingress -n kubernetes-dashboard --watch
```

This command will display real-time updates about the Ingress configuration. Once you see an IP address listed, proceed to the next step.

### 🛠️ Step 4: Updating Hosts File

Now that we have the IP address, we need to update the `hosts` file on your system. Open the hosts file using a text editor with administrative privileges. For example:

```bash
sudo vim /etc/hosts
```

Add an entry to map the IP address to a domain name, like this:

```plaintext
192.168.49.2     dashboard.com
```

Remember to replace `<IP Address>` with the actual IP you obtained from the Ingress.

### 🌐 Step 5: Accessing the Kubernetes Dashboard

With the host's file updated, you can now access the Kubernetes Dashboard using your browser. Open a web browser and enter either the IP address you used or the custom domain name you specified (`dashboard.com`). You should see the Kubernetes Dashboard interface.

📌 Note: In this setup, we associated a local domain name with the private IP address obtained from the Ingress controller. If you were to perform these steps on platforms like Amazon EKS or Microsoft AKS, you would receive a public IP address instead.

## Conclusion:

🎉 Congratulations! You've successfully installed and configured an Ingress controller on your Minikube cluster and set up rules to access the Kubernetes Dashboard. Ingress controllers provide a powerful way to manage traffic in your Kubernetes environment, allowing you to efficiently route incoming requests to the appropriate services. By following this guide, you've gained valuable insights into leveraging Ingress for better traffic management. 🚦