
## Prerequisites


#### Add kong to `helm` repo

```bash
helm repo add kong https://charts.konghq.com
```


## Running K8S

#### Create Secret for Github PAT

```bash
kubectl create secret docker-registry gh-regcred --docker-server=ghcr.io --docker-username=GITHUB_USERNAME --docker-password=GITHUB_PAT
```


#### Install Kong Ingress

```bash
kubectl create configmap kong-plugin-jwtheader --from-file=kong-jwt2header
```

```bash
helm install kong/kong -f kong-values.yaml --generate-name
```


#### Apply usual K8S config

```bash
kubectl apply -f .
```

#### Accessing

API gateway can be access through localhost:80, for instance User service:

```bash
http://localhost:80/api/user/...
```