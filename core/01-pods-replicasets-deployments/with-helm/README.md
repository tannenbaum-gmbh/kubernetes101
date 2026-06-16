# Pods, ReplicaSets and Deployments – with Helm

## Chart Structure

```
chart/
├── Chart.yaml          # Chart metadata
├── values.yaml         # Default configuration values
└── templates/
    ├── deployment.yaml # Deployment template
    └── service.yaml    # Service template
```

## Exercises

```bash
# Install the chart
helm install my-webapp ./chart

# List releases
helm list

# Inspect rendered templates
helm template my-webapp ./chart

# Override values (scale up)
helm upgrade my-webapp ./chart --set replicaCount=5

# Override image tag
helm upgrade my-webapp ./chart --set image.tag=1.26

# View revision history
helm history my-webapp

# Rollback to previous revision
helm rollback my-webapp 1

# Cleanup
helm uninstall my-webapp
```
