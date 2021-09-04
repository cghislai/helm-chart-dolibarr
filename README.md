# Dolibarr

To deploy this chart, create/adjust your values.yaml file then:

1. Create the namespace resources, and update your pulLSecret if required for local pulls.

```
kubectl create namespace dolibarr
kubectl create secret generic docker-config-json \
         --from-file=.dockerconfigjson=/home/cghislai/.docker/config.json \
         --type=kubernetes.io/dockerconfigjson \
         --namespace dolibarr
kubectl patch serviceaccount default -n dolibarr -p '{"imagePullSecrets": [{"name": "docker-config-json"}]}'
```
1bis: Use minikube mount "/home/cghislai/dev/charlyghislain/res/dolibarr:/minkube-data" if you need to provision
from hostpath /minikube-data.

2. Deploy the stack

```
helm dependency update
helm install -n dolibarr -f values.yaml dolibarr . 
```

1. Adjust your /etc/hosts file. Check the ingress to see hostname / ip mapping required.

```
kubectl get ingress -n dolibarr
```

## Post steps

- Complete install:  

## Provisionning

- Locally, use minikube mount to put the dump in the minikube host, then update values to use hostpath + subPath.
- Provide the pvc any other way on cluster

## Generated secrets

```
echo -n "Dolbarr admin password: " ;\
kubectl  -n dolibarr  get secret dolibarr-dolibarr-secrets -o json | jq -r '.data["admin-password"]' | base64 --dec; \
echo; \
```  

