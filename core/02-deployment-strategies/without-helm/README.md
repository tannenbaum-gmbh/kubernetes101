# Deployment Strategies

## Strategies

| Strategy | Description | Downtime |
|----------|-------------|----------|
| **RollingUpdate** (default) | Gradually replaces old Pods with new ones. Controlled by `maxSurge` and `maxUnavailable`. | None |
| **Recreate** | Terminates all existing Pods before creating new ones. | Yes |
| **Blue-Green** | Runs two identical environments; traffic is switched by updating the Service selector. | None (instant cutover) |
| **Canary** | Routes a small percentage of traffic to the new version. Usually implemented with multiple Deployments and weighted Services or Ingress. | None |

## Files

| File | Description |
|------|-------------|
| `rolling-update.yaml` | Deployment with `RollingUpdate` strategy |
| `recreate.yaml` | Deployment with `Recreate` strategy |
| `blue-green/blue-deployment.yaml` | Blue (current) version Deployment |
| `blue-green/green-deployment.yaml` | Green (new) version Deployment |
| `blue-green/service.yaml` | Service pointing to blue; update selector to switch to green |

## Exercises

```bash
# --- Rolling Update ---
kubectl apply -f rolling-update.yaml
# Watch the rollout
kubectl rollout status deployment/nginx-rolling
# Trigger an update
kubectl set image deployment/nginx-rolling nginx=nginx:1.26
kubectl rollout status deployment/nginx-rolling

# --- Recreate ---
kubectl apply -f recreate.yaml
kubectl set image deployment/nginx-recreate nginx=nginx:1.26
# Notice all old Pods are terminated first

# --- Blue-Green ---
kubectl apply -f blue-green/
# All traffic goes to blue
kubectl get pods -l app=nginx

# Deploy green in parallel
# Traffic still goes to blue; test green internally

# Switch traffic to green by patching the service selector
kubectl patch service nginx-service -p '{"spec":{"selector":{"version":"green"}}}'

# Verify traffic switched
kubectl describe service nginx-service

# Cleanup
kubectl delete -f blue-green/
kubectl delete -f rolling-update.yaml
kubectl delete -f recreate.yaml
```
