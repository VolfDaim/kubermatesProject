# Grafana | Telegraf | InfluxDB
Необходимы kubectl, minikube, также контейнеры influxdb, telegraf, grafana
## Последовательность команд запуска
```
kubectl create namespace kubermates

kubectl create secret generic influxdb-creds \
  --from-literal=INFLUXDB_DATABASE=local_monitoring \
  --from-literal=INFLUXDB_USERNAME=root \
  --from-literal=INFLUXDB_PASSWORD=root1234 \
  --from-literal=INFLUXDB_HOST=influxdb

kubectl expose deployment influxdb --port=8086 --target-port=8086 --protocol=TCP --type=ClusterIP

kubectl expose deployment telegraf --port=8125 --target-port=8125 --protocol=UDP --type=NodePort

minikube service telegraf --namespace monitoring

kubectl create secret generic grafana-creds \
  --from-literal=GF_SECURITY_ADMIN_USER=admin \
  --from-literal=GF_SECURITY_ADMIN_PASSWORD=admin1234

kubectl expose deployment grafana --type=LoadBalancer --port=3000 --target-port=3000 --protocol=TCP

minikube service grafana --namespace monitoring
```
