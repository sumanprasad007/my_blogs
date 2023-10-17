---
title: "Deep Dive Into the Four Types of Prometheus Metrics"
datePublished: Tue Oct 17 2023 16:50:13 GMT+0000 (Coordinated Universal Time)
cuid: clnuk8hvf000109jm9v89fble
slug: deep-dive-into-the-four-types-of-prometheus-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697561370851/71279875-9510-4d5e-9fd6-f7e769751d13.gif
tags: aws, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

Welcome to the first instalment of our metrics series! In this post, we'll take a deep dive into the four types of Prometheus metrics, exploring how they work, their significance, and their role in the world of IT monitoring. Prometheus metrics are essential for tracking performance, consumption, and productivity over time. So, let's embark on this metrics journey and gain a comprehensive understanding of what they are and how they function.

### **📊 Metrics: The Pulse of Monitoring**

Metrics are the lifeblood of IT monitoring, providing insights into the performance and health of systems. They offer a window into various measurements, such as CPU and memory usage, request duration, latencies, and much more. These metrics evolve over time and enable engineers to create alerts and dashboards to ensure systems perform as expected.

### At their core, a metric data point consists of:

1. A metric name
    
2. A timestamp indicating when the data point was collected
    
3. A measurement represented by a numeric value
    

### **🔀 Enter Dimensional Metrics**

Over the last decade, as systems have grown increasingly complex, the concept of dimensional metrics has emerged. Dimensional metrics include a set of tags or labels, providing additional context to the metric. These labels offer the capability to aggregate and analyze a metric across multiple components and dimensions. This is particularly valuable in understanding the behavior of modern, dynamic systems.

### **🚀 Prometheus: A Monitoring Powerhouse**

In the world of monitoring, Prometheus, an open-source project hosted by the Cloud Native Computing Foundation (CNCF), has risen to prominence. It is the de facto standard for metrics monitoring and supports a robust metric exposition format and a remote write protocol. This combination has been widely adopted by the community and various vendors.

### **📡 OpenMetrics and OpenTelemetry**

Alongside Prometheus, the CNCF also oversees OpenMetrics, which builds upon Prometheus's exposition format to provide a standardized model for metric collection. This initiative aims to become part of the Internet Engineering Task Force (IETF).

More recently, OpenTelemetry has emerged with the goal of unifying the collection of metrics, traces, and logs. It's designed to facilitate instrumentation and correlation across telemetry signals.

### **🧐 Choosing the Right Standard**

With several options available, you might be wondering which standard is best for your needs. To help you make an informed choice, we've prepared a three-part blog series that delves deep into the metric standards hosted by the CNCF. We'll cover Prometheus metrics in this post, review OpenTelemetry metrics in the next, and in the final post, compare both formats and provide recommendations for interoperability.

## **📊 Prometheus Metrics: The Fab Four**

Prometheus excels in monitoring by collecting four types of metrics as part of its exposition format:

1. **Counters**
    
2. **Gauges**
    
3. **Histograms**
    
4. **Summaries**
    

Prometheus uses a pull model to collect these metrics, scraping HTTP endpoints that expose them. While this model works seamlessly in Kubernetes clusters, it can be challenging to monitor dynamic fleets of virtual machines, AWS Fargate containers, or Lambda functions with Prometheus.

### **🚫 The Challenge of Dynamic Environments**

Identifying the metrics endpoints to be scraped and dealing with network security policies can be cumbersome. To address these challenges, the community introduced the Prometheus Agent Mode in 2021, which exclusively collects metrics and sends them to a monitoring backend using the remote write protocol.

**🔄 Exposition Formats: Prometheus and OpenMetrics**

Prometheus can scrape metrics in both its own exposition format and the OpenMetrics format. Metrics are exposed via HTTP in either a text-based format (human-readable and widely supported) or a more efficient protocol buffer format.

**📐 A Simple Metric Model**

Prometheus follows a straightforward metric model with four metric types, all represented in the exposition format using a single underlying data type. This data type consists of a metric name, a set of labels, and a float value. The timestamp is added when the metrics are scraped.

Each unique combination of a metric name and a set of labels defines a series, while each timestamp and float value constitutes a sample (a data point) within a series.

**📝 Providing Context with Metadata**

One standout feature of the Prometheus exposition format is its ability to associate metadata with metrics, defining their type and offering a description. This information can be used by tools like Grafana to provide additional context to users, aiding in metric selection and application of PromQL functions.

### **📷 Example: A Prometheus Metric**

Here's an example of a metric exposed using the Prometheus exposition format:

```json
# HELP http_requests_total Total number of http api requests
# TYPE http_requests_total counter
http_requests_total{api="add_product"} 4633433
```

The `# HELP` line provides a description, and the `# TYPE` line specifies the metric type. In this case, it's a counter.

## **🔍 Next Steps**

In the upcoming sections of this series, we'll delve deeper into each of the Prometheus metrics in the exposition format. You'll gain a thorough understanding of counters, gauges, histograms, and summaries, exploring their use cases and how they contribute to effective system monitoring.

Stay tuned for more metrics wisdom in the next installment of this series! 📊🚀📐🔍

With this foundational knowledge, you're well-prepared to navigate the world of Prometheus metrics and make informed decisions for your monitoring needs. Happy metric monitoring! 😊📈📉📁