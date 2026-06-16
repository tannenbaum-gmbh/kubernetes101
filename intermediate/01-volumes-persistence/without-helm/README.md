# Volumes and Persistence

## Concepts

| Resource | Description |
|----------|-------------|
| **PersistentVolume (PV)** | Cluster-level storage resource |
| **PersistentVolumeClaim (PVC)** | User's request for storage |
| **StorageClass** | Enables dynamic provisioning of PVs |
| **StatefulSet** | Manages stateful Pods; each Pod gets its own PVC |

## Volume Access Modes

| Mode | Short | Description |
|------|-------|-------------|
| `ReadWriteOnce` | RWO | One node can read/write |
| `ReadOnlyMany` | ROX | Many nodes can read |
| `ReadWriteMany` | RWX | Many nodes can read/write |

## Exercises

```bash
# Create PV and PVC
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml

# Check PVC is Bound
kubectl get pv,pvc

# Create Pod using PVC
kubectl apply -f pod-with-pvc.yaml
kubectl exec pvc-pod -- df -h /usr/share/nginx/html

# Write data and verify persistence
kubectl exec pvc-pod -- sh -c "echo 'Hello PV!' > /usr/share/nginx/html/index.html"
kubectl delete pod pvc-pod
kubectl apply -f pod-with-pvc.yaml
kubectl exec pvc-pod -- cat /usr/share/nginx/html/index.html   # Data persists!

# StatefulSet
kubectl apply -f statefulset.yaml
kubectl get statefulset
kubectl get pods  # nginx-statefulset-0, nginx-statefulset-1, nginx-statefulset-2

# Cleanup
kubectl delete -f .
```
