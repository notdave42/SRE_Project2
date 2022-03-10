| # API Service  |       |                                                                                                               |
|----------------|-------|---------------------------------------------------------------------------------------------------------------|
| Category       | SLI   | SLO                                                                                                           |
| -------------- | ----- | ------------------------------------------------------------------------------------------------------------- |
| Availability   |  The service will be useable more than 99% of the time - Google SRE book | 99%                                                                                                           |
| Latency        |  Proportion of requests where the length of time it takes to respond to the request is less than 100ms - Google SRE book | 90% of requests below 100ms                                                                                   |
| Error Budget   |   The success rate of the service is over 80% - Boyant.io- https://buoyant.io/2020/10/21/kubernetes-slos-with-prometheus-linkerd/ | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget   |
| Throughput     | The proportion of time where the data processing rate is faster than 5 RPS -https://static.googleusercontent.com/media/sre.google/en//static/pdf/art-of-slos-handbook-a4.pdf   | 5 RPS indicates the application is functioning                                                                |
