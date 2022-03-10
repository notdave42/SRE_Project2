| # API Service  |       |                                                                                                               |
|----------------|-------|---------------------------------------------------------------------------------------------------------------|
| Category       | SLI   | SLO                                                                                                           |
| -------------- | ----- | ------------------------------------------------------------------------------------------------------------- |
| Availability   |    sum (rate(apiserver_request_total{job="apiserver",code!~"5.."}[2d]))/sum (rate(apiserver_request_total{job="apiserver"}[2d]))   | Maintain 99% availablity of the service over a 2 day period                                                                                                           |
| Latency        |   histogram_quantile(0.90,sum(rate(apiserver_request_duration_seconds_bucket{job="apiserver"}[5m])) by (le, verb))    | Maintain a latency 90% of requests to the service below 100ms                                                                                   |
| Error Budget   |   1 - ((1 - (sum(increase(apiserver_request_total{job="apiserver", code="200"}[7d])) by (verb)) / sum(increase(apiserver_request_total{job="apiserver"}[7d])) by (verb)) / (1 - .90))    | Error budget is defined at 20%. This means that 20% of the all the service requests can fail and still be within the budget   |
| Throughput     |  sum(rate(apiserver_request_total{job="apiserver",code=~"2.."}[5m]))     | The rate of successful requests to the service will be more than 
5y
