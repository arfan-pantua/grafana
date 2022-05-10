# Installing and configuring Grafana HA (AWS Provider)

## Create Iam Policy using cli
- `aws iam create-policy --policy-name allow-to-rds-postgress-grafana --policy-document file://<path-to-monitoring-storage-policy.json>`
## Create namespace
- `kubectl create namespace grafana`
## Attach policy to cluster using eksctl and create service account
- `eksctl create iamserviceaccount --name grafana-sa --cluster <cluster-name> --namespace=grafana --attach-policy-arn arn:aws:iam::706050889978:policy/allow-to-rds-postgress-grafana --approve --override-existing-serviceaccounts`
## Create secret
- `kubectl  create secret generic -n grafana grafana-secret-config --from-file=grafana-secret-config.yaml=grafana-secret-config.yaml`

## Create database in RDS
- `kubectl apply -f .\ubuntu-pod.yaml -n default`
## Going to pod of Ubuntu and install postgres
- `apt update`
- `apt install postgresql postgresql-contrib`
-  `psql --host=dev-20220411-rds-pg.crzsc5gb1vu2.ap-southeast-1.rds.amazonaws.com --port=5432 -U hx --dbname=postgres`
- `CREATE DATABASE grafana`;
## Helming
### Grafana Helm
- `helm repo add stable https://charts.helm.sh/stable`
- `helm upgrade --install  grafana -n grafana grafana/grafana --values .\values.yaml`