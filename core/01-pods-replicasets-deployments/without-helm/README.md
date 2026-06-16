# Pods, ReplicaSets and Deployments

## Concepts

- **Pod**: The smallest deployable unit in Kubernetes. Contains one or more containers that share network and storage.
- **ReplicaSet**: Ensures a specified number of Pod replicas are running at any time. Usually managed by a Deployment.
- **Deployment**: Provides declarative updates for Pods and ReplicaSets. Enables rolling updates and rollbacks.

## Files

| File | Description |
|------|-------------|
| `pod.yaml` | A single nginx Pod |
| `replicaset.yaml` | A ReplicaSet maintaining 3 nginx replicas |
| `deployment.yaml` | A Deployment managing nginx Pods |

## Exercises

```bash
# Apply a single Pod
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod nginx-pod

# Delete the Pod and observe it does NOT restart (no controller)
kubectl delete pod nginx-pod

# Apply a ReplicaSet
kubectl apply -f replicaset.yaml
kubectl get rs
kubectl get pods

# Delete one Pod – the ReplicaSet recreates it
kubectl delete pod <pod-name>
kubectl get pods

# Apply a Deployment (preferred over bare ReplicaSet)
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl rollout status deployment/nginx-deployment

# Scale the Deployment
kubectl scale deployment/nginx-deployment --replicas=5
kubectl get pods

# Update the image (triggers a rolling update)
kubectl set image deployment/nginx-deployment nginx=nginx:1.26
kubectl rollout status deployment/nginx-deployment

# Roll back to the previous version
kubectl rollout undo deployment/nginx-deployment

# Cleanup
kubectl delete -f deployment.yaml
kubectl delete -f replicaset.yaml
```
