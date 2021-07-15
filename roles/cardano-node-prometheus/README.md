# cardano-node-prometheus role
Configures monitoring via Prometheus on a host with `cardano-node-service` installed. This involves installing [`prometheus-node-exporter`](https://github.com/prometheus/node_exporter), as well as exposing the Prometheus metrics endpoint on a `cardano-node` instance.