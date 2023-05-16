---
title: "Kubernetes Live Project | Configmaps & Secrets | How To Use Configmaps & Secrets Inside Pod"
datePublished: Tue May 16 2023 04:23:50 GMT+0000 (Coordinated Universal Time)
cuid: clhprrg7f000309l5fuwk9q21
slug: kubernetes-live-project-configmaps-secrets-how-to-use-configmaps-secrets-inside-pod
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684086007815/e7a4693b-2472-4372-a570-4178c879c5df.png
tags: software-development, aws, developer, devops, beginners

---

## **📍** Introduction:

Kubernetes is an open-source container orchestration platform that allows you to manage containerized applications at scale. One of the important features of Kubernetes is the ability to store configuration data as ConfigMaps and Secrets.

In this article, we will cover how to use ConfigMaps and Secrets inside Pods in Kubernetes. We will also demonstrate how to create ConfigMaps and Secrets in a live Kubernetes project using code snippets and examples.

## **🔹** What are ConfigMaps and Secrets?

ConfigMaps are Kubernetes object that allows you to store configuration data as key-value pairs or as files. You can use ConfigMaps to store configuration data such as environment variables, command-line arguments, and configuration files.

Secrets are similar to ConfigMaps, but they are specifically designed to store sensitive data such as passwords, tokens, and keys. Secrets are base64-encoded before they are stored in Kubernetes, and they are only accessible to authorized users.

## **🔹** Using ConfigMaps and Secrets in Pods:

You can use ConfigMaps and Secrets in Pods to provide configuration data and sensitive data to your applications. In order to use ConfigMaps and Secrets in Pods, you need to define them as volumes in your Pod specification.

Defining a ConfigMap volume in your Pod:

To define a ConfigMap volume in your Pod, you need to add a volume to your Pod specification with the type "configMap". You also need to specify the name of the ConfigMap you want to use and the key that you want to use as the volume.

### ⚜ Code for Pod specification that uses a ConfigMap:

```plaintext
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: mycontainer
      image: myimage
      volumeMounts:
        - name: config
          mountPath: /etc/config
  volumes:
    - name: config
      configMap:
        name: myconfigmap
        items:
          - key: mykey
            path: mykey
```

In this example, we define a ConfigMap volume with the name "config" and the ConfigMap "myconfigmap". We also specify the key "mykey" as the volume.

## **🔹** Defining a Secret volume in your Pod:

To define a Secret volume in your Pod, you need to add a volume to your Pod specification with the type "secret". You also need to specify the name of the Secret you want to use and the key that you want to use as the volume.

### ⚜ Code for Pod specification that uses a Secret:

```plaintext
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: mycontainer
      image: myimage
      volumeMounts:
        - name: secret
          mountPath: /etc/secret
  volumes:
    - name: secret
      secret:
        secretName: mysecret
        items:
          - key: mykey
            path: mykey
```

In this example, we define a Secret volume with the name "secret" and the Secret "mysecret". We also specify the key "mykey" as the volume.

## **🔹** Creating ConfigMaps and Secrets in a live Kubernetes project:

Now that we have covered how to use ConfigMaps and Secrets in Pods, let's see how to create ConfigMaps and Secrets in a live Kubernetes project.

### ⚜ Creating a ConfigMap:

To create a ConfigMap, you can use the "kubectl create configmap" command. Here's an example of how to create a ConfigMap from a file:

```plaintext
kubectl create configmap myconfigmap --from-file=config-file.properties
```

In this example, we create a ConfigMap with the name "myconfigmap" from the file "config-file properties". The key in the ConfigMap will be the file name ("[config-file.properties](http://config-file.properties)") and the value will be the contents of the file.

You can also create a ConfigMap from literal values using the "--from-literal" flag. Here's an example:

```plaintext
kubectl create configmap myconfigmap --from-literal=mykey=myvalue
```

In this example, we create a ConfigMap with the name "myconfigmap" with a key "mykey" and a value "myvalue".

## **🔹** Creating a Secret:

To create a Secret, you can use the "kubectl create secret" command. Here's an example of how to create a Secret from a file:

```plaintext
kubectl create secret generic mysecret --from-file=key.pem --from-file=cert.pem
```

In this example, we create a Secret with the name "mysecret" from two files "key.pem" and "cert.pem". The keys in the Secret will be the file names ("key.pem" and "cert.pem") and the values will be the contents of the files.

### ⚜ Secret from literal values using the "--from-literal" flag

```plaintext
kubectl create secret generic mysecret --from-literal=mykey=myvalue
```

In this example, we create a Secret with the name "mysecret" with a key "mykey" and a value "myvalue".

## **🔹 Crucial points to revise**

1. What is a Kubernetes ConfigMap?
    

A ConfigMap is an object in Kubernetes that provides a way to store configuration data in key-value pairs. It can be used to store configuration data for an application or a cluster, such as environment variables, command-line arguments, configuration files, and other types of data.

1. What is a Kubernetes Secret?
    

