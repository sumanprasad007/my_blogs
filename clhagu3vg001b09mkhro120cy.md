---
title: "Kubernetes Services Deep Dive| Demonstration Steps| Learn Traffic Flow Using Kubershark"
datePublished: Fri May 05 2023 11:21:26 GMT+0000 (Coordinated Universal Time)
cuid: clhagu3vg001b09mkhro120cy
slug: kubernetes-services-deep-dive-demonstration-steps-learn-traffic-flow-using-kubershark
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683285659223/9a70ede6-13d3-49c8-91b0-d2e7ac96c21d.png
tags: software-development, aws, developer, devops, beginners

---

# **📍 Introduction:**

## 🔹 What are Kubernetes Services?

Kubernetes services provide an abstraction layer that decouples the frontend of an application from its backend pods. They enable seamless communication and load balancing between pods, ensuring high availability and scalability. Services are assigned a unique IP address and DNS name within the cluster, allowing other components to discover and access them easily.

### ⚜ Code Snippet: Creating a ClusterIP service in Kubernetes

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

In the above example, we define a ClusterIP service named "my-service" that selects pods with the label "app: my-app" and exposes port 80. The service is configured to forward traffic to the pods' port 8080.

### ⚜ Types of Kubernetes Services:

Kubernetes supports different types of services to cater to various networking requirements:

* ClusterIP: The default type, only accessible within the cluster.
    
* NodePort: Exposes the service on a static port on each cluster node.
    
* LoadBalancer: Provides an externally accessible IP address through a cloud provider's load balancer.
    
* ExternalName: Maps service to an external DNS name.
    

## Understanding how Kubectl & API Server works:

When you run `kubectl` commands, it communicates with the Kubernetes API server to execute the requested operations. Here's an overview of the process:

1. `kubectl` reads the Kubernetes configuration file (`kubeconfig`) located at `$HOME/.kube/config` by default, unless specified otherwise using the `--kubeconfig` flag.
    
2. The configuration file contains information about the Kubernetes cluster, including the API server's URL, authentication details, and the cluster context.
    
3. `kubectl` uses the configuration to determine the API server's address and establishes a secure connection (HTTPS) using Transport Layer Security (TLS).
    
4. Once connected, `kubectl` sends the appropriate HTTP request to the API server based on the command you executed (e.g., `GET /api/v1/pods` for `kubectl get pods`).
    
5. The API server receives the request, authenticates the client (e.g., using client certificates, bearer tokens, or other authentication methods), and validates the authorization to perform the requested operation.
    
6. If authorized, the API server retrieves the requested information or performs the requested action on the Kubernetes cluster.
    
7. The API server sends the response back to `kubectl`, which then formats and displays the output to the user.
    

Essentially, `kubectl` acts as a command-line interface to interact with the Kubernetes API server, allowing you to manage and operate your cluster using various commands and options. Now, let's move on to accessing your application using NodePort mode with the assigned port.

## 🔹 Accessing Application using Service as Nodeport Port:

When you expose a service in Kubernetes using the NodePort type, it allocates a specific port on each cluster node to route traffic to the service. Here's how you can access your application using NodePort mode with Minikube:

1. Start by ensuring that Minikube is running and your application deployment and service are configured correctly.
    
2. Retrieve the Minikube IP address using the following command:
    
    ```plaintext
    minikube ip
    ```
    
    The command will output the IP address of your Minikube cluster, such as `192.168.49.2`.
    
