---
title: "Day 2 - Kubernetes Networking: Ingress, Network Policies, DNS, CNI Plugins"
datePublished: Wed Apr 26 2023 04:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clgx64lmt0000a9nv4txqbyde
slug: day-2-kubernetes-networking-ingress-network-policies-dns-cni-plugins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682421840964/86748457-80f5-4dd3-9b00-883220c48e1e.png
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

Welcome to this blog post where we will be discussing various Kubernetes concepts and how to practically use them on AWS. This post is specifically targeted towards the #KubeWeek challenge and we will be focusing on Services, Ingress, Network Policies, DNS, and CNI (Container Network Interface) plugins.

To complete this challenge, we will be using an AWS EC2 instance with kubectl and minikube installed. We will be focusing on the following topics:

* Services
    
* Ingress
    
* Network Policies
    
* DNS
    
* CNI plugins
    

Let's get started!

## **🔹** Setting up Minikube on AWS EC2 instance

Before we start exploring the Kubernetes concepts, we need to set up Minikube on our AWS EC2 instance. To do that, follow these steps:

1. Launch an AWS EC2 instance with Ubuntu.
    
2. Install the required dependencies:
    

```python
sudo apt-get update && \
sudo apt-get install -y apt-transport-https \
    ca-certificates curl software-properties-common gnupg2
```

1. Add the Kubernetes repository key:
    

```python
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

1. Add the Kubernetes repository:
    

```python
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```

1. Install Kubernetes tools:
    

```python
sudo apt-get update && \
sudo apt-get install -y kubectl && \
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && \
chmod +x minikube && sudo mv minikube /usr/local/bin/
```

1. Start Minikube:
    

```python
minikube start --driver=docker
```

We now have Minikube up and running on our AWS EC2 instance. Let's start exploring some of the core Kubernetes concepts.

# **📍** Services

Kubernetes Services are an abstraction layer that enables communication between a set of pods and other Kubernetes Services. Services provide a stable IP address and DNS name that can be used by other pods to access the service.

In Kubernetes, Services are created using a YAML file that specifies the configuration of the Service. Here is an example YAML file for creating a Service:

```python
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
  - name: http
    port: 80
    targetPort: 80
  - name: https
    port: 443
    targetPort: 443
  type: LoadBalancer
```

Let's break down this YAML file:

* `apiVersion` - The version of the Kubernetes API used to create the Service.
    
* `kind` - The type of Kubernetes resource we want to create.
    
* `metadata` - The metadata associated with the Service, including the name of the Service.
    
* `spec` - The specification of the Service, including the selector and ports.
    
* `selector` - The label selector used to identify the pods that should be part of the Service.
    
* `ports` - The ports that the Service will listen on, along with their names and target ports.
    
* `type` - The type of Service we want to create. In this case, we are creating a LoadBalancer Service.
    

To create this Service, save the YAML file as `my-service.yaml` and execute the following command:

```python
kubectl apply -f my-service.yaml
```

# **📍** Ingress

Ingress is a Kubernetes resource that enables the external access to Services in a cluster. Ingress acts as a layer 7 load balancer that routes traffic to different Services based on the HTTP or HTTPS path specified in the request.

To create an Ingress resource, we need to first ensure that we have an Ingress controller installed on our Kubernetes cluster. An Ingress controller is a piece of software that implements the Ingress specification and provides the actual load balancing functionality.

For the purpose of this demo, we will be using the NGINX Ingress controller. To install the NGINX Ingress controller, execute the following command:

```python
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.0/deploy/static/provider/aws/deploy.yaml
```

Once the Ingress controller is installed, we can create an Ingress resource using a YAML file. Here is an example YAML file for creating an Ingress resource:

```python
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /my-service
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              name: http
```

Let's break down this YAML file:

* `apiVersion` - The version of the Kubernetes API used to create the Ingress resource.
    
* `kind` - The type of Kubernetes resource we want to create.
    
* `metadata` - The metadata associated with the Ingress resource, including the name of the Ingress resource and any annotations.
    
* `spec` - The specification of the Ingress resource, including the rules.
    
* `rules` - The routing rules for the Ingress resource.
    
* `http` - The protocol used for the rule.
    
* `paths` - The paths that match the rule.
    
* `path` - The path that matches the rule.
    
* `pathType` - The type of path matching used. In this case, we are using `Prefix` matching.
    
* `backend` - The backend Service that traffic will be routed to.
    
* `service` - The name of the Service that traffic will be routed to.
    
* `port` - The port that traffic will be routed to.
    

To create this Ingress resource, save the YAML file as `my-ingress.yaml` and execute the following command:

```python
kubectl apply -f my-ingress.yaml
```

# **📍** Network Policies

Kubernetes Network Policies are a way to define how traffic is allowed to flow between pods in a cluster. Network Policies allow for fine-grained control over network traffic, allowing administrators to restrict access to specific pods or namespaces.

To create a Network Policy, we need to first ensure that we have a CNI plugin installed on our Kubernetes cluster that supports Network Policies. For the purpose of this demo, we will be using the Calico CNI plugin. To install the Calico CNI plugin, execute the following command:

```python
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

