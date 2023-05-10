---
title: "Understanding Kubernetes Ingress and SSL Routing for Secure and Scalable Deployments"
datePublished: Wed May 10 2023 14:49:06 GMT+0000 (Coordinated Universal Time)
cuid: clhhtgfue000109l19nrydcvm
slug: understanding-kubernetes-ingress-and-ssl-routing-for-secure-and-scalable-deployments
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683730050725/59cf39e2-18b0-4db6-b1d2-520802073dda.png
tags: software-development, aws, developer, devops, beginners

---

## **📍 Introduction:**

Kubernetes has become one of the most popular container orchestration platforms out there and with good reason. It simplifies the process of deploying and managing containers, making it easier to build and deploy applications. One of the key components of Kubernetes is Ingress, which allows you to route traffic to different services within your cluster.

In this guide, we will cover all the important aspects of Kubernetes Ingress, including Ingress routing, path-based routing, Ingress controller, unsecure and secure Ingress, SSL offloading, SSL bridging, comparison between SSL Passthrough, SSL-Offloading/Termination, and SSL-Bridge/Re-encrypt, OpenShift routes, TLS secrets, and provide code snippets to perform practical tasks.

## **🔹** Ingress Routing

Ingress routing is the process of directing traffic to the correct backend service based on the incoming request. Ingress routing can be performed based on the URL path or the host name in the request. For example, consider the following Ingress rule:

```plaintext
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        backend:
          serviceName: app1-service
          servicePort: 80
      - path: /app2
        backend:
          serviceName: app2-service
          servicePort: 80
```

In this example, requests to [`example.com/app1`](http://example.com/app1) will be directed to the `app1-service` and requests to [`example.com/app2`](http://example.com/app2) will be directed to the `app2-service`.

## **🔹** Path-based Routing:

Path-based routing is a type of Ingress routing where requests are directed to backend services based on the URL path in the request. Path-based routing is useful when multiple services are exposed under the same domain name. For example, consider the following Ingress rule:

```plaintext
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        backend:
          serviceName: app1-service
          servicePort: 80
      - path: /app2
        backend:
          serviceName: app2-service
          servicePort: 80
```

In this example, requests to [`example.com/app1`](http://example.com/app1) will be directed to the `app1-service` and requests to [`example.com/app2`](http://example.com/app2) will be directed to the `app2-service`.

## **🔹**Ingress Controller

An Ingress Controller is a Kubernetes resource that manages Ingress rules and directs traffic to the appropriate backend service. There are several Ingress Controllers available, such as Nginx, Traefik, and Istio. Each Ingress Controller has its own set of features and configuration options.

## **🔹** Unsecure and Secure Ingress

In Kubernetes, you can configure Ingress to accept both unsecured (HTTP) and secured (HTTPS) traffic. Unsecured traffic can be used for testing and development purposes, while secured traffic is used in production environments.

## **🔹** SSL Offloading

SSL Offloading is a method of decrypting SSL/TLS traffic at the Ingress Controller and forwarding unencrypted traffic to the backend service. SSL Offloading is useful when you have multiple backend services that require SSL/TLS encryption, as it reduces the overhead of encrypting and decrypting traffic at each service.

## **🔹** SSL Bridging

SSL Bridging is a method of decrypting SSL/TLS traffic at the Ingress Controller and re-encrypting the traffic before forwarding it to the backend service. SSL Bridging is useful when you have backend services that require SSL/TLS encryption, but do not support SSL/TLS termination.

Comparison between SSL Passthrough, SSL-Offloading/Termination, and SSL-Bridge/Re-encrypt

SSL Passthrough is a method of forwarding SSL/TLS traffic directly to the backend service without decrypting it at the Ingress Controller. SSL Passthrough is useful when you have backend services that require SSL/TLS encryption and do not support SSL/TLS termination.

SSL-Offloading/Termination, SSL Bridging, and SSL Passthrough are three different approaches to handling SSL/TLS traffic in Kubernetes. SSL Offloading/Termination and SSL Bridging provide better performance, but may not be suitable for all use cases. SSL Passthrough provides better security but may be slower than SSL Offloading/Termination and SSL Bridging.

## **🔹** OpenShift Routes

OpenShift is a Kubernetes-based platform that provides additional features for enterprise environments. One of these features is Routes, which are similar to Ingress but provide additional functionality such as automatic SSL certificate management.

## **🔹** TLS Secrets

In Kubernetes, TLS secrets are used to store SSL/TLS certificates and keys for secured Ingress traffic. TLS secrets can be created manually or automatically using services such as Let's Encrypt.

Let's take a closer look at how to configure Ingress in Kubernetes and OpenShift.

## **🔹** Configuring Ingress in Kubernetes

To configure Ingress in Kubernetes, you need to create an Ingress resource and specify the rules for routing traffic. Here is an example of an Ingress resource that routes traffic to two different services based on the path of the request:

```plaintext
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              name: http
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-service
            port:
              name: http
```

In this example, traffic that matches the path "/app1" is routed to the service "app1-service", and traffic that matches the path "/app2" is routed to the service "app2-service".

## **🔹** Configuring Ingress in OpenShift

To configure Ingress in OpenShift, you can use the Routes resource. Here is an example of a Route resource that routes traffic to a service based on the path of the request:

```plaintext
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: example-route
spec:
  host: example.com
  to:
    kind: Service
    name: app-service
  path: /app
  port:
    targetPort: http
```

In this example, traffic that matches the path "/app" is routed to the service "app-service".

## **🔹** TLS Secrets in Kubernetes and OpenShift

To enable secured Ingress traffic, you need to create TLS secrets that store SSL/TLS certificates and keys. Here is an example of a TLS secret that contains a self-signed SSL/TLS certificate and key:

```plaintext
apiVersion: v1
kind: Secret
metadata:
  name: tls-secret
type: kubernetes.io/tls
data:
  tls.crt: base64-encoded-certificate
  tls.key: base64-encoded-key
```

In this example, the certificate and key are base64-encoded and stored in the "tls.crt" and "tls.key" fields.

## **📍** Conclusion

Ingress is an essential component of Kubernetes that allows you to route external traffic to internal services. In this guide, we covered the basics of Ingress routing, path-based routing, Ingress Controller, unsecure and secure Ingress, SSL offloading, SSL bridging, comparison between SSL Passthrough, SSL-Offloading/Termination, and SSL-Bridge/Re-encrypt, OpenShift routes, TLS secrets, and provided code snippets to perform practical tasks.

When configuring Ingress in Kubernetes or OpenShift, it's important to consider the security and performance requirements of your applications. SSL Offloading/Termination and SSL Bridging provide better performance, but may not be suitable for all use cases. SSL Passthrough provides better security, but may be slower than SSL Offloading/Termination and SSL Bridging.

With the knowledge gained from this guide, you should now be able to configure Ingress for your Kubernetes or OpenShift cluster and ensure that your applications are accessible and secured. Additionally, it's worth noting that there are many Ingress Controllers available for Kubernetes, each with its own strengths and weaknesses. Some popular options include Nginx, Traefik, and Istio. It's important to choose an Ingress Controller that meets your specific requirements and fits well with your overall architecture.

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**https://github.com/sumanprasad007**](https://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683348228748/f0f7768f-11d6-4395-9519-c82cdd645149.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")