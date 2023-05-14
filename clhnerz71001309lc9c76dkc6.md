---
title: "Kubernetes Custom Resources | Custom Resources Definition (CRD) | Custom Controller"
datePublished: Sun May 14 2023 12:44:47 GMT+0000 (Coordinated Universal Time)
cuid: clhnerz71001309lc9c76dkc6
slug: kubernetes-custom-resources-custom-resources-definition-crd-custom-controller
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684067884060/9dbd8677-0b54-4c02-a4d7-4f4c54550177.jpeg
tags: software-development, aws, developer, devops, beginners

---

## **📍 Introduction**

Kubernetes is an open-source platform for managing containerized applications across a cluster of nodes. It provides a variety of built-in resources that can be used to define and manage applications. However, there may be cases where the built-in resources may not meet your specific requirements. In such cases, you can create Custom Resources and Controllers to extend Kubernetes functionality to meet your specific use cases. In this blog, we will discuss Custom Resources, Custom Resource Definitions, and Custom Controllers in Kubernetes and their use cases.

## **🔹** What is a Custom Resource?

---

A Custom Resource is an extension of the Kubernetes API that allows you to define your own resource types and objects. Custom Resources are defined using Custom Resource Definitions (CRDs) and can be managed using Kubernetes controllers. Custom Resources are typically used to represent applications, services, or resources that are not already represented by the built-in Kubernetes resources.

For example, let's say you want to create a Custom Resource to represent a database instance that you want to deploy in your Kubernetes cluster. You can define a Custom Resource for the database instance and use it to manage the lifecycle of the database instance within your cluster.

## **🔹** Why do you need a Custom Resource in Kubernetes?

---

Custom Resources provide a way to extend Kubernetes functionality to meet your specific use cases. By defining your own Custom Resources, you can represent any application or service that is not already represented by the built-in Kubernetes resources.

Custom Resources also provide a consistent interface for managing custom resources across multiple Kubernetes clusters. You can use the same Custom Resource Definition (CRD) to define your custom resource across different Kubernetes clusters, which makes it easier to manage your resources consistently.

## **🔹** What is a Custom Resource Definition?

---

A Custom Resource Definition (CRD) is a Kubernetes object that defines the structure and behavior of a Custom Resource. A CRD is used to define the API schema for your Custom Resource and how it can be accessed and manipulated.

The CRD defines the following attributes of a Custom Resource:

* The name of the Custom Resource
    
* The version of the Custom Resource
    
* The schema of the Custom Resource
    
* The storage location of the Custom Resource
    
* The behaviour of the Custom Resource
    

Once a CRD is defined, Kubernetes can use it to validate Custom Resource objects and manage them using Custom Controllers.

## **🔹** What is a Custom Controller?

---

A Custom Controller is a Kubernetes component that manages the lifecycle of a Custom Resource. A Custom Controller watches for changes to Custom Resources and takes actions based on those changes. For example, a Custom Controller can create or delete pods based on changes to Custom Resources.

Custom Controllers are typically implemented as Kubernetes controllers, which are Kubernetes objects that monitor resources and reconcile the desired state with the current state. Custom Controllers can be written in any programming language and can use the Kubernetes API to manage Custom Resources.

## **🔹** How to write a Custom Controller in Kubernetes?

---

To write a Custom Controller in Kubernetes, you need to define the following components:

* The Custom Resource Definition (CRD) that defines the structure and behavior of the Custom Resource.
    
* The Custom Controller that watches for changes to the Custom Resource and takes actions based on those changes.
    

To write a Custom Controller in Kubernetes, we need to perform the following steps:

1. Watch for changes to the Custom Resource using the Kubernetes API
    
2. Parse the Custom Resource and take action based on its state
    
3. Create, update, or delete Kubernetes resources based on the state of the Custom Resource
    

Here's an example of how to write a Custom Controller in Python using the Kubernetes Python client:

