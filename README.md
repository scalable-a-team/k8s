
## Prerequisites


#### Add required `helm` repo

```bash
helm repo add kong https://charts.konghq.com
```

``` bash
helm repo add signoz https://charts.signoz.io
```

## Running K8S

#### Create Secret for Github PAT

```bash
kubectl create secret docker-registry gh-regcred --docker-server=ghcr.io --docker-username=GITHUB_USERNAME --docker-password=GITHUB_PAT
```


#### Install RabbitMQ Cluster Operator
```bash
kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"   
```

#### Install Kong Ingress

```bash
kubectl create configmap kong-plugin-jwtheader --from-file=kong-jwt2header

helm install kong/kong -f kong-values.yaml --generate-name
```

#### Install OpenTelemetry Collector and SigNoz Fullstack App (Optional)
```bash
kubectl create ns signoz

helm --namespace signoz install signoz signoz/signoz
```
#### Apply usual K8S config

```bash
kubectl apply -f .
```

#### Accessing Kong

API gateway can be access through `localhost:80`, for instance User service:

```bash
http://localhost:80/api/user/...
```

#### Access Tracing/Log/Metrics dashboard
Need to expose SigNoz frontend to `localhost:3301` and access

```bash
export SERVICE_NAME=$(kubectl get svc --namespace signoz -l "app.kubernetes.io/component=frontend" -o jsonpath="{.items[0].metadata.name}")

kubectl --namespace signoz port-forward svc/$SERVICE_NAME 3301:3301
```

Next, register a random account (these will not be persistence after clearing k8s)


#For running Elastic-search on k8s deployment
```
minikube start
```
```
helm install elasticsearch-multi-master elastic/elasticsearch -f ./es-master.yaml

helm install elasticsearch-multi-data elastic/elasticsearch -f ./es-data.yaml

helm install elasticsearch-multi-client elastic/elasticsearch -f ./es-client.yaml
```

#### Configing Sharded Mongo


```bash
./mongo/initiate.sh
```
