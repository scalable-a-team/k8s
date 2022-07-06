
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
helm install kong/kong --generate-name --set ingressController.installCRDs=false
```


#### Apply usual K8S config

```bash
kubectl apply -f .
```