```plaintext
from kubernetes import client, config, watch

# Load Kubernetes configuration
config.load_incluster_config()

# Create Kubernetes API clients
api = client.CoreV1Api()
custom_api = client.CustomObjectsApi()

# Define the Custom Controller
class MyResourceController:
    def __init__(self):
        self.watch = watch.Watch()

    def run(self):
        # Watch for changes to the Custom Resource
        for event in self.watch.stream(custom_api.list_cluster_custom_object, "example.com", "v1", "myresources"):
            # Get the Custom Resource
            custom_resource = event['object']

            # Take action based on the state of the Custom Resource
            if custom_resource['status']['phase'] == "Running":
                # Create a Service to expose the Custom Resource
                service = client.V1Service()
                service.metadata = client.V1ObjectMeta(name=custom_resource['metadata']['name'])
                service.spec = client.V1ServiceSpec(selector={"app": custom_resource['metadata']['name']}, ports=[client.V1ServicePort(port=80, target_port=8080)])
                api.create_namespaced_service(namespace=custom_resource['metadata']['namespace'], body=service)
            elif custom_resource['status']['phase'] == "Failed":
                # Delete the Service that exposed the Custom Resource
                api.delete_namespaced_service(name=custom_resource['metadata']['name'], namespace=custom_resource['metadata']['namespace'])

# Run the Custom Controller
controller = MyResourceController()
controller.run()
```

In this example, we create a Custom Controller that watches for changes to a Custom Resource named "MyResource". When the Custom Resource enters the "Running" phase, the Custom Controller creates a new Service to expose the Custom Resource. When the Custom Resource enters the "Failed" phase, the Custom Controller deletes the Service that exposed the Custom Resource. The Custom Controller is implemented using the Kubernetes Python client.

To deploy this Custom Controller in Kubernetes, we need to create a Deployment or a StatefulSet that runs the Custom Controller as a Pod. The Pod should have access to the Kubernetes API to interact with the cluster. We can use a Kubernetes ServiceAccount and a Kubernetes RoleBinding to grant the Pod access to the Kubernetes API.

## **🔹** Comparison with the native Kubernetes Resources

---

Custom Resources can be compared to the native Kubernetes resources in the following ways:

* Built-in resources such as Pods, Services, and Deployments are well-defined and provide a consistent interface for managing applications in Kubernetes. Custom Resources, on the other hand, provide a way to extend Kubernetes functionality to meet specific use cases.
    
* Built-in resources have well-defined behaviours and can be managed using built-in controllers. Custom Resources require Custom Controllers to be implemented to manage their lifecycle.
    
* Built-in resources are typically well-tested and have a large community of users. Custom Resources require additional testing and may have a smaller community of users.
    

Native Kubernetes Controllers are built-in controllers that manage the lifecycle of Native Kubernetes Resources. For example, the Deployment Controller manages the lifecycle of Deployments, and the Service Controller manages the lifecycle of Services.

Custom Controllers, on the other hand, are user-defined controllers that manage the lifecycle of Custom Resources. Custom Controllers are built using the Kubernetes API and are responsible for creating, updating, and deleting Custom Resources based on their state. Native Kubernetes Controllers have well-defined logic and follow established patterns for managing the lifecycle of Native Kubernetes Resources. Custom Controllers, on the other hand, require custom logic to manage the lifecycle of Custom Resources.

## **📍** Conclusion

Custom Resources and Controllers provide a way to extend Kubernetes functionality to meet your specific use cases. By defining your own Custom Resources, you can represent any application or service that is not already represented by the built-in Kubernetes resources. Custom Controllers can be used to manage the lifecycle of Custom Resources. We hope this blog post has provided you with an in-depth understanding of Custom Resources, Custom Resource Definitions, and Custom Controllers in Kubernetes.

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683909716692/b6161a02-f32e-4061-b3e2-cd707c70e44e.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")