# Application Metrics with Prometheus

This README provides an overview of how metrics are exposed and collected from our application using Prometheus. It covers the `/metrics` endpoint, Prometheus server scraping, and how to access metrics.

## Overview

Our application uses the Prometheus Go client library to collect and expose metrics about its operation. This includes data like the number of incoming HTTP requests, processing times, error counts, etc.

Metrics are exposed through a special HTTP endpoint, typically named `/metrics`. The `/metrics` endpoint is accessible to the Prometheus server, which periodically "scrapes" (downloads) the metrics data for storage and analysis.

## Accessing Metrics

To access the metrics of a particular application pod, you can use port-forwarding with `kubectl`:

```bash
kubectl port-forward pod/<pod-name> 8080:<metrics-port>
```

Replace <pod-name> with the name of your pod, and <metrics-port> with the port number where the /metrics endpoint is exposed.

After setting up port-forwarding, you should be able to access the metrics data in your local browser at http://localhost:8080/metrics.
  
## Understanding the Metrics
The metrics exposed at the /metrics endpoint are in the Prometheus exposition format, which is a text-based format designed for easy parsing and analysis. Here is a simple example of what this data might look like:
 
```bash
# HELP http_requests_total The total number of HTTP requests.
# TYPE http_requests_total counter
http_requests_total{method="post",code="200"} 1027
http_requests_total{method="post",code="400"} 3
```
 
Each line represents a single metric. Lines starting with # HELP provide a description of the metric, and lines starting with # TYPE provide the type of the metric (counter, gauge, histogram, etc.). Other lines provide the metric values, with each {} block representing a set of labels for the metric.

More Information
For more information about the specific metrics exposed by our application, see the application's documentation or source code.

For more information about Prometheus and its metrics format, see the [Prometheus documentation](https://prometheus.io/docs/introduction/overview/)

