# DaemonSets – with Helm

## Exercises

```bash
# Install (runs on all nodes)
helm install my-ds ./chart

# Restrict to nodes with specific labels
helm upgrade my-ds ./chart --set "nodeSelector.hardware=gpu"

# Cleanup
helm uninstall my-ds
```
