---
title: "Optimizing Docker with Multi-Stage Builds and Distroless Containers"
datePublished: Thu Apr 13 2023 14:18:09 GMT+0000 (Coordinated Universal Time)
cuid: clgf7gn2r000409ml7ao56fyg
slug: optimizing-docker-with-multi-stage-builds-and-distroless-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681395451315/63d87e22-011c-4221-bf0b-5d32b060ca6d.jpeg
tags: docker, aws, developer, devops, beginners

---

# **📍 Introduction:**

Multi-Stage Docker Builds for Reducing Image Size and Enhancing Security Docker is a popular platform for packaging, distributing, and running applications in containers. With Docker, you can create lightweight, portable, and scalable containers that can run anywhere, regardless of the underlying infrastructure. However, one of the biggest challenges with Docker is to keep the container images small and secure.

In this blog post, we will demonstrate how to use multi-stage Docker builds to reduce image size and enhance security. We will use a simple Go application as an example and show you how to build a minimal Docker image using a distroless base image.

# **📍** Multi-Stage Docker Builds

Multi-stage Docker builds allow you to build an application in multiple stages, each with its own base image and set of instructions. The idea is to use one stage to compile the application and another stage to create the final image. This approach helps to reduce the size of the final image by discarding any unnecessary files and dependencies used during the build process.

# **📍 Examples - Dockerfile**

Let's take a look at an example Dockerfile that uses multi-stage builds to build a simple Go application:

```python
FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################

FROM scratch

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]
```

In this Dockerfile, we first create a build stage using the `ubuntu` base image. We install the `golang-go` package, copy the application source code to the container, and build the binary using the `go build` command. We set the `CGO_ENABLED=0` environment variable to disable the use of C libraries and reduce the size of the final image.

In the second stage, we use a `scratch` base image, which is an empty image with no operating system or shell. We copy the compiled binary from the build stage to the final image using the `COPY --from=build` command. Finally, we set the entrypoint for the container to run the binary.

## **🔹** Reduce Docker Image Size

Using multi-stage builds allows us to reduce the size of the final Docker image significantly. By discarding any unnecessary files and dependencies used during the build process, we end up with a minimal image that only contains the necessary files to run the application.

In our example, the final image size is only a few megabytes, compared to the hundreds of megabytes of the `ubuntu` base image. This makes the image much faster to download and deploy, which is especially important for large-scale production environments.

## **🔹**Creating a Distroless Image

Distroless images are minimalistic Docker images that only contain the necessary dependencies to run an application. They do not include a Linux distribution or any shell access. This makes them more secure and reduces their size.

To create a distroless image, we need to use a base image that does not contain a Linux distribution. We can use Google's Distroless base image, which includes only the necessary libraries to run the application.

Let's modify our Dockerfile to use the Distroless image:

```python
# Use a Distroless base image
FROM gcr.io/distroless/static

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]
```

Here, we're using the [`gcr.io/distroless/static`](http://gcr.io/distroless/static) image as our base image. This is a Distroless image that only contains the necessary libraries to run a static binary.

Next, we copy the compiled binary from the build stage to the root of the image. Finally, we set the entrypoint for the container to run the binary.

## **🔹 Building the image**

We can now build our Docker image using the following command:

```python
docker build -t my-app:distroless -f Dockerfile.distroless .
```

This will create a new Docker image tagged `my-app:distroless` that uses the Distroless base image and contains only the necessary dependencies to run our application.

Container Security One of the benefits of using multi-stage builds and Distroless images is that they improve container security. By reducing the number of dependencies included in the container, we can reduce the attack surface of our application.

# **📍** Best practices to secure Docker containers.

## **🔹** Use trusted base images:

When building a Docker image, it is essential to use a trusted base image. A trusted base image is one that is maintained by the Docker community or by reputable organizations. These images are usually regularly updated, and any security vulnerabilities are patched promptly. Using a trusted base image helps minimize the risk of your application being compromised.

## **🔹** Keep your images up-to-date:

Just like your base images, your application images should also be regularly updated. You should regularly check for security updates and patches for your operating system and application packages. Keeping your images up-to-date ensures that any security vulnerabilities are addressed promptly.

## **🔹** Use multi-stage builds:

Multi-stage builds can help reduce the size of your Docker images and improve security. With multi-stage builds, you can compile your application in a separate container and copy only the necessary files to the final container. This helps reduce the attack surface of your application and minimize the risk of security vulnerabilities.

## **🔹** Use non-root users:

By default, Docker containers run as the root user. Running containers as the root user can be a security risk as it gives the container full access to the host system. You should create a non-root user in your Dockerfile and use that user to run your container. This ensures that your container runs with minimal privileges and reduces the risk of security vulnerabilities.

## **🔹** Limit container privileges:

Docker containers can be configured to run with a limited set of privileges. You can use the `--cap-drop` and `--cap-add` flags to limit the capabilities of your container. This helps reduce the attack surface of your application and minimizes the risk of security vulnerabilities.

## **🔹** Use container orchestration platforms:

Container orchestration platforms like Kubernetes provide additional security features such as network policies, resource constraints, and runtime security. These features help ensure that your containers are secure and are not compromised.

# **📍** Example:

```python
# Use a trusted base image
FROM golang:1.16-alpine as build

# Set a non-root user
USER nobody:nobody

# Copy the application files
COPY . /app

# Build the application
WORKDIR /app
RUN go build -o app .

# Use a distroless image for security
FROM gcr.io/distroless/base-debian10

# Copy only the necessary files from the build container
COPY --from=build /app/app /app

# Set a non-root user
USER nonroot

# Set the entrypoint to run the application
CMD ["/app/app"]
```

In this Dockerfile, we start from a trusted base image of `golang:1.16-alpine` and set a non-root user. We copy the application files to the `/app` directory and build the application. Then, we use a distroless image from [`gcr.io/distroless/base-debian10`](http://gcr.io/distroless/base-debian10) for security reasons. We only copy the compiled application from the previous build stage and set a non-root user. Finally, we set the entrypoint to run the application.

This Dockerfile uses multi-stage builds to reduce the size of the image and improve security by using a distroless image. The non-root user is also used for security reasons, as running containers as root can be a security risk.

# **📍** Conclusion:

In conclusion, by implementing security measures such as multi-stage builds, distroless images, and using a non-root user, we can greatly enhance the security of our Docker containers for Go applications. Additionally, we can reduce the size of our images, making them faster and more efficient to deploy. It's important to keep in mind the security risks associated with Docker containers, and take proactive steps to mitigate them.