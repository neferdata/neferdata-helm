This process is not completely automated. 

You have to apply cluster-role manually with:

```
kubectl apply -f cluster-role.yaml
```

them install external dns with:

```
helm dependency update && helm install external-dns .
```