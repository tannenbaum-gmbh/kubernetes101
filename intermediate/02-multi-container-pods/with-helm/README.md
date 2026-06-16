# Multi-Container Pods – with Helm

## Exercises

```bash
# Install with sidecar and init containers (default)
helm install my-app ./chart
kubectl logs my-app-pod -c main
kubectl logs my-app-pod -c sidecar

# Install without sidecar
helm install my-app ./chart --set sidecar.enabled=false

# Cleanup
helm uninstall my-app
```
