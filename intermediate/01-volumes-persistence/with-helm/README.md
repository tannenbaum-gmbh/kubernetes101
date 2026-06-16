# Volumes and Persistence – with Helm

## Exercises

```bash
# Install with persistence enabled (default)
helm install my-app ./chart
kubectl get pvc

# Install without persistence
helm install my-app ./chart --set persistence.enabled=false

# Cleanup
helm uninstall my-app
kubectl delete pvc my-app-data  # PVCs are not deleted automatically
```
