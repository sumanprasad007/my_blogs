---
title: "Simplify Data Persistence in Docker with Volumes and Bind Mounts"
datePublished: Fri Apr 14 2023 06:25:24 GMT+0000 (Coordinated Universal Time)
cuid: clgg60j9s000i09mh1sjbhk8o
slug: simplify-data-persistence-in-docker-with-volumes-and-bind-mounts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681453286939/a9c67ab0-ece6-43e3-a3f1-ee960f8468e6.png
tags: docker, aws, developer, devops, beginners

---

# **📍** Introduction:

If you've ever used Docker, you might have encountered a common problem - the data you store in a Docker container disappears when the container dies. This is because the file system of a Docker container is deleted when the container is removed.

Fortunately, Docker provides two solutions to this problem - volumes and bind mounts. In this blog post, we'll take a closer look at both of these solutions and see how you can use them to persist data beyond the lifetime of containers.

As Docker containers are ephemeral, it is essential to persist data beyond the lifetime of the container. Docker volumes and bind directories on a host as a mount are the two ways of handling data persistence in Docker containers. In this guide, we'll explore these two approaches and their key differences.

# **📍** What are Docker Volumes? 🤔

![](https://user-images.githubusercontent.com/43399466/218018334-286d8949-d155-4d55-80bc-24827b02f9b1.png align="left")

Docker volumes provide a way to store data on the host file system that persists even if the container is deleted and recreated. This approach provides better flexibility than bind mounts and can be backed up separately from the host file system. Volumes can also be moved between containers and hosts.

# **📍** How to Create and Manage Docker Volumes? 🛠️

You can create and manage Docker volumes using the `docker volume` command. Let's see how we can create a new volume and mount it to a container:

## **🔹 Create Volume:**

```python
# Creating a new volume
docker volume create <volume_name>
```

Any data written to the `/data` directory inside the container will be persisted in the volume on the host file system.

## **🔹 List docker volumes:**

```python
docker volume ls
```

## **🔹** Mounting a Volume

Once you've created a volume, you can mount it to a container using the `-v` or `--mount` option when running a `docker run` command. For example:

```python
docker run -it -v <volume_name>:/data <image_name> /bin/bash
```

This command will mount the volume `<volume_name>` to the `/data` directory in the container. Any data written to the `/data` directory inside the container will be persisted in the volume on the host file system.

# **📍** What are Bind Directories on a Host as a Mount? 🤔

Bind mounts allow you to mount a directory from the host file system into a container. This approach has the same behaviour as volumes but is specified using a host path instead of a volume name.

## **🔹** For example:

```python
docker run -it -v <host_path>:<container_path> <image_name> /bin/bash
```

## **🔹** Key Differences between Docker Volumes and Bind Directories on a Host as a Mount 🔑

Volumes are better suited for more complex use cases where you need more control over the data being persisted in the container. In contrast, bind directories on a host as a mount are appropriate for simple use cases where you need to mount a directory from the host file system into a container.

# **📍** Conclusion:

In summary, Docker volumes and bind directories on a host as a mount provide different ways to handle data persistence in Docker containers. Choose the approach that best fits your use case to ensure that your data is persisted beyond the lifetime of the container. 🚀

Hashtags:

#Docker #Volumes #BindMounts #DataPersistence #Containers #DevOps