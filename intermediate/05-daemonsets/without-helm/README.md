# DaemonSets

## Concepts

A **DaemonSet** ensures that all (or some) nodes run a copy of a Pod. Common use cases:
- **Log collection**: Fluentd, Filebeat
- **Monitoring**: Prometheus Node Exporter, Datadog Agent
- **Networking**: CNI plugins, kube-proxy
- **Storage**: Ceph OSD, GlusterFS

## DaemonSet vs Deployment

| | DaemonSet | Deployment |
|-|-----------|------------|
| Number of Pods | One per Node | Fixed number (replicas) |
| Scaling | Automatic with nodes | Manual/HPA |
| Node selection | All nodes (or by selector/toleration) | Any available node |

## Exercises

```bash
# Apply DaemonSet
kubectl apply -f daemonset.yaml
kubectl get daemonset
kubectl get pods -o wide   # One Pod per node

# Check logs from all DaemonSet Pods
kubectl logs -l app=log-collector

# Node-selector DaemonSet (no GPU nodes -> no pods scheduled)
kubectl apply -f daemonset-node-selector.yaml
kubectl get pods -l app=gpu-monitor   # Empty - no nodes with 'hardware=gpu'

# Label a node (minikube has a single node called 'minikube')
kubectl label node minikube hardware=gpu
kubectl get pods -l app=gpu-monitor   # Now scheduled

# Remove label
kubectl label node minikube hardware-

# Cleanup
kubectl delete -f .
```
