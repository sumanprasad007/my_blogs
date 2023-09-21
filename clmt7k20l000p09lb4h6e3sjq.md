---
title: "Custom Resource Definitions (CRDs): Extending Kubernetes 🚀"
datePublished: Thu Sep 21 2023 13:27:49 GMT+0000 (Coordinated Universal Time)
cuid: clmt7k20l000p09lb4h6e3sjq
slug: custom-resource-definitions-crds-extending-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695302831086/a779ff9d-2a4d-4d4b-b374-a8b4197368bf.gif
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

# **Introduction:**

Kubernetes has established itself as the de facto standard for container orchestration, making it easier than ever to manage and scale applications. Yet, every environment is unique, and one size does not always fit all. Enter Custom Resource Definitions (CRDs), a powerful feature that allows you to extend Kubernetes functionality by defining custom resources and controllers. In this blog post, we'll delve into CRDs, why they are needed, the problems they solve, and provide a real-time example with a step-by-step approach to create them. Let's get started! 🌟

## **Why Do We Need CRDs? 🤔**

Kubernetes provides a rich set of resources like Pods, Services, and ConfigMaps, but what if your application needs to manage something that Kubernetes doesn't natively support? This is where CRDs come to the rescue. They empower you to define your own custom resources, enabling you to model and manage domain-specific objects within Kubernetes.

### **The Problems CRDs Solve 🛠️**

#### 1\. Abstraction and Automation

Imagine you're running a microservices-based application, and you want to automate the provisioning of database instances for each microservice. Kubernetes itself doesn't have a built-in resource for databases, so you'd typically manage this manually or with external tools. CRDs allow you to create a "Database" custom resource, abstracting away the complexity and enabling automation through Kubernetes.

#### 2\. Consistency and Standardization

CRDs ensure consistency by providing a standardized way to define, configure, and manage your custom resources. This consistency is vital when you have multiple teams or clusters, as it reduces operational friction and potential errors.

#### 3\. Kubernetes-Native Experience

With CRDs, you can leverage Kubernetes' native tooling and commands to manage your custom resources. `kubectl` can be used to interact with custom resources just like built-in ones, offering a seamless experience for operators and developers.

## **A Real-Life Example: Creating a "Website" CRD 🌐**

Let's walk through creating a simple "Website" CRD to demonstrate how CRDs work in practice.

### **Step 1: Define the CRD YAML**

Create a YAML file, `website-crd.yaml`, with the following content:

```plaintext
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: websites.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
  scope: Namespaced
  names:
    plural: websites
    singular: website
    kind: Website
    shortNames:
      - web
```

In this YAML:

* `group` specifies the API group for our CRD.
    
* `versions` defines the API versions we support.
    
* `scope` specifies whether the custom resource is namespaced or cluster-wide.
    
* `names` defines the naming conventions for our custom resource.
    

### **Step 2: Apply the CRD**

Use `kubectl` to apply the CRD definition:

```plaintext
kubectl apply -f website-crd.yaml
```

### **Step 3: Create a Custom Resource**

Now, let's create a custom resource of type "Website." Create a file named `my-website.yaml` with the following content:

```plaintext
apiVersion: example.com/v1
kind: Website
metadata:
  name: my-website
spec:
  domain: www.example.com
  backend:
    serviceName: backend-service
    port: 80
```

Apply the custom resource:

```plaintext
kubectl apply -f my-website.yaml
```

### **Step 4: Verify and Interact**

You can now use `kubectl` to interact with your custom resource, just like any other Kubernetes resource:

```plaintext
kubectl get websites
kubectl describe website my-website
```

## **Conclusion 🎉**

Custom Resource Definitions are a powerful tool in the Kubernetes toolbox. They enable you to model and manage domain-specific resources, extending Kubernetes to fit your unique needs. By abstracting away complexity, ensuring consistency, and providing a Kubernetes-native experience, CRDs empower you to take control of your Kubernetes environment and automate tasks that were once manual. So go ahead, define your custom resources, and unlock the full potential of Kubernetes! 💪🏆

Happy Kubernetizing! 🚢🌟

### **🔍 Checkout GitHub Repository for projects:**

**🔗** [**linktr.ee/sumanprasad007**](http://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)