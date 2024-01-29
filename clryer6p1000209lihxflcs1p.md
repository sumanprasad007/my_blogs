---
title: "Kubernetes Cheat Sheet - A Perfect Companion to All Your Cluster Management Needs"
datePublished: Mon Jan 29 2024 04:06:42 GMT+0000 (Coordinated Universal Time)
cuid: clryer6p1000209lihxflcs1p
slug: kubernetes-cheat-sheet-a-perfect-companion-to-all-your-cluster-management-needs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706500988868/c282464b-52a2-415b-b51d-7d30f2e50a30.png
tags: linux, aws, technology, python, web-development, kubernetes, developer, devops, terraform, aws-lambda, kunalkushwaha, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge, kubeweekchallenge

---

Hey Kubernetes enthusiasts! 🚀 Today, we're thrilled to share an incredible Kubernetes Cheat Sheet that covers all your cluster management needs. A big shoutout and thanks to Pragyanatvade for putting together this invaluable resource for the Kubernetes community! 🙌

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Checkout the below post for the full "Kubernetes Cheat Sheet Pdf"</div>
</div>

%[https://www.linkedin.com/posts/prasad-suman-mohan_kubernetes-cheat-sheet-activity-7157583140507529218-pPB2?utm_source=share&utm_medium=member_desktop] 

📜 **Cheat Sheet Sections:**

### Nodes:

* `kubectl get nodes`: List all nodes in the cluster.
    
* `kubectl describe node <node-name>`: Display detailed information about a specific node.
    

### Roles:

* `kubectl get roles`: List all roles in the cluster.
    
* `kubectl describe role <role-name>`: Get detailed information about a specific role.
    

### Pods:

* `kubectl get pods`: Display all pods in the current namespace.
    
* `kubectl describe pod <pod-name>`: Show details about a specific pod.
    

### Namespace:

* `kubectl get namespaces`: List all namespaces in the cluster.
    
* `kubectl create namespace <namespace-name>`: Create a new namespace.
    

### Deployment:

* `kubectl get deployments`: List all deployments in the current namespace.
    
* `kubectl describe deployment <deployment-name>`: View details of a specific deployment.
    

### DaemonSets:

* `kubectl get daemonsets`: List all daemon sets in the current namespace.
    
* `kubectl describe daemonset <daemonset-name>`: Show details of a specific daemon set.
    

### Events:

* `kubectl get events`: Display cluster events.
    
* `kubectl describe event <event-name>`: View details of a specific event.
    

### Logs:

* `kubectl logs <pod-name>`: Retrieve logs from a specific pod.
    

### Service Account:

* `kubectl get serviceaccounts`: List all service accounts in the current namespace.
    
* `kubectl describe serviceaccount <sa-name>`: Get details of a specific service account.
    

### ReplicaSet:

* `kubectl get replicasets`: List all replica sets in the current namespace.
    
* `kubectl describe replicasets <rs-name>`: Show details of a specific replica set.
    

### Multiple Resources:

* `kubectl apply -f <resource-file.yaml>`: Apply configurations from a YAML file.
    

### Secrets:

* `kubectl get secrets`: List all secrets in the current namespace.
    
* `kubectl describe secret <secret-name>`: Show details of a specific secret.
    

### ConfigMaps:

* `kubectl get configmaps`: List all config maps in the current namespace.
    
* `kubectl describe configmap <configmap-name>`: View details of a specific config map.
    

### Ingress:

* `kubectl get ingress`: List all ingresses in the current namespace.
    
* `kubectl describe ingress <ingress-name>`: Display details of a specific ingress.
    

### PV (Persistent Volume):

* `kubectl get pv`: List all persistent volumes in the cluster.
    
* `kubectl describe pv <pv-name>`: Show details of a specific persistent volume.
    

### PVC (Persistent Volume Claim):

* `kubectl get pvc`: List all persistent volume claims in the current namespace.
    
* `kubectl describe pvc <pvc-name>`: View details of a specific persistent volume claim.
    

### Storage Class:

* `kubectl get storageclass`: List all storage classes in the cluster.
    
* `kubectl describe storageclass <sc-name>`: Get details of a specific storage class.
    

### API Calls:

* `kubectl api-resources`: Display the available API resources.
    
* `kubectl get <resource>`: Fetch resources of a specific type.
    

### Cluster Info:

* `kubectl cluster-info`: Show details about the cluster.
    

### Taint:

* `kubectl taint nodes <node-name> key=value:effect`: Apply a taint to a node.
    

### Level:

* `kubectl get nodes --selector=<label-selector>`: Filter nodes by label.
    

### Other Scenarios:

* Explore advanced scenarios with `kubectl explain` and official Kubernetes documentation.
    

🌐 **Connect with us:**

* Follow Pragyanatvade for more Kubernetes insights.
    
* Mention @kubernetes in your Kubernetes journey.
    

A massive thank you again to Pragyanatvade for this fantastic Kubernetes Cheat Sheet! 🎉 Start optimizing your cluster management with these essential commands. Happy Kuberneting! 🚢🐳 #Kubernetes #CheatSheet #ClusterManagement #DevOps #ThankYouPragyanatvade