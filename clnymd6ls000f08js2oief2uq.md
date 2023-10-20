---
title: "Unraveling the Magic of Prometheus Histogram Metrics"
datePublished: Fri Oct 20 2023 13:00:56 GMT+0000 (Coordinated Universal Time)
cuid: clnymd6ls000f08js2oief2uq
slug: unraveling-the-magic-of-prometheus-histogram-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697564036581/efa43e2f-4d3f-4f64-9e8f-6182d7fd306c.gif
tags: kubernetes, devops, aws-lambda, trainwithshubham, 90daysofdevops-chanllenge

---

## **Introduction**

Welcome back to our metric series! In this post, we'll explore Prometheus Histogram metrics, which play a vital role in capturing and analyzing the distribution of measurements. Histograms are particularly valuable for measuring request durations and response sizes, providing insights into how these measurements are distributed. Let's dive into the world of Histogram metrics and discover their significance in IT monitoring.

### **📊 Histograms: Capturing the Distribution**

Histogram metrics are like treasure chests that unveil the distribution of measurements. They partition the entire range of measurements into intervals known as buckets, tracking how many measurements fall into each bucket.

A histogram metric comprises several components:

1. A counter with the total number of measurements, with a metric name suffixed by `_count`.
    
2. A counter with the sum of all measurement values, with a metric name suffixed by `_sum`.
    
3. Histogram buckets, exposed as counters, with the metric name suffixed by `_bucket`. Each bucket is labeled with `le` (less than or equal to), indicating the upper inclusive bound. This means that a bucket with an upper bound of `N` includes all data points with values less than or equal to `N`.
    

### **📈 Example: Measuring Response Time**

For example, to measure the response time of an "add\_product" API endpoint on [`host1.domain.com`](http://host1.domain.com), a histogram metric might look like this:

```json
# HELP http_request_duration_seconds Api requests response time in seconds
# TYPE http_request_duration_seconds histogram
http_request_duration_seconds_sum{api="add_product", instance="host1.domain.com"} 8953.332
http_request_duration_seconds_count{api="add_product", instance="host1.domain.com"} 27892
http_request_duration_seconds_bucket{api="add_product", instance="host1.domain.com", le="0"}
http_request_duration_seconds_bucket{api="add_product", instance="host1.domain.com", le="0.01"} 0
http_request_duration_seconds_bucket{api="add_product", instance="host1.domain.com", le="0.025"} 8
# ... (other bucket values)
http_request_duration_seconds_bucket{api="add_product", instance="host1.domain.com", le="+Inf"} 27892
```

In this example, we have the sum, count, and various buckets. The sum and count can be used to calculate the average measurement over time. In PromQL, the average duration for the last five minutes might be computed as follows:

```json
rate(http_request_duration_seconds_sum{api="add_product", instance="host1.domain.com"}[5m]) / rate(http_request_duration_seconds_count{api="add_product", instance="host1.domain.com"}[5m])
```

You can also use these to compute averages across different series. For instance, to calculate the average request duration across all APIs and instances in the last five minutes:

```json
sum(rate(http_request_duration_seconds_sum[5m])) / sum(rate(http_request_duration_seconds_count[5m]))
```

### **📊 Percentiles with Histograms**

Histograms also enable the computation of percentiles at query time for individual series as well as across series. In PromQL, you can use the `histogram_quantile` function to achieve this. It's worth noting that Prometheus uses quantiles, which are essentially the same as percentiles but are represented on a scale of 0 to 1, while percentiles use a scale of 0 to 100. For example, to calculate the 99th percentile (0.99 quantile) of response time for the "add\_product" API on [`host1.domain.com`](http://host1.domain.com), you would use this query:

```json
histogram_quantile(0.99, rate(http_request_duration_seconds_bucket{api="add_product", instance="host1.domain.com"}[5m]))
```

The power of histograms is further evident in their ability to be aggregated. To find the 99th percentile of response time across all APIs and instances, you'd use:

```json
histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))
```

In cloud-native environments, where numerous instances of the same component are often running, this aggregation capability is crucial.

### **👎 Drawbacks of Histograms**

While histograms are incredibly useful, they do have a few drawbacks:

1. **Predefined Buckets**: Bucket definitions must be established in advance, which can be a design challenge. Poorly defined buckets may prevent accurate percentile calculations and consume unnecessary resources.
    
2. **Approximate Percentiles**: Histograms provide approximate, rather than exact, percentiles. This is usually acceptable as long as bucket definitions are designed to yield reasonably accurate results.
    
3. **Computational Cost**: Calculating percentiles server-side can be computationally expensive when processing large datasets. Prometheus offers solutions like recording rules to precompute required percentiles.
    

### **🐍 Creating a Custom Histogram Metric in Python**

To create a custom histogram metric using the Prometheus client library for Python, you can follow this example:

```json
from prometheus_client import Histogram

api_request_duration = Histogram(
    name='http_request_duration_seconds',
    documentation='Api requests response time in seconds',
    labelnames=['api', 'instance'],
    buckets=(0.01, 0.025, 0.05, 0.1, 0.25, 0.5, 1, 2.5, 5, 10, 25)
)

api_request_duration.labels(
    api='add_product',
    instance='host1.domain.com'
).observe(0.3672)
```

In this Python code snippet, a custom histogram metric is defined with specified buckets, allowing you to observe values for the "add\_product" API on [`host1.domain.com`](http://host1.domain.com).

## **📏 Conclusion**

Prometheus Histogram metrics are essential for monitoring and understanding the distribution of measurements. They offer insights into metrics like request durations and response sizes. With the ability to compute percentiles and aggregate data, histograms are valuable tools in the realm of IT monitoring.

In the following sections of this series, we will continue exploring different Prometheus metric types and uncover how they can be effectively employed in various monitoring scenarios.

With this knowledge, you're equipped to harness the power of Prometheus Histogram metrics and enhance your IT monitoring capabilities. Stay tuned for more metric wisdom in the upcoming posts! 📊📈🧐🔍

Happy monitoring! 😊📁📉👨‍💻