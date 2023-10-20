---
title: "Unpacking the Power of Prometheus Summary Metrics"
datePublished: Fri Oct 20 2023 14:37:36 GMT+0000 (Coordinated Universal Time)
cuid: clnypti4r000809maeor7fwih
slug: unpacking-the-power-of-prometheus-summary-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697814675109/1814b50f-b9a4-404a-a6fb-41a6328fdb90.gif
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

Welcome back to our metric series! In this post, we're about to embark on a journey to explore Prometheus Summary metrics, which are invaluable for measuring request durations and response sizes. Summary metrics provide a comprehensive view of measurements, comprising a counter for total measurements, a counter for the sum of values, and quantiles. These quantiles offer insights into the distribution of measurements. Join us as we uncover the significance of Summary metrics in the realm of IT monitoring.

### **📊 Summary Metrics: The Whole Picture**

Summary metrics are akin to a versatile tool in the world of monitoring. They go beyond just aggregating data and provide a rich set of information:

1. **Total Count**: A counter metric with the total number of measurements, with the metric name suffixed by `_count`.
    
2. **Sum of Values**: Another counter metric with the sum of all measurement values, suffixed by `_sum`.
    
3. **Quantiles**: Optionally, a set of quantiles of measurements exposed as a gauge metric. These quantiles are presented with a `quantile` label. Unlike histograms, Prometheus client libraries use streamed quantiles, computed over a sliding time window.
    

### **📈 Example: Measuring Response Time**

To measure the response time of the "add\_product" API on [`host1.domain.com`](http://host1.domain.com), a summary metric might look like this:

```json
# HELP http_request_duration_seconds Api requests response time in seconds
# TYPE http_request_duration_seconds summary
http_request_duration_seconds_sum{api="add_product", instance="host1.domain.com"} 8953.332
http_request_duration_seconds_count{api="add_product", instance="host1.domain.com"} 27892
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="0"}
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="0.5"} 0.232227334
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="0.90"} 0.821139321
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="0.95"} 1.528948804
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="0.99"} 2.829188272
http_request_duration_seconds{api="add_product", instance="host1.domain.com", quantile="1"} 34.283829292
```

This example includes the sum and count, along with five quantiles. Quantile 0 represents the minimum value, quantile 1 is the maximum value, quantile 0.5 is the median, and quantiles 0.90, 0.95, and 0.99 represent the 90th, 95th, and 99th percentiles, respectively, of the response time for the "add\_product" API on [`host1.domain.com`](http://host1.domain.com).

### **👍 Advantages and Drawbacks**

While summaries provide more accurate quantiles than histograms, they come with certain advantages and drawbacks:

**Advantages**:

1. **Streamlined Quantiles**: Quantiles are calculated over a sliding time window, reducing the amount of data that needs to be sorted, which enhances efficiency.
    

**Drawbacks**:

1. **Client-Side Computation**: Calculating quantiles is computationally expensive on the client-side, as it requires maintaining a sorted list of data points. Not all Prometheus client libraries support quantiles, adding complexity to their implementation.
    
2. **Predefined Quantiles**: Quantiles must be predefined by the client library, limiting the quantiles that can be queried. New quantiles can't be calculated at query time, requiring code modifications for any additions.
    
3. **Lack of Aggregation**: Summaries cannot be aggregated across multiple series, making them less suitable for dynamic modern systems. This limitation becomes apparent when attempting to compute percentiles or quantiles across all instances of a component.
    

### **🐍 Creating a Summary Metric in Python**

To create a summary metric using the Prometheus client library for Python, you can use the following code snippet:

```json
from prometheus_client import Summary

api_request_duration = Summary(
    name='http_request_duration_seconds',
    documentation='Api requests response time in seconds',
    labelnames=['api', 'instance']
)

api_request_duration.labels(api='add_product', instance='host1.domain.com').observe(0.3672)
```

In this Python code, we define a summary metric named `http_request_duration_seconds` and provide labels for "api" and "instance." However, please note that the Prometheus client library for Python does not support quantiles in summary metrics.

## **📏 Conclusion**

Prometheus Summary metrics offer a comprehensive view of measurements, including total counts, the sum of values, and quantiles. They are a valuable tool for monitoring request durations and response sizes. While quantiles provide accurate insights into the distribution of data, the limitations regarding client-side computation and aggregation across multiple series should be considered.

In the upcoming sections of this series, we'll continue exploring different Prometheus metric types and discover how to use them effectively in diverse monitoring scenarios. With this knowledge, you're well-equipped to harness the potential of Prometheus Summary metrics and enhance your IT monitoring capabilities. Stay tuned for more metric wisdom in the upcoming posts! 📊📈🔍🧐

Happy monitoring! 😊👨‍💻📁📉🌟