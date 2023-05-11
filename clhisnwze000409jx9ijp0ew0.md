---
title: "Introduction to Kubernetes RBAC"
datePublished: Thu May 11 2023 07:14:41 GMT+0000 (Coordinated Universal Time)
cuid: clhisnwze000409jx9ijp0ew0
slug: introduction-to-kubernetes-rbac
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683785014682/bac98ca4-d2f9-4f31-8130-93f3eeecbe4a.png
tags: software-development, aws, developer, devops, beginners

---

## **📍** Introduction to K8s RBAC:

Kubernetes (K8s) is an open-source platform for automating the deployment, scaling, and management of containerized applications. It is highly extensible and can be customized to suit the needs of different applications. One of the essential features of K8s is Role-Based Access Control (RBAC), which helps administrators manage access to resources in a cluster.

RBAC is a security mechanism that controls access to resources in K8s. It is a way of defining who can perform what actions on which resources. RBAC defines roles, which are a set of permissions that define what actions a user or group of users can perform on a specific resource.

In this blog, we will discuss RBAC in K8s and how to create and manage users and service accounts. We will also explore roles, role bindings, and identity providers.

## **📍** What is RBAC?

RBAC is a security mechanism that is used to control access to resources in K8s. It is based on the principle of least privilege, which means that a user or group of users should only have the necessary permissions to perform their tasks. RBAC uses roles to define what actions a user or group of users can perform on a specific resource.

## **🔹** How to create Users and how to do user management in Kubernetes?

  
In Kubernetes, users are typically created and managed through an external authentication system, such as an LDAP directory or an identity provider like Google or GitHub. These systems provide a way to authenticate users and allow them to access Kubernetes resources based on their assigned roles and permissions.

Once a user is authenticated, Kubernetes uses Role-Based Access Control (RBAC) to determine what resources the user can access and what actions they can perform on those resources. This allows cluster administrators to control who can access and modify the Kubernetes resources in the cluster.

Let's take a simple example to explain this to a non-IT person:

Suppose you are the owner of a company that has a Kubernetes cluster to host its applications. You have a team of developers who need access to the Kubernetes cluster to manage the applications. To give your developers access, you first need to create user accounts for them in an external authentication system, such as an LDAP directory or an identity provider. Once their user accounts are created, you can configure RBAC in Kubernetes to grant them the appropriate access to the cluster.

For example, you might create a Role in Kubernetes that allows users to read and list the pods in the cluster. You can then create a RoleBinding that assigns this Role to a group of users, such as your team of developers.

## **📍** Kubernetes Service Accounts:

In Kubernetes, a Service Account is an identity that allows a Pod to interact with the Kubernetes API server and other Kubernetes resources. Think of a Service Account as a way for a Pod to prove its identity and obtain permission to access resources in the cluster.

Here's a simple example to explain Service Accounts to a non-IT person:

Imagine you're a VIP attending a party at a club. To enter the club and access certain areas, you need to prove your identity by showing your ID and pass a security check. Once you're inside, you can use your VIP pass to access exclusive areas and services. In Kubernetes, a Pod is like a person at the party, and a Service Account is like a VIP pass. The Service Account allows the Pod to access certain areas and services in the cluster. The Pod can use the Service Account to prove its identity and obtain permission to access Kubernetes resources.

## **📍** Roles:

A role is a set of permissions that defines what actions a user or group of users can perform on a specific resource in a K8s cluster. A role is defined using a YAML file that specifies the rules for the role.

The following is an example of a role definition:

```plaintext
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: <role-name>
  namespace: <namespace>
rules:
- apiGroups: [""]
  resources: ["<resource>"]
  verbs: ["<verb>"]
```

This role definition allows the specified user or group of users to perform the specified verb on the specified resource.

## **📍** Role Bindings:

A role binding is a Kubernetes resource that binds a role to a user, group of users, or service account. A role binding allows a user or service account to perform the actions defined in the role.

The following is an example of a role-binding definition:

```plaintext
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: <role-binding-name>
  namespace: <namespace>
subjects:
- kind: User
  name: <username>
roleRef:
  kind: Role
  name: <role-name>
  apiGroup: rbac.authorization.k8s.io
```

This role-binding definition binds the specified user to the specified role.

## **📍** Identity Providers:

An identity provider (IDP) is a third-party service that is used to authenticate and authorize users in a K8s cluster. K8s supports various identity providers, including LDAP, Active Directory, and OpenID Connect.

The following is an example of an OpenID Connect identity provider configuration:

```plaintext
apiVersion: v1
kind: ConfigMap
metadata:
  name: oidc-config
data:
  issuer: <issuer-url>
  client-id: <client-id>
  client-secret: <client-secret>
  redirect-uri: <redirect-uri>
  response-type: code
```

This configuration specifies the URL of the OpenID Connect provider, the client ID and secret, the redirect URI, and the response type.

## **🔹** How to login to the OpenShift cluster that we created in the steps:

To log in to an OpenShift cluster, follow these steps:

1. Get the URL of the OpenShift cluster and your credentials from your system administrator.
    
    🔗 [https://developers.redhat.com/developer-sandbox](https://developers.redhat.com/developer-sandbox)
    
2. Install the oc command-line tool on your local machine.
    
3. Use the oc login command to log in to the OpenShift cluster:
    

```plaintext
oc login <cluster-url> --username=<username> --password=<password>
```

This command logs you into the specified OpenShift cluster with the specified username and password.

1. Once you are logged in, you can use the oc command-line tool to manage resources in the cluster.
    

## **📍** Conclusion:

K8s RBAC is a powerful security mechanism that helps administrators manage access to resources in a K8s cluster. It allows administrators to define roles, role bindings, and service accounts to control access to resources. Identity providers can be used to authenticate and authorize users in a K8s cluster. By following the steps outlined in this blog, you can create and manage users, service accounts, roles, and role bindings in a K8s cluster, and you can also configure identity providers to authenticate and authorize users.

## **📍** References:

1. Kubernetes RBAC documentation: [**https://kubernetes.io/docs/reference/access-authn-authz/rbac/**](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
    
2. OpenShift documentation: [**https://docs.openshift.com/**](https://docs.openshift.com/)
    
3. Kubernetes RBAC tutorial: [**https://auth0.com/blog/kubernetes-rbac-and-namespaces-explained/**](https://auth0.com/blog/kubernetes-rbac-and-namespaces-explained/)
    
4. Kubernetes API reference: [**https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/**](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/)
    

## **🔹 Checkout GitHub Repository for projects:**

🔗 [**github.com/sumanprasad007**](http://github.com/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683348228748/f0f7768f-11d6-4395-9519-c82cdd645149.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")