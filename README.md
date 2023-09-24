# Tool required

1. helm: 
```
brew install helm
```
1. kubectl:
```
brew install kubectl
```

# Setting up the cluster

1. Create a cluster
1. Deploy ingress-nginx
    helm install ingress-nginx .
    hell dependency build && helm install ingress-nginx .
1. Setup DNS records with the ingress-nginx external IP
1. Setup service account json secret so that cloud proxy can connect to the database: Follow https://cloud.google.com/sql/docs/mysql/connect-kubernetes-engine#gsa
1. Deploy neferdata without SSL
    run  helm dependency update && helm install neferdata . --dry-run to test, if happy run
    helm dependency update && helm install neferdata . 
1. Deploy cert-manager
1. Create a cert-manager issuer
1. Upgrade neferdata to include SSL

# Updating ui and api

1. cd to the neferdata folder
1. modify the values.yaml file
1. switch the kubectl context to point to the gke neferdata cluster.
```
kubectl config use-context gke_cldshld_us-central1_neferdata   
```
1. apply your changes with:
```
cd helm/neferdata
helm dependency update && helm upgrade neferdata .
```
1. Ensure that all pods are healthy by running: 

```
darioalessandro@MacBook-Pro-di-Dario neferdata % kubectl get pods
NAME                                        READY   STATUS    RESTARTS   AGE
cert-manager-55b858df44-zhmsz               1/1     Running   0          38m
cert-manager-cainjector-7f47598f9b-8vfpb    1/1     Running   0          64m
cert-manager-webhook-7d694cd764-rs5zs       1/1     Running   0          64m
ingress-nginx-controller-6b448794df-jr22b   1/1     Running   0          129m
neferdata-api-b6bd759f5-bqnw7               2/2     Running   0          12m
neferdata-ui-7d5fbdfc4d-v9nwl               1/1     Running   0          6s
```
 
# Frequently used commands

1. Connect to a running pod:

```
kubectl exec -it neferdata-api-db6db8d46-dqsfk -- /bin/bash   
```