# Installing and configuring Grafana HA (AWS Provider)

By default grafana would be use Sqlite for the DB. Also Grafana is installed as stateless, deployment, kind in k8s instead of statefull, thats explain once grafana pod is restarted all data included would be lost. In this repo we wil install grafana HA even the pod is restarted.

## Prerequisites
- Postgress
- EKS
- Kubectl

## Running Script
Fill the env in `initiate.sh` file then run it