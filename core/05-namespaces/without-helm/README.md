# Namespaces

## Concepts

Namespaces provide virtual clusters within a physical cluster. They are useful for:
- **Multi-tenancy**: Isolating different teams or projects
- **Environment separation**: `dev`, `staging`, `production`
- **Resource quotas**: Limiting CPU/memory per team

## Default Namespaces

| Namespace | Purpose |
|-----------|---------|
| `default` | Default namespace for resources without an explicit namespace |
| `kube-system` | Kubernetes system components |
| `kube-public` | Publicly accessible cluster information |
| `kube-node-lease` | Node heartbeat leases |

## Files

| File | Description |
|------|-------------|
| `namespace.yaml` | Creates the `training` namespace |
| `deployment-in-namespace.yaml` | Deployment scoped to `training` |
| `resource-quota.yaml` | Limits resources in the `training` namespace |
| `limit-range.yaml` | Default container limits for the `training` namespace |

## Exercises

```bash
# Create namespace
kubectl apply -f namespace.yaml
kubectl get namespaces

# Deploy resources into the namespace
kubectl apply -f deployment-in-namespace.yaml
kubectl apply -f resource-quota.yaml
kubectl apply -f limit-range.yaml

# List resources in the namespace
kubectl get all -n training

# Set default namespace for current context
kubectl config set-context --current --namespace=training

# Cross-namespace DNS: <service>.<namespace>.svc.cluster.local
# e.g. nginx-svc.training.svc.cluster.local

# Describe quota usage
kubectl describe resourcequota training-quota -n training

# Reset default namespace
kubectl config set-context --current --namespace=default

# Cleanup
kubectl delete namespace training
```
