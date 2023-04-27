---
title: "Day 3 - Kubernetes Workloads (Deployments, StatefulSets, DaemonSets, Jobs,
CronJobs)"
datePublished: Thu Apr 27 2023 04:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clgymn1an045qw4nvhrf797o1
slug: day-3-kubernetes-workloads-deployments-statefulsets-daemonsets-jobs-cronjobs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682529350982/04c0d302-4e85-4e35-9cd0-7d3a14cca002.png
tags: linux, aws, developer, devops, beginners

---

# **📍 Introduction:**

Welcome to the #KubeWeek challenge, it's 3rd day of the challenge where we strive to expand our knowledge and skills in the exciting world of Kubernetes! In this challenge, we'll be focusing on Kubernetes Workloads, including Deployments, StatefulSets, DaemonSets, Jobs, and CronJobs.

## **🔹** Pre-requisites:

To deploy a Deployment, can follow below steps to configure the Kubernetes Server:

1. Launch an AWS instance with t2.medium, or above.
    
2. Install Kubectl using the instructions provided at [https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
    
3. Install Minikube using the instructions provided at [**https://minikube.sigs.k8s.io/docs/start/**](https://minikube.sigs.k8s.io/docs/start/)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682512608619/67b5a323-3099-4194-80ae-3479ad23fd4a.png align="center")

# **📍** Deployment:

A Deployment in Kubernetes provides a declarative way to manage updates to Pods and ReplicaSets. It allows you to define a desired state for your application and the Deployment Controller will make the necessary changes to bring the actual state to the desired state at a controlled rate. With Deployments, you can create new ReplicaSets or replace existing ones, while ensuring high availability and scaling. Even the scaling is done using zero downtime as updation process is gradually done by targetting a node at a time and even the roll-back can be done easily whenever required...

1. Create a new file using the vim editor.
    
2. Add the following configuration to the file:
    

```python
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

### ⚜ Apply the configuration by running the following command:

```python
kubectl apply -f nginx-deployment.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513227117/8fc3c98b-2b5e-4c78-b484-5a69754758b0.png align="center")

### ⚜ Check the output to ensure that the Deployment has been successfully deployed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513003918/99d22df8-9f93-4f99-af96-d9163dcaa044.png align="center")

# **📍** StatefulSets:

StatefulSet is another API object used to manage stateful applications in Kubernetes. It manages the deployment and scaling of a set of Pods while ensuring ordering and uniqueness of these Pods are maintained. StatefulSets are similar to Deployments in that they manage Pods based on identical container specifications. However, each Pod has a persistent identifier that makes it unique and not interchangeable with other Pods. This makes StatefulSets ideal for applications that require persistent storage and ordered scaling. It's mostly done for the Databases or other crucial apps.

### ⚜ To deploy a StatefulSet, you can follow these steps:

1. Create a new file using the vim editor.
    
2. Add the following configuration to the file:
    

```python
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: example-statefulset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example
  serviceName: example
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
      - name: example
        image: example:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - name: data
          mountPath: /data
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

### ⚜ Apply the configuration by running the following command:

```python
kubectl apply -f statefulset.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513188489/6b527280-6b1a-482f-a93d-0cc3f385a8d9.png align="center")

### ⚜ Check the output to ensure that the StatefulSet has been successfully deployed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513153553/4b2a2684-5fef-44e8-b7de-2250ff0dfa3e.png align="center")

# **📍** DaemonSet:

A DaemonSet is another API object that ensures that all or some Nodes in a Kubernetes cluster run a copy of a Pod. It is useful when you need to run a copy of a Pod on each Node in the cluster. As nodes are added to the cluster, Pods are added to them, and as nodes are removed, those Pods are garbage collected. Deleting a DaemonSet will clean up all the Pods it created.

```python
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  namespace: kube-system
  labels:
    k8s-app: fluentd-logging
spec:
  selector:
    matchLabels:
      name: fluentd-elasticsearch
  template:
    metadata:
      labels:
        name: fluentd-elasticsearch
    spec:
      tolerations:
      - key: node-role.kubernetes.io/control-plane
        operator: Exists
        effect: NoSchedule
      - key: node-role.kubernetes.io/master
        operator: Exists
        effect: NoSchedule
      containers:
      - name: fluentd-elasticsearch
        image: quay.io/fluentd_elasticsearch/fluentd:v2.5.2
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
      terminationGracePeriodSeconds: 30
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
```

