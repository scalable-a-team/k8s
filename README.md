
## Prerequisites


#### Add kong to `helm` repo

```bash
helm repo add kong https://charts.konghq.com
```


## Running K8S

#### Create Secret for Github PAT

```bash
kubectl create secret docker-registry gh-regcred --docker-server=ghcr.io --docker-username=nakarinh14 --docker-password=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
```


#### Install Kong Ingress

```bash
helm install kong/kong --generate-name --set ingressController.installCRDs=false
```


#### Apply usual K8S config

```bash
kubectl apply -f .
```

