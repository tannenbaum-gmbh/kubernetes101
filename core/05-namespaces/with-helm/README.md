# Namespaces – with Helm

## Exercises

```bash
# Install – creates namespace, deployment, service, and resource quota
helm install my-app ./chart

# Install into a different namespace
helm install my-app ./chart \
  --set namespace.name=production \
  --set resourceQuota.enabled=false

# List resources in the created namespace
kubectl get all -n training

# Cleanup
helm uninstall my-app
kubectl delete namespace training
```
