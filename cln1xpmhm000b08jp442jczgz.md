---
title: "Prometheus Metrics with PromQL: Harnessing the Power of Histograms and Gauges 📈🔍"
datePublished: Wed Sep 27 2023 16:02:08 GMT+0000 (Coordinated Universal Time)
cuid: cln1xpmhm000b08jp442jczgz
slug: prometheus-metrics-with-promql-harnessing-the-power-of-histograms-and-gauges
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695830495579/cda1dfdb-ffa0-40df-8d9c-81c3e8925335.gif
tags: kubernetes, monitoring, devops, 90daysofdevops, trainwithshubham

---

# **Introduction:**

Prometheus is a stalwart in the world of monitoring and observability, and its query language, PromQL, offers a plethora of capabilities. In this blog, we dive deep into two essential Prometheus metric types - histograms and gauges. You'll learn their different functionalities, discover how to push metrics to Prometheus using the Push Gateway and explore real-world use cases with examples. So, let's embark on a journey to understand how these tools can solve monitoring challenges! 🚀

## **Histograms: Slicing and Dicing Metrics for Precision 📊**

Histograms are a versatile metric type in Prometheus, primarily used to measure and analyze the distribution of values over time. They enable you to track the spread and concentration of data, making them invaluable for understanding system performance.

### **Functionality of Histograms in PromQL**

Histograms come with several built-in functions in PromQL:

* `histogram_quantile(q, le)`: Calculates quantiles (e.g., 95th percentile) from histogram data.
    
* `rate(metric[duration])`: Computes the rate of change over a specified duration for histogram buckets.
    
* `sum_over_time(metric[duration])`: Aggregates values over a specific time range for histogram buckets.
    
* `increase(metric[duration])`: Measures the increase in values over a duration.
    

### **Real-Time Use Case: Latency Monitoring ⏱️**

Imagine you're monitoring an e-commerce website, and you want to measure the 99th percentile latency of product search queries:

```plaintext
histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket{job="web", endpoint="product_search"}[5m])) by (le))
```

With this query, you can pinpoint high-latency queries, enabling you to optimize your system for better user experience.

## **Gauges: Tracking Instantaneous Values ⏲️**

Gauges, on the other hand, represent single numerical values that can go up or down. They're perfect for tracking metrics like CPU usage, memory consumption, or the number of active connections.

### **Functionality of Gauges in PromQL**

While gauges are simple in concept, you can still leverage various PromQL functions to extract valuable insights:

* `increase(metric[duration])`: Measures the change in gauge values over a specified duration.
    
* `rate(metric[duration])`: Calculates the rate of change over time for gauge values.
    
* `absent(metric)`: Checks if a gauge metric is absent, aiding in anomaly detection.
    

### **Real-Time Use Case: Server Resource Monitoring 🖥️**

Consider a scenario where you need to monitor the memory usage of a server:

```plaintext
node_memory_MemAvailable_bytes
```

This straightforward gauge query fetches the available memory on the server, helping you ensure optimal resource allocation.

## **Push Gateway: Bridging the Gap to Push Metrics 🌐**

In Prometheus, metrics are typically pulled from targets by the Prometheus server. However, there are cases where you want to push metrics, like in ephemeral or batch job scenarios. That's where the Prometheus Push Gateway comes in.

### **Push Gateway Functionality**

* Acts as a buffer for metrics sent by jobs or services.
    
* Metrics are pushed to the Push Gateway instead of being pulled.
    
* Metrics are pulled from the Push Gateway by Prometheus.
    

### **Real-Time Use Case: Batch Job Metrics Processing 🔄**

Imagine you have batch jobs running at irregular intervals, and you need to collect metrics from them. You can push metrics from these jobs to the Push Gateway:

```plaintext
# Pushing a metric using cURL
echo "my_batch_job_duration_seconds 123.45" | curl --data-binary @- http://pushgateway:9091/metrics/job/my_batch_job
```

The Push Gateway ensures that metrics from these intermittent jobs are available for Prometheus without polling them directly.

## **Problem-Solving with Metrics 🧩**

Prometheus, histograms, gauges, and the Push Gateway work together seamlessly to solve various monitoring challenges:

* **Problem**: Understanding latency outliers.
    
    * **Solution**: Use histograms to calculate quantiles for detailed latency analysis.
        
* **Problem**: Real-time server resource monitoring.
    
    * **Solution**: Leverage gauges to track instantaneous values like memory and CPU usage.
        
* **Problem**: Collecting metrics from batch jobs.
    
    * **Solution**: Employ the Push Gateway to accept metrics from batch jobs and make them accessible to Prometheus.
        

With the right metrics, tools, and PromQL queries, you can gain deep insights into your systems, diagnose issues, and optimize performance. Prometheus, histograms, gauges, and the Push Gateway are your allies in this quest for observability excellence. 🚀🔍 Remember to consult the Prometheus documentation and explore more use cases to fully unlock the potential of these monitoring tools! 📚🔓

Happy monitoring! 📈🔔

### **🔍 Checkout my Portfolio:**

**🔗** [**linktr.ee/sumanprasad007**](http://linktr.ee/sumanprasad007)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692607442282/98c6c100-886d-4894-80bc-db5df0141100.png?auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

### **🔍 Check out my YouTube channel - Prasad Suman Mohan:**

🔗 [**youtube.com/@sumanprasad007**](http://youtube.com/@sumanprasad007)

%[https://youtu.be/rAYm2Go2TvY]