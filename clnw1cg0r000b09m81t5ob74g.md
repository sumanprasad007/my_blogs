---
title: "Understanding Prometheus Counter Metrics 📊"
datePublished: Wed Oct 18 2023 17:36:57 GMT+0000 (Coordinated Universal Time)
cuid: clnw1cg0r000b09m81t5ob74g
slug: understanding-prometheus-counter-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697563395072/c1873b46-2783-4b3c-990f-52918ef9aee8.gif
tags: aws, web-development, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

In the world of monitoring and observability, Prometheus is a powerful tool for collecting and analyzing metrics from your applications and infrastructure. Among the various metric types that Prometheus supports, counters are fundamental for tracking cumulative, always-increasing values. In this blog, we'll delve into Prometheus counter metrics, their usage, and real-world applications, all sprinkled with relevant examples and emojis. 🚀

%[https://youtu.be/fJziSyJJgtU] 

### **📈 Counters: Metrics That Only Go Up**

Counters are like your personal tally, continuously increasing with every occurrence of a particular event. They are perfect for tracking things that naturally accumulate, such as the number of API requests, errors, orders, or bytes sent over a network interface.

**Example**: Let's say we're measuring the number of API calls for an "add\_product" operation:

```json
# HELP http_requests_total Total number of http api requests
# TYPE http_requests_total counter
http_requests_total{api="add_product"} 4633433
```

The metric name is `http_requests_total`, labeled with `api="add_product"`, and the counter's value is 4,633,433. This tells us that the "add\_product" API has been called 4,633,433 times since the last service start or counter reset.

### **💡 Real-Time Use Case 1: API Request Rate**

Now, simply knowing the absolute number doesn't provide much insight. However, when used with PromQL's `rate` function, you can calculate the requests per second the API is receiving.

```json
rate(http_requests_total{api="add_product"}[5m])
```

This query computes the average requests per second over the last five minutes.

### **💡 Real-Time Use Case 2: Absolute Change**

To calculate the absolute change over a time period, you can use the `increase` function.

```json
increase(http_requests_total{api="add_product"}[5m])
```

This returns the total number of requests made in the last five minutes. It's essentially the same as multiplying the per-second rate by the number of seconds in the interval (five minutes in our case).

```json
rate(http_requests_total{api="add_product"}[5m]) * 5 * 60
```

### **🌐 More Use Cases for Counters**

1. **E-commerce Orders**: Counters are perfect for measuring the number of orders in an e-commerce site. As each order is placed, the counter increases, providing real-time statistics on order volume.
    
2. **Network Traffic**: They're great for tracking the number of bytes sent and received over a network interface. These counters help monitor bandwidth utilization.
    
3. **Application Error Count**: To monitor application errors, counters can tally the number of errors, giving a straightforward indication of the error rate.
    

### **🐍 Example: Creating and Incrementing a Counter in Python**

Using the Prometheus client library for Python, you can easily create and increment a counter metric. For instance, in Python:

```json
from prometheus_client import Counter

api_requests_counter = Counter(
    'http_requests_total',
    'Total number of http api requests',
    ['api']
)
api_requests_counter.labels(api='add_product').inc()
```

### **🔁 Handling Counter Resets**

Since counters can be reset to zero, it's important to ensure that the backend used for storing and querying metrics can handle this scenario while still providing accurate results in the event of a counter restart.

## **Conclusion**

Counters in Prometheus are your go-to metric type for tracking cumulative, always-increasing values. They are indispensable for monitoring everything from API requests and network traffic to order volumes and error rates. By understanding how to use counters effectively, you can gain valuable insights into the growth and behavior of your systems. 📈🔢🚀