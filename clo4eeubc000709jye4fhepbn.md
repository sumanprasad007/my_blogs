---
title: "Choosing Between Histograms and Summaries in Prometheus Metrics"
datePublished: Tue Oct 24 2023 14:04:53 GMT+0000 (Coordinated Universal Time)
cuid: clo4eeubc000709jye4fhepbn
slug: choosing-between-histograms-and-summaries-in-prometheus-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698156257525/a3e73f2f-5fb4-484a-91f5-bea39cf21d71.gif
tags: aws, monitoring, devops, 90daysofdevops, trainwithshubham

---

## **Introduction**

Welcome to the final part of our blog series on Prometheus metrics! In this installment, we'll help you answer the age-old question: "Histograms or Summaries, What Should I Use?" We'll explore the nuances of both metric types and provide guidance on selecting the right one for your specific use case. Let's dive in and make an informed choice!

### **📊 Histograms vs. Summaries: The Ultimate Showdown**

When deciding between histograms and summaries in Prometheus, you'll want to consider the following factors:

**1\. Flexibility and Aggregated Percentiles**:

* **Histograms**: Preferred in most cases due to their flexibility. They allow for aggregated percentiles, making them versatile in various scenarios.
    
* **Summaries**: Best suited when percentiles are not required, and averages are sufficient. They shine in situations where extreme precision is vital, such as contractual obligations for critical system performance.
    

**2\. Use Cases**:

* **Histograms**: Ideal for situations where you need to measure the distribution of measurements, like request durations or response sizes.
    
* **Summaries**: Useful when you need precise percentiles, such as ensuring compliance with performance-related contracts.
    

### **📊 Histograms vs. Summaries: A Quick Comparison**

Let's summarize the key characteristics of histograms and summaries in Prometheus:

| **Property** | **Histograms** | **Summaries** |
| --- | --- | --- |
| Flexibility | Highly flexible | Less flexible |
| Aggregated Percentiles | Supported | Not supported |
| Use Cases | Distribution of measurements | Precise percentiles |

## **🚀 Conclusion**

In this blog post series, we've embarked on a journey to understand Prometheus metrics. We've covered counters, gauges, histograms, and summaries, each with its unique role in IT monitoring. As we wrap up this series, it's time to dive into the world of OpenTelemetry metrics in the next part.

If you're on the lookout for a robust time-series database to store your metrics, consider Timescale. Particularly if you're a PostgreSQL user, you'll find Timescale to be a game-changer. Timescale, a PostgreSQL extension, enhances your PostgreSQL database's capacity to handle large volumes of metrics while ensuring fast writes and queries. It achieves this through automatic partitioning, query planner enhancements, improved materialized views, columnar compression, and more.

If you're running PostgreSQL on your hardware, simply add the TimescaleDB extension. For AWS users, you can quickly try Timescale by creating a free account on our platform – no credit card required, and it only takes a few seconds!

With a deeper understanding of Prometheus metrics and the ability to choose between histograms and summaries, you're better equipped for effective IT monitoring. Stay tuned for the upcoming part of our series, where we'll explore OpenTelemetry metrics. Your metrics journey is just beginning! 📊📈🔍📡🌐

Happy monitoring and metric management! 😊📁📉🚀🌟