A Secret is an object in Kubernetes that provides a way to store sensitive data, such as passwords, authentication tokens, and other types of data. Secrets are stored in a similar way to ConfigMaps, using key-value pairs, but are encrypted and can only be accessed by authorized users.

1. Difference between ConfigMap & Secret?
    

The main difference between ConfigMaps and Secrets is that ConfigMaps are used to store non-sensitive configuration data, while Secrets are used to store sensitive data that should not be exposed to unauthorized users.

ConfigMaps are stored in plaintext and can be accessed by anyone with access to the Kubernetes API, while Secrets are stored encrypted and can only be accessed by authorized users.

1. How to use ConfigMap data as ENV Vars inside a Django Python Container?
    

To use ConfigMap data as environment variables inside a Django Python container, you can create a ConfigMap object with the key-value pairs of the environment variables and mount it as an environment variable in the container.

Here's an example YAML file that creates a ConfigMap object with two key-value pairs:

```plaintext
apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfigmap
data:
  DB_HOST: mydbhost
  DB_PORT: '5432'
```

You can then mount this ConfigMap as environment variables in the container by adding the following section to the Pod spec:

```plaintext
spec:
  containers:
  - name: mycontainer
    image: myimage
    envFrom:
    - configMapRef:
        name: myconfigmap
```

This will mount the ConfigMap as environment variables with the keys as the environment variable names and the values as the environment variable values.

1. How to use Configmap data as Volume Mount file inside a Django Python container App?
    

To use ConfigMap data as a file inside a Django Python container, you can create a ConfigMap object with the key-value pair of the file contents and mount it as a volume in the container.

Here's an example YAML file that creates a ConfigMap object with a key-value pair of a configuration file:

```plaintext
apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfigmap
data:
  config.ini: |
    [db]
    host = mydbhost
    port = 5432
```

You can then mount this ConfigMap as a volume in the container by adding the following section to the Pod spec:

```plaintext
spec:
  containers:
  - name: mycontainer
    image: myimage
    volumeMounts:
    - name: config-volume
      mountPath: /app/config.ini
      subPath: config.ini
  volumes:
  - name: config-volume
    configMap:
      name: myconfigmap
```

This will mount the ConfigMap as a file inside the container at the mount path `/app/config.ini`.

1. What are the advantages of using a Volume Mount over Env var for reading ConfigMap in Kubernetes?
    

Using a volume mount to read ConfigMap data in Kubernetes has several advantages over using environment variables:

* Environment variables have a size limit, while ConfigMaps can store larger amounts of data.
    
* Using a volume mount allows you to preserve the original file structure and format of the data, while environment variables require you to convert the data to a string
    
* Using a volume mount allows you to modify the ConfigMap data without having to rebuild and redeploy the container, while environment variables require you to rebuild and redeploy the container every time the data changes.
    
* Using a volume mount also allows you to use the data in other ways, such as sharing the data between containers or using it as a configuration file for a service.
    

1. Interview Questions related to Secrets in Kubernetes?
    

Q1. What is the difference between a ConfigMap and a Secret in Kubernetes? A1. ConfigMaps are used to store non-sensitive configuration data, while Secrets are used to store sensitive data that should not be exposed to unauthorized users. ConfigMaps are stored in plaintext and can be accessed by anyone with access to the Kubernetes API, while Secrets are stored encrypted and can only be accessed by authorized users.

Q2. How are Secrets stored in Kubernetes? A2. Secrets are stored in Kubernetes as base64-encoded strings. When a Secret is accessed by a container, it is automatically decoded into its original form.

Q3. How can you create a Secret in Kubernetes? A3. You can create a Secret in Kubernetes using the `kubectl create secret` command or by creating a YAML file that defines the Secret and using the `kubectl apply` command to apply it to the cluster.

Q4. How can you use a Secret in a container? A4. You can use a Secret in a container by mounting it as a volume or as environment variables. When mounted as a volume, the Secret data is available as files inside the container. When used as environment variables, the Secret data is available as environment variables inside the container.

Q5. How can you update a Secret in Kubernetes? A5. You can update a Secret in Kubernetes by using the `kubectl edit secret` command or by creating a new YAML file that defines the updated Secret and using the `kubectl apply` command to apply it to the cluster. When a Secret is updated, any pods that use the Secret will automatically receive the updated data.

## **📍** Conclusion:

In this article, we have covered how to use ConfigMaps and Secrets inside Pods in Kubernetes. We have also demonstrated how to create ConfigMaps and Secrets in a live Kubernetes project using code snippets and examples.

ConfigMaps and Secrets are powerful tools for managing configuration data and sensitive data in Kubernetes. They allow you to store data separately from your application code, making it easier to manage and maintain your applications. Kubernetes ConfigMaps and Secrets are powerful tools for managing configuration data and sensitive data in Kubernetes. ConfigMaps provide an easy way to store and access non-sensitive configuration data, while Secrets provide a secure way to store and access sensitive data. By understanding the differences between ConfigMaps and Secrets and how to use them in a Kubernetes cluster, you can streamline your deployment process and ensure that your application is running securely and efficiently.

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683909716692/b6161a02-f32e-4061-b3e2-cd707c70e44e.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")