Once the Calico CNI plugin is installed, we can create a Network Policy using a YAML file. Here is an example YAML file for creating a Network Policy:

```python
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-network-policy
spec:
  podSelector:
    matchLabels:
      app: my-app
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - port: 3306
```

Let's break down this YAML file:

* `apiVersion` - The version of the Kubernetes API used to create the Network Policy.
    
* `kind` - The type of Kubernetes resource we want to create.
    
* `metadata` - The metadata associated with the Network Policy, including the name of the Network Policy.
    
* `spec` - The specification of the Network Policy, including the podSelector and ingress rules.
    
* `podSelector` - The labels used to select the pods that the Network Policy will apply to.
    
* `matchLabels` - The labels used to match the pods.
    
* `ingress` - The rules for incoming traffic.
    
* `from` - The sources of incoming traffic.
    
* `podSelector` - The labels used to select the pods that the traffic is coming from.
    
* `matchLabels` - The labels used to match the pods that the traffic is coming from.
    
* `ports` - The ports that incoming traffic is allowed on.
    

To create this Network Policy, save the YAML file as `my-network-policy.yaml` and execute the following command:

```python
kubectl apply -f my-network-policy.yaml
```

# **📍** DNS

DNS (Domain Name System) is a critical component of any network, allowing clients to resolve hostnames to IP addresses. In a Kubernetes cluster, DNS is used to resolve Service names to their corresponding IP addresses.

Kubernetes has an integrated DNS solution called CoreDNS, which provides automatic DNS resolution for Services within a cluster.

To configure DNS in our Kubernetes cluster, we need to ensure that CoreDNS is running. To check if CoreDNS is running, execute the following command:

```python
kubectl get pods -n kube-system -l k8s-app=kube-dns
```

If CoreDNS is not running, execute the following command to deploy it:

```python
kubectl apply -f https://github.com/kubernetes/kubernetes/blob/master/cluster/addons/dns/coredns.yaml.sed
```

Once CoreDNS is running, we can test DNS resolution by executing the following command:

```python
kubectl run --rm -it busybox --image=busybox:1.28 --restart=Never -- nslookup my-service
```

Replace `my-service` with the name of a Service in your cluster. This command will create a new pod and execute the `nslookup` command to resolve the Service name.

# **📍** CNI Plugins

CNI (Container Network Interface) plugins are responsible for configuring the networking for pods in a Kubernetes cluster. There are many different CNI plugins available, each with its own strengths and weaknesses.

For the purpose of this demo, we will be using the Calico CNI plugin, which provides advanced networking features such as Network Policies.

To install the Calico CNI plugin, execute the following command:

```python
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

Once the Calico CNI plugin is installed, we can verify that it is running by executing the following command:

```python
kubectl get pods -n kube-system -l k8s-app=calico-node
```

This command will list the pods running in the `kube-system` namespace with the label `k8s-app=calico-node`.

# **📍** Conclusion

In conclusion, we have learned about several Kubernetes concepts that are essential for deploying and managing applications on a Kubernetes cluster.

Services are used to expose pods to the network and provide a stable IP address and DNS name. Ingress is used to route traffic from outside the cluster to Services inside the cluster. Network Policies are used to control the traffic between pods by specifying rules for incoming and outgoing traffic. DNS is used to resolve Service names to IP addresses and is critical for communication between pods and Services within a cluster. Finally, CNI plugins are responsible for configuring networking for pods in a Kubernetes cluster. With the code snippets and practical examples provided in this blog post, you should have a better understanding of how to deploy and manage your own Kubernetes cluster using AWS EC2, kubectl, and Minikube.