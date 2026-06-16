# Multi-Container Pods and Init Containers

## Multi-Container Patterns

| Pattern | Description |
|---------|-------------|
| **Sidecar** | Extends and enhances the main container (logging, monitoring, sync) |
| **Ambassador** | Proxies communication between the main container and external services |
| **Adapter** | Transforms output from the main container into a standardized format |

## Init Containers

Init containers run **sequentially to completion** before any main container starts. Use cases:
- Wait for a dependency (database, service)
- Pre-populate a shared volume
- Register the Pod with external systems

## Files

| File | Description |
|------|-------------|
| `sidecar-pod.yaml` | Nginx + log-sidecar sharing an emptyDir volume with an init container |
| `ambassador-pod.yaml` | App container + nginx ambassador proxy |
| `init-container-pod.yaml` | Pod with two init containers (wait + prepare) |

## Exercises

```bash
# Sidecar
kubectl apply -f sidecar-pod.yaml
kubectl get pod sidecar-pod

# Follow logs of each container
kubectl logs sidecar-pod -c nginx
kubectl logs sidecar-pod -c log-sidecar

# Init container – will loop because 'myservice' doesn't exist
kubectl apply -f init-container-pod.yaml
kubectl get pod init-demo   # Shows Init:0/2, then Init:1/2 ...
kubectl logs init-demo -c wait-for-service

# Exec into a specific container
kubectl exec sidecar-pod -c nginx -- curl localhost

# Cleanup
kubectl delete -f .
```
