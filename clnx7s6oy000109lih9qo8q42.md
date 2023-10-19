---
title: "Deep Dive into Prometheus Gauge Metrics"
datePublished: Thu Oct 19 2023 13:24:55 GMT+0000 (Coordinated Universal Time)
cuid: clnx7s6oy000109lih9qo8q42
slug: deep-dive-into-prometheus-gauge-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697563716262/8287bf34-2c52-4970-a673-7c47b820f67e.gif
tags: aws, web-development, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

Welcome to the next installment of our metrics series! In this post, we're going to explore Prometheus Gauge metrics in detail. Gauges are a crucial metric type used to measure values that can arbitrarily increase or decrease over time. These metrics provide immediate, meaningful information without additional processing and are widely used to monitor various parameters. So, let's dive into the world of Prometheus Gauges and discover their importance in IT monitoring.

### **📈 Gauges: Metrics with Real-Time Significance**

Gauges are among the most familiar metric types. Unlike counters, which only increase, gauges can both increase and decrease, making them ideal for tracking values that fluctuate. Gauges are particularly well-suited for measurements like temperature, CPU and memory usage, and the size of a queue. The value of a gauge metric, without any additional calculation, is immediately meaningful.

### **🌡️ Example: Monitoring Memory Usage**

For instance, to measure memory usage on a host, a gauge metric can be used, such as:

```json
# HELP node_memory_used_bytes Total memory used in the node in bytes
# TYPE node_memory_used_bytes gauge
node_memory_used_bytes{hostname="host1.domain.com"} 943348382
```

This metric informs us that, at the time of measurement, the memory used on the node [`host1.domain.com`](http://host1.domain.com) is approximately 900 megabytes. The metric's value is directly interpretable, as it tells us the exact amount of memory consumption on that node.

### **🚫 No Rate or Delta, But More Functions**

Unlike counters, gauges do not lend themselves to rate or delta calculations since they can increase or decrease. However, functions that compute average, maximum, minimum, or percentiles for specific series are often used with gauge metrics. In Prometheus, these functions include `avg_over_time`, `max_over_time`, `min_over_time`, and `quantile_over_time`. For example, to calculate the average memory usage on [`host1.domain.com`](http://host1.domain.com) over the last ten minutes:

```json
avg_over_time(node_memory_used_bytes{hostname="host1.domain.com"}[10m])
```

### **🐍 Creating Gauge Metrics in Python**

Creating a gauge metric using the Prometheus client library for Python is straightforward. Here's an example:

```json
from prometheus_client import Gauge

memory_used = Gauge(
    'node_memory_used_bytes',
    'Total memory used in the node in bytes',
    ['hostname']
)

memory_used.labels(hostname='host1.domain.com').set(943348382)
```

In this code snippet, we define a gauge metric named `node_memory_used_bytes`, provide a description, and specify a label called `hostname`. We then set the gauge's value for the [`host1.domain.com`](http://host1.domain.com) host.

## **🌟 Conclusion**

Prometheus Gauge metrics are a fundamental part of IT monitoring. They provide immediate and meaningful information about values that can both increase and decrease over time. Whether you're monitoring memory usage, CPU load, or any other dynamic parameter, gauges are your go-to metric type.

In the upcoming sections of this series, we'll continue exploring other Prometheus metric types, such as histograms and summaries, and learn how to use them effectively in various monitoring scenarios. With this knowledge, you're well on your way to mastering Prometheus metrics and enhancing your IT monitoring capabilities. Stay tuned for more metric wisdom in the upcoming posts! 📈📉🧐🌟

Happy monitoring! 😊🔍📁👨‍💻