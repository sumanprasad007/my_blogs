---
title: "Day 5 - Kubernetes Storage
Kubernetes Security"
datePublished: Sat Apr 29 2023 02:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clh1d8etx00wn9wnv5b6ghj25
slug: day-5-kubernetes-storage-kubernetes-security
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682703079540/6480de64-ed08-4144-83a1-772f746cf400.png
tags: software-development, aws, developer, devops, beginners

---

# **📍** Introduction:

Kubernetes has become the de facto standard for container orchestration due to its flexibility, scalability, and robustness. In this blog post, we will explore two crucial aspects of Kubernetes: storage and security. We will delve into concepts such as Persistent Volumes, Persistent Volume Claims, Storage Classes, StatefulSets, RBAC (Role-Based Access Control), Pod Security Policies, Secrets, Network Policies, and TLS (Transport Layer Security). By understanding these concepts and their implementation, you will be able to enhance the storage capabilities and security posture of your Kubernetes clusters.

## **🔹 Persistent Volumes**

Persistent Volumes (PVs) in Kubernetes provide durable storage resources that can be shared across multiple pods. They are decoupled from individual pods, allowing data persistence even when pods are terminated or rescheduled.

### ⚜ Code Snippet:

```python
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: my-storage-class
  hostPath:
    path: /data/my-pv
```

## **🔹**Persistent Volume Claims

Persistent Volume Claims (PVCs) act as a request for storage resources from a Persistent Volume. They allow pods to consume the storage provided by a Persistent Volume.

### ⚜ Code Snippet:

```python
yamlCopy codeapiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: my-storage-class
```

## **🔹** Storage Classes

Storage Classes provide a way to dynamically provision storage resources in Kubernetes. They abstract the underlying storage implementation details and enable the dynamic allocation of Persistent Volumes.

### ⚜ Code Snippet:

```python
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-storage-class
provisioner: example.com/provisioner
```

## **🔹** StatefulSets

StatefulSets are used to manage stateful applications in Kubernetes. They provide stable network identities and persistent storage for pods, enabling the management of ordered pod creation and termination.

### ⚜ Code Snippet:

```python
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-statefulset
spec:
  serviceName: my-statefulset
  replicas: 3
  selector:
    matchLabels:
      app: my-statefulset
  template:
    metadata:
      labels:
        app: my-statefulset
    spec:
      containers:
        - name: my-app
          image: my-image
```

## **🔹** RBAC (Role-Based Access Control)

RBAC in Kubernetes allows fine-grained access control to resources within a cluster. It enables administrators to define roles and bind them to users or groups, ensuring proper authorization.

### ⚜ Code Snippet:

```python
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: my-role
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]


kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: my-role-binding
subjects:
  - kind: User
    name: alice
    api Version: rbac.authorization.k8s.io/v1 
    roleRef: kind: Role name: my-role 
    apiGroup: rbac.authorization.k8s.io 
subjects:
  - kind: User 
    name: alice 
    apiGroup: rbac.authorization.k8s.io
```

## **🔹** Pod Security Policies

Pod Security Policies provide a declarative way to enforce security constraints on pods running in a Kubernetes cluster. They define a set of conditions that pods must satisfy to be scheduled and run.

### ⚜ Code Snippet:

```python
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: my-pod-security-policy
spec:
  privileged: false
  seLinux:
    rule: RunAsAny
  volumes:
    - 'configMap'
    - 'secret'
  hostNetwork: false
  hostIPC: false
  hostPID: false
  runAsUser:
    rule: MustRunAsNonRoot
  fsGroup:
    rule: RunAsAny
  supplementalGroups:
    rule: RunAsAny
  allowedCapabilities: []
  requiredDropCapabilities: []
```

## **🔹** Secrets

Secrets in Kubernetes provide a way to store and manage sensitive information, such as API keys, passwords, and certificates. They are encrypted and can be mounted as volumes or used as environment variables in pods.

### ⚜ Code Snippet:

```python
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: dXNlcm5hbWU=
  password: cGFzc3dvcmQ=
```

## **🔹** Network Policies

Network Policies control the ingress and egress network traffic for pods in a Kubernetes cluster. They enable you to define granular network rules and segment your applications.

### ⚜ Code Snippet:

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
              role: frontend
        - namespaceSelector:
            matchLabels:
              project: my-project
      ports:
        - protocol: TCP
          port: 80
```

## **🔹** TLS (Transport Layer Security)

TLS (Transport Layer Security) provides secure communication between clients and servers. In Kubernetes, TLS can be configured for various components, such as ingress controllers, API servers, and service-to-service communication.

### ⚜ Code Snippet:

```python
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/rewrite-target: /
    cert-manager.io/cluster-issuer: my-cluster-issuer
spec:
  tls:
    - hosts:
        - example.com
      secretName: my-tls-secret
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-service
                port:
                  number: 80
```

# **📍** Conclusion:

Kubernetes storage and security are vital aspects of managing and securing your containerized applications. By understanding and implementing Persistent Volumes, Persistent Volume Claims, Storage Classes, StatefulSets, RBAC, Pod Security Policies, Secrets, Network Policies, and TLS, you can ensure data persistence, granular access control, and enhanced network security within your Kubernetes clusters. Stay updated with best practices and security guidelines to ensure the continued robustness and protection of your Kubernetes deployments.