```python
kubectl apply nginx-daemonset.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682513502795/d2862f95-bad4-4d86-a665-e3ab3a5da254.png align="center")

# **📍 Kubernetes Jobs:**

Kubernetes Jobs are used to run a specific task or set of tasks to completion. When a Job is created, a specific number of Pods are created to execute the task(s) in parallel. Once all the Pods have completed the task, the Job is considered complete. Kubernetes Jobs are useful for running batch processing jobs or any type of one-off task that needs to be completed in a specific time frame.

### ⚜ **Creating a Kubernetes Job**

To create a Kubernetes Job, we need to define a Pod template that contains the command to run the task(s) and specify the number of Pods to create. Here is an example of a Job definition file that runs a simple task:

```python
apiVersion: batch/v1
kind: Job
metadata:
  name: example-job
spec:
  template:
    metadata:
      name: example-pod
    spec:
      containers:
      - name: example-container
        image: busybox
        command: ["echo", "Hello, Kubernetes!"]
      restartPolicy: Never
  backoffLimit: 4
```

In this example, we are creating a Job called "example-job" that will create one Pod running a container based on the BusyBox image. The container will run the command "echo Hello, Kubernetes!" and then exit. The "restartPolicy" is set to "Never" so that the Pod will not be restarted if it fails. The "backoffLimit" is set to 4, which means that if the Job fails, Kubernetes will attempt to restart it up to 4 times.

### ⚜ **Running a Kubernetes Job**

To run a Kubernetes Job, we can use the "kubectl create" command:

```python
kubectl create -f example-job.yaml
```

This command will create the Job based on the Job definition file "example-job.yaml". Once the Job is created, we can check its status using the "kubectl get jobs" command:

```python
kubectl get jobs
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682531284122/ef6ea2b8-bce1-407c-a2db-234c655ed984.png align="center")

This command will show the current status of all Jobs in the Kubernetes cluster. To view more detailed information about a specific Job, we can use the "kubectl describe job" command:

```python
kubectl describe job example-job
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682531337354/cdadfb6e-4a15-42af-acfa-17e29ada6ec7.png align="center")

This command will show detailed information about the "example-job" Job, including the number of Pods created, the status of each Pod, and any errors that occurred during the Job's execution.

### ⚜ **Cleaning up a Kubernetes Job**

Once a Kubernetes Job has completed, we can clean up the resources it used by deleting the Job:

```python
kubectl delete job example-job
```

This command will delete the "example-job" Job and all the Pods it created.

# **📍 Kubernetes CronJobs:**

Kubernetes CronJobs are used to schedule recurring tasks in a Kubernetes cluster. They are similar to Unix cron jobs in that they allow users to specify a schedule for when a task should be executed. Kubernetes CronJobs are useful for tasks that need to be performed on a regular basis, such as backing up a database or sending out regular reports.

### ⚜ **Creating a Kubernetes CronJob**

To create a Kubernetes CronJob, we need to define a Pod template and specify a schedule for when the task should be executed. Here is an example of a CronJob definition file that runs a task every minute:

```python
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: report-generator
spec:
  schedule: "0 0 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: report-generator
              image: my-report-generator
              command: ["generate-report.sh"]
```

In this manifest file, we are creating a CronJob named "report-generator" that runs the "[generate-report.sh](http://generate-report.sh)" script every day at midnight. The Job template specifies that the script should be run in a container named "report-generator" using the "my-report-generator" image.

To deploy this CronJob, you can use the kubectl apply command:

```python
kubectl apply -f cronjob.yaml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682532164417/f4fde2d1-e4a1-4b35-801e-1afcc1377f78.png align="center")

Once the CronJob is deployed, Kubernetes will automatically create a new Job object at the scheduled time. The Job will run the specified command in a new container, and then terminate once the task is complete.

To view the status of a CronJob, you can use the kubectl get cronjobs command:

```python
kubectl get cronjobs
```

This will show you a list of all the CronJobs in the current namespace, along with their current status.

# **📍 Conclusion:**

In conclusion, Kubernetes offers various options for deploying different types of workloads in a cluster, including Deployments, StatefulSets, DaemonSets, Jobs, and CronJobs. Each type of workload has its specific use case and provides unique features to help manage and scale applications efficiently.

Deployments are commonly used for stateless applications, while StatefulSets are preferred for stateful applications. DaemonSets are suitable for running a single copy of a pod on each node, while Jobs and CronJobs are used for running tasks or batch jobs at specific intervals or once. Overall, Kubernetes provides a powerful platform for managing and scaling containerized applications. By using the appropriate workload type based on the application's needs, developers and system administrators can deploy and manage applications effectively. A CronJob is a powerful tool for scheduling tasks in a Kubernetes cluster. By defining a schedule and a Job template, you can ensure that important tasks are performed automatically and regularly.