3. Use the assigned NodePort of your service along with the Minikube IP address to access your application. If your service has been assigned NodePort `30080`, you can access it at `http://<Minikube-IP>:30080`. For example, if the Minikube IP address is `192.168.49.2`, you would access the application at [`http://192.168.49.2:30080`](http://192.168.49.2:30080).
    
    Note: The port number (`30080` in this example) depends on the assigned NodePort value for your service.
    

By following these steps, you can access your application running in the Kubernetes cluster using NodePort mode by providing the Minikube IP address with the assigned port. To further demonstrate how to access your application using NodePort mode with Minikube, let's provide a code snippet that showcases the process.

### ⚜ Code Snippet for Service Type NodePort

```plaintext
# Step 1: Start Minikube (if not already running)
minikube start

# Step 2: Deploy your application
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Step 3: Get the NodePort assigned to the service
kubectl get service <service-name>

# Step 4: Access your application using the Minikube IP and assigned NodePort
minikube ip
# Note down the Minikube IP address (e.g., 192.168.49.2)

# Combine the Minikube IP and assigned NodePort to access the application
# Replace <NodePort> with the assigned NodePort and <Minikube-IP> with the Minikube IP address
http://<Minikube-IP>:<NodePort>
```

In the above code snippet, we assume that you have a Kubernetes deployment and service defined in `deployment.yaml` and `service.yaml`, respectively. Replace `<service-name>` with the actual name of your service.

By following these steps, you can deploy your application, retrieve the assigned NodePort using `kubectl get service`, obtain the Minikube IP using `minikube ip`, and then access your application using the combination of the Minikube IP and assigned NodePort.

This approach allows external access to your application running inside the Minikube cluster through the specified NodePort. Ensure that the necessary network settings, such as firewall rules or network routing, are configured to allow incoming traffic on the specified NodePort. With this setup, you can access your application in the Minikube cluster using the provided Minikube IP address and NodePort combination. Let's explore how to access your application from the outside world using the LoadBalancer mode by modifying the service type and discussing service discovery functionality.

## 🔹 Accessing Your Application Using LoadBalancer Mode:

To expose your application to the outside world using the LoadBalancer mode, you can modify the service type from NodePort to LoadBalancer in the service definition. However, please note that this functionality is typically available when using Kubernetes on a cloud a service provider like AWS (EKS), Azure (AKS), or Google Cloud (GKE) since they provide integrated load balancers.

Here are the steps to modify the service type and obtain the public IP using a cloud provider:

### ⚜ Code Snippet for Service Type LoadBalancer

```plaintext
# Step 1: Edit the service configuration
kubectl edit svc <service-name>
```

This command opens the service definition in the default text editor.

```plaintext
# Step 2: Change the service type from NodePort to LoadBalancer
apiVersion: v1
kind: Service
metadata:
  name: <service-name>
spec:
  type: LoadBalancer
  ...
```

Modify the `type` field from `NodePort` to `LoadBalancer` in the service definition and save the changes.

```plaintext
# Step 3: Verify the service's external IP
kubectl get svc <service-name>
```

The command above retrieves the service details, including the external IP assigned by the cloud provider's load balancer.

With the updated service configuration and the assigned external IP, your application is now accessible from the outside world. Please note that the process may vary slightly depending on the cloud provider you are using. Ensure that you have the necessary permissions and configurations set up with your cloud provider to enable the LoadBalancer service type.

## 🔹 Service Discovery Functionality:

In Kubernetes, service discovery allows other components within the cluster to locate and communicate with services. It relies on the labels and selectors defined in the service and pod configurations.

When you create a service, you specify the selector field in the service definition, which defines a label selector to match the pods that the service should route traffic to. If the labels and selectors are not properly aligned, you won't be able to reach your application through the service.

For example, consider the following service definition:

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

In this case, the service expects pods with the label `app: my-app` to be available. If you change the label of the pods or use a different selector in the service definition, the service won't be able to discover and route traffic to the pods correctly.

It's crucial to ensure that the labels and selectors are consistent between the service and the pods for proper service discovery and communication within the Kubernetes cluster. By following the steps above and understanding the service discovery functionality, you can expose your application to the outside world using the LoadBalancer mode and ensure proper communication within the cluster.

## 🔹 Explaining the Load-Balancing Functionality with KubeShark:

First, let's install and run KubeShark to observe the load-balancing behavior of a Kubernetes service:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683284014944/dae60ae4-9f41-4141-8229-543e502567cd.png align="center")

### ⚜ Step 1: Install KubeShark

```plaintext
# Install KubeShark using pip
pip install kubeshark
```

### ⚜ Step 2: Run KubeShark

```plaintext
# Start KubeShark and tap into all pods within the cluster
kubeshark tap -A
```

Running the `kubeshark tap -A` command starts the KubeShark application and captures the network traffic between pods in the Kubernetes cluster.

### ⚜ Step 3: Access KubeShark UI

By default, KubeShark exposes its UI on port 8899. You can access it by opening a web browser and navigating to `http://<Minikube-IP>:8899`. Replace `<Minikube-IP>` with the IP address of your Minikube cluster.

Once you have accessed the KubeShark UI, you will be able to visualize and analyze the captured network traffic within the cluster.

### ⚜ Step 4: Observe Load-Balancing Behavior

By hitting the Minikube IP address from an external client, you can observe the load-balancing behavior of the Kubernetes service through KubeShark.

When the external client sends requests to the Minikube IP, the service's load balancer distributes the incoming traffic among the available pods that match the service's selector. This load-balancing behavior ensures that the traffic is evenly distributed across the pods, improving the scalability and availability of your application.

In KubeShark, you can see the captured network packets corresponding to the requests and responses exchanged between the external client and the pods. Analyzing the packet details and flow visualization, you can observe how the load balancer redirects traffic between the pods to achieve load balancing.

By using KubeShark to capture and analyze network traffic, you can gain insights into the load-balancing behavior of Kubernetes services and understand how traffic is distributed among the pods within your cluster.

# **📍 Conclusion:**

1. Kubernetes Services Deep Dive:
    
    * Kubernetes services provide stable network endpoints for accessing and communicating with applications running in a Kubernetes cluster.
        
    * Services enable load balancing, service discovery, and routing of network traffic to pods based on labels and selectors.
        
    * Service types include ClusterIP, NodePort, and LoadBalancer, each serving different purposes and providing different access methods.
        
2. Live Demo - Learn Traffic Flow Using KubeShark:
    
    * KubeShark is a traffic analysis and visualization tool for Kubernetes clusters.
        
    * By installing and running KubeShark with the `kubeshark tap -A` command, you can capture and analyze network traffic between pods.
        
    * Accessing the KubeShark UI allows you to observe the load-balancing behavior of Kubernetes services and how traffic is distributed among pods.
        
3. Accessing Applications using NodePort Mode:
    
    * NodePort mode allows external access to applications running in a Kubernetes cluster by assigning a specific port on each cluster node.
        
    * To access an application using NodePort mode, you need to retrieve the Minikube IP address and combine it with the assigned NodePort.
        
4. Accessing Applications using LoadBalancer Mode:
    
    * LoadBalancer mode exposes applications to the outside world using cloud provider load balancers.
        
    * By modifying the service type from NodePort to LoadBalancer and using the cloud provider's load balancer, you can obtain a public IP to access your application.
        
5. Service Discovery Functionality:
    
    * Service discovery in Kubernetes allows components within the cluster to locate and communicate with services.
        
    * Labels and selectors play a crucial role in service discovery, ensuring that services correctly route traffic to pods with matching labels.
        

Understanding these topics provides a comprehensive understanding of how Kubernetes services work, how traffic flows within the cluster, and how to access applications from the outside world. By leveraging these concepts, you can effectively manage and scale your applications in Kubernetes clusters.

# **📍 Resources:**

%[https://www.youtube.com/watch?v=fCX8O7GA_lY]