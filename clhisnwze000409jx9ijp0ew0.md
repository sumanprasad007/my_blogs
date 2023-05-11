---
title: "Kubernetes RBAC Introduction with Demo"
datePublished: Thu May 11 2023 07:14:41 GMT+0000 (Coordinated Universal Time)
cuid: clhisnwze000409jx9ijp0ew0
slug: kubernetes-rbac-introduction-with-demo
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

In Kubernetes, we have to manage the users and services role using the Identity providers i.e. LDAP, Active Directory, and OpenID Connect and many more. Another way in K8s, users are created and managed using the kubectl command-line tool. The following steps outline how to create a new user and manage user access:

1. Create a new user using the htpasswd tool:
    

```plaintext
htpasswd -c /path/to/users.htpasswd <username>
```

This command creates a new file called users.htpasswd and adds new user to it.

1. Create a new role:
    

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

This command creates a new role that defines what actions the user can perform on the specified resource.

1. Create a new role binding:
    

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

This command creates a new role binding that binds the user to the role.

## **📍** Kubernetes Service Accounts:

A service account is an identity that is used by pods to access other resources in a K8s cluster. It is similar to a user account but is used by automated processes instead of human users.

Service accounts can be created and managed using the kubectl command-line tool. The following steps outline how to create a new service account:

1. Create a new service account:
    

```plaintext
apiVersion: v1
kind: ServiceAccount
metadata:
  name: <service-account-name>
  namespace: <namespace>
```

This command creates a new service account with the specified name and namespace.

1. Create a new role:
    

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

This command creates a new role that defines what actions the service account can perform on the specified resource.

1. Create a new role binding:
    

This command creates a new role binding that binds the service account to the role:

```plaintext
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: <role-binding-name>
  namespace: <namespace>
subjects:
- kind: ServiceAccount
  name: <service-account-name>
  namespace: <namespace>
roleRef:
  kind: Role
  name: <role-name>
  apiGroup: rbac.authorization.k8s.io
```

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