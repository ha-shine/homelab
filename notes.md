# Summary

- Using k3s for k8s cluster, `apollo-1` being the master
- VictoriaMetrics and Grafana for monitoring, installed using `victoria-metrics-k8s-stack` and operator separately

## K3 Notes

- `K3S_TOKEN` can be found at server node `/var/lib/rancher/k3s/server/node-token`

## Nodes

- 2-node cluster connected with a switch

| hostname |   ip address    |
|----------|-----------------|
| apollo-1 | 192.168.69.1/22 |
| apollo-2 | 192.168.69.2/22 |

## Monitoring

- Uses VictoriaMetrics for monitoring, operator was installed separately

## Change log

|    date    | change                                         |
|------------|------------------------------------------------|
| 2026-04-13 | Replace beszel with VictoriMetrics and Grafana |
| 2026-04-13 | Installed beszel hub and agent in the cluster  |
| 2026-04-12 | Installed tailscale operator in the cluster    |
| 2026-04-11 | Setup k8s cluster with two nodes               |
