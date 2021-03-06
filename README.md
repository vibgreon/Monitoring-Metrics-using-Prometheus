<div align="center">
<img src="assets/1.svg" height="auto" width="100" /><img src="assets/2.svg" height="auto" width="100" />
<br />
<h1>Monitoring Metrics using Prometheus</h1>
<p>
An example application that shows how to implement Prometheus Metrics
</p>
</div>

[![CodeQL](https://github.com/vibgreon/Monitoring-Metrics-using-Prometheus/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/vibgreon/Monitoring-Metrics-using-Prometheus/actions/workflows/codeql-analysis.yml)

## About

An example application that shows how to implement Prometheus Metrics into your Golang application and visualize the data using Grafana.

## Getting started

#### Starting the application

You can start all services by running the docker-compose file:

```
docker-compose up -d
```

#### Generating load on HTTP Server

You can either generate load manually by visiting the HTTP page on localhost:8080 or generate load using some load generator. I use [Hey](https://github.com/rakyll/hey), which is an easy-to-use command-line tool.

```sh
hey -z 5m -q 5 -m GET -H "Accept: text/html" http://127.0.0.1:8080
```

```sh
hey -n 10000 -c 100 -m GET -H "Accept: text/html" http://127.0.0.1:8080
```

You can now see the metrics of your application on http://localhost:8080/metrics.

```sh
vibgreon@vibgreon:~/Desktop/learning-go/advanced-programs/PrometheusHTTPServer$ hey -n 10000 -c 100 -m GET -H "Accept: text/html" http://127.0.0.1:8080

Summary:
  Total:  3.0324 secs
  Slowest:  0.2544 secs
  Fastest:  0.0005 secs
  Average:  0.0287 secs
  Requests/sec: 3297.7592

  Total data: 1610000 bytes
  Size/request: 161 bytes

Response time histogram:
  0.000 [1] |
  0.026 [6087]  |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.051 [2503]  |■■■■■■■■■■■■■■■■
  0.077 [794] |■■■■■
  0.102 [285] |■■
  0.127 [138] |■
  0.153 [87]  |■
  0.178 [18]  |
  0.204 [39]  |
  0.229 [29]  |
  0.254 [19]  |


Latency distribution:
  10% in 0.0041 secs
  25% in 0.0093 secs
  50% in 0.0199 secs
  75% in 0.0364 secs
  90% in 0.0617 secs
  95% in 0.0849 secs
  99% in 0.1565 secs

Details (average, fastest, slowest):
  DNS+dialup: 0.0000 secs, 0.0005 secs, 0.2544 secs
  DNS-lookup: 0.0000 secs, 0.0000 secs, 0.0000 secs
  req write:  0.0001 secs, 0.0000 secs, 0.0284 secs
  resp wait:  0.0268 secs, 0.0003 secs, 0.2543 secs
  resp read:  0.0014 secs, 0.0000 secs, 0.0380 secs

Status code distribution:
  [200] 10000 responses

```

### Importing Grafana dashboard

Lastly, you can visualize the metrics data using Grafana, which should be running on localhost:3000 after deploying the docker-compose file.

1. You need to set Prometheus as your data source
2. Visualize the exposed Prometheus metrics in a Dashboard (I have also included a dashboard file in the Grafana folder that you can import)

## License

[MIT](https://github.com/vibgreon/Monitoring-Metrics-using-Prometheus/blob/main/LICENSE)
