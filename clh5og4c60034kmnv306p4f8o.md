---
title: "Understanding Kubernetes Pods: Deployment, ReplicaSet, and Auto Healing"
datePublished: Tue May 02 2023 02:55:39 GMT+0000 (Coordinated Universal Time)
cuid: clh5og4c60034kmnv306p4f8o
slug: understanding-kubernetes-pods-deployment-replicaset-and-auto-healing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682962873998/a7b19734-e39e-4bd4-938b-3c1fb1957f07.png
tags: software-development, aws, developer, devops, beginners

---

# **📍**Introduction:

Kubernetes is an open-source container orchestration platform that helps manage and scale containerized applications. Pods are the basic building blocks of Kubernetes, representing a single instance of a running process in the cluster. In this blog post, we will explore the concepts of Deployment, ReplicaSet, and Auto Healing in Kubernetes Pods. We will also provide practical code snippets to demonstrate these concepts.

# **📍** Deployment vs ReplicaSet vs Pod:

In Kubernetes, different objects serve various purposes when managing pods. Let's understand the differences between Deployment, ReplicaSet, and Pod.

### **🔹** Pod:

A pod is the smallest deployable unit in Kubernetes, representing a single instance of a running process. It encapsulates one or more containers, storage resources, and network configurations. Pods are ephemeral and disposable, which means they can be created, destroyed, or replaced easily.

### **🔹** ReplicaSet:

A ReplicaSet ensures that a specified number of pod replicas are running at any given time. It acts as a supervisor for pods and maintains a desired state. If any pod fails or gets terminated, the ReplicaSet automatically replaces it to maintain the desired number of replicas. However, ReplicaSet does not provide versioning or rolling updates.

### **🔹** Deployment:

A Deployment provides declarative updates to pods and ReplicaSets. It allows you to define the desired state of your application, including the number of replicas and container specifications. Deployments support features like rolling updates, rollbacks, scaling, and more. They also ensure high availability by managing ReplicaSets in the background.

# **📍** Auto Healing:

Auto Healing is a crucial feature in Kubernetes that ensures the continuous availability of applications by automatically recovering from failures. When a pod fails or becomes unresponsive, Kubernetes detects the failure and takes action to replace or heal it.

Kubernetes provides various mechanisms for Auto Healing, such as:

### **🔹** Readiness Probes:

Kubernetes periodically checks the readiness of pods by sending requests to specified endpoints. If a pod fails to respond within a specified timeout period, it is considered unhealthy and gets replaced.

### **🔹** Liveness Probes:

Liveness probes monitor the health of pods by periodically checking a specific endpoint. If the probe fails, Kubernetes terminates the pod and replaces it with a new one.

### **🔹** Replication Controller:

The Replication Controller ensures the desired number of replicas are running. If a pod fails or terminates, the Replication Controller automatically creates a new pod to maintain the desired state.

# **📍** Demo:

Let's now dive into a practical demonstration of Kubernetes Pods, Deployments, and Auto Healing.

### **🔹** Pod Creation:

To create a basic pod, you need to define its specifications in a YAML file. Here's an example of a Pod definition:

```plaintext
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx:latest
      ports:
        - containerPort: 80
```

### **🔹** Deployment Creation:

Deployments allow you to manage and update the desired state of your application. Here's an example of a Deployment definition:

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
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
          image: nginx:latest
          ports:
            - containerPort: 80
```

To demonstrate Auto Healing using readiness probes, add the following section to the Pod definition:

### **🔹 Auto Healing Code:**

```plaintext
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx:latest
      ports:
        - containerPort: 80
      readinessProbe:
        httpGet:
          path: /health
          port: 80
        initialDelaySeconds: 10
        periodSeconds: 5
```

In the above example, we added a readiness probe to the Pod. The readiness probe is configured to perform an HTTP GET request to the `/health` endpoint on port 80. It waits for 10 seconds after the container starts before performing the first check. Subsequently, it checks the readiness every 5 seconds. If the probe fails, Kubernetes considers the pod as unhealthy and initiates the healing process.

To apply the pod definition, save the file and run the following command:

### **🔹** Apply the Kubernetes files:

```plaintext
kubectl apply -f pod-definition.yaml
```

Kubernetes will create the pod and start the container. The readiness probe will periodically check the health of the pod by accessing the specified endpoint. If the probe fails to receive a successful response within a specified timeout, Kubernetes will automatically terminate the unhealthy pod and create a new one.

Note: Make sure to implement the `/health` endpoint in your application that responds with a status code 200 when the application is healthy.

# **📍** Conclusion:

In this blog post, we explored the concepts of Kubernetes Pods, Deployments, and Auto Healing. We learned that Pods are the basic units, while Deployments and ReplicaSets help manage and maintain the desired state of Pods. Auto Healing mechanisms like readiness probes, liveness probes, and Replication Controllers ensure continuous availability and recovery from failures.

Kubernetes provides a robust platform for container orchestration, enabling seamless scaling, updating, and managing containerized applications. By understanding and utilizing the concepts covered in this blog post, you can effectively deploy and manage Pods in your Kubernetes cluster.

# **📍 Resources:**

Image Credit: [https://www.educative.io/blog/kubernetes-deployments-strategies](https://www.educative.io/blog/kubernetes-deployments-strategies)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682962894251/2b4079b9-f25a-4e05-9bad-11d28c231ef2.png align="center")

%[https://youtu.be/lVKLkyuRWCY?list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa]