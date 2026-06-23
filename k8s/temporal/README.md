# Temporal

Create the database secret before installing either chart. The secret must contain the
Bitnami PostgreSQL admin and application-user password keys. The `password` key is
also used by Temporal to connect as the `temporal` user:

```sh
kubectl create namespace temporal
kubectl create secret generic temporal-postgresql-secret \
  --namespace temporal \
  --from-literal=postgres-password='<postgres-admin-password>' \
  --from-literal=password='<password>'
```

Install PostgreSQL first, then Temporal:

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami

helm upgrade --install temporal-postgresql bitnami/postgresql \
  --namespace temporal \
  --values k8s/temporal/postgresql-values.yml

helm upgrade --install temporal temporal \
  --repo https://go.temporal.io/helm-charts \
  --namespace temporal \
  --values k8s/temporal/values.yml \
  --timeout 900s

kubectl apply --filename k8s/temporal/service.yaml
```

If the Web UI reports that the `default` namespace does not exist, re-run the
Temporal Helm upgrade above so the namespace creation hook runs. You can also
create it manually from the admin tools pod:

```sh
kubectl exec --namespace temporal deployment/temporal-admintools -- \
  temporal operator namespace create --namespace default --retention 3d
```

Namespace registration can take up to 15 seconds to become visible in the UI.
