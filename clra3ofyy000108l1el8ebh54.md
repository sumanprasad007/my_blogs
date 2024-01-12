---
title: "Day 20: Navigating the SSL/TLS Seas 🚢🔐"
datePublished: Fri Jan 12 2024 03:50:10 GMT+0000 (Coordinated Universal Time)
cuid: clra3ofyy000108l1el8ebh54
slug: day-20-navigating-the-ssltls-seas
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705031232187/305ea4b1-aeaf-44b3-867b-3e1870c5b8e0.gif
tags: aws, python, web-development, kubernetes, webdev, developer, python3, devops, aws-lambda, aws-certified-solutions-architect-associate, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

## Introduction 🎉

Embark on a journey into the realm of SSL/TLS, where encryption transforms the waves of data into secure passages. Let's unravel the basics of SSL/TLS certificates, their orchestration within Load Balancers, and the art of safeguarding connections. Get ready to set sail into the world of secure communication!

## SSL/TLS - A Secure Prelude 🌐🔒

### What's in a Name?

SSL, or Secure Sockets Layer, and its successor TLS, Transport Layer Security, are cryptographic protocols orchestrating secure connections. Though TLS is the modern star, the term SSL is still affectionately used. Public SSL certificates, issued by Certificate Authorities like Comodo and Let's Encrypt, play a pivotal role, ensuring encrypted journeys across the web.

### Certificate Lifelines ⏳📜

SSL certificates have a life cycle marked by expiration dates. Certificate renewal is a dance of security, ensuring your encryption remains a shield against prying eyes.

## Load Balancer - SSL Symphony 🎶🔗

### Certificate Management

In the Load Balancer orchestra, an X.509 certificate takes center stage, managing SSL/TLS connections. AWS Certificate Manager (ACM) is the conductor, allowing seamless certificate management. You can also upload your certificates, orchestrating a symphony of secure connections.

### HTTPS Listener Choreography

In the HTTPS listener ballet, a default certificate takes the lead. Supporting multiple domains is an art form, accomplished with optional certificate lists. Clients gracefully use Server Name Indication (SNI) to specify their destination hostname, creating a harmonious connection.

## SSL – Server Name Indication (SNI) 🌐🎭

### Artistry in Handshakes

SNI shines in the art of handling multiple SSL certificates on one server. A newer protocol requiring clients to reveal the target server hostname during the initial SSL handshake, SNI enables servers to gracefully pick the correct certificate. Note: Works wonders for ALB & NLB but takes a bow for CLB.

## Elastic Load Balancers - SSL Ensembles 🔄🔐

### The Classic Symphony (CLB)

Classic Load Balancers play a singular tune, supporting only one SSL certificate. Multiple CLBs twirl in unison for varied SSL certificates across hostnames.

### The ALB & NLB Harmony (v2)

Application Load Balancers and Network Load Balancers, the newer virtuosos, support multiple SSL certificates. They dance to the SNI melody, creating a symphony of secure connections across multiple domains.

## Connection Draining - A Safe Exit 🚀🚧

### A Graceful Finale

Connection Draining (CLB) and Deregistration Delay (ALB & NLB) take a bow as the curtain falls. They ensure in-flight requests complete their performance before instances gracefully exit or go under maintenance. This graceful ballet prevents abrupt interruptions and adds finesse to your Load Balancer orchestration.

## Conclusion 🌟

As we navigate the SSL/TLS seas, may your connections be secure, your certificates ever-renewing, and your Load Balancer orchestra playing a symphony of encrypted harmony. Sail on, brave mariner, into the secure waters of SSL/TLS! 🔐🚢

## Image Credits:

[https://www.google.com/url?sa=i&url=https%3A%2F%2Fgeekflare.com%2Ffree-ssl-tls-certificate%2F&psig=AOvVaw0i4d9c88D-u-lCYhLrkZKJ&ust=1705117480691000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCOjwuOL31oMDFQAAAAAdAAAAABAP](https://www.google.com/url?sa=i&url=https%3A%2F%2Fgeekflare.com%2Ffree-ssl-tls-certificate%2F&psig=AOvVaw0i4d9c88D-u-lCYhLrkZKJ&ust=1705117480691000&source=images&cd=vfe&opi=89978449&ved=0CBMQjRxqFwoTCOjwuOL31oMDFQAAAAAdAAAAABAP)