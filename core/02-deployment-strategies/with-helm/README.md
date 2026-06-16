# Deployment Strategies – with Helm

The chart supports both `RollingUpdate` and `Recreate` strategies via `values.yaml`.

## Exercises

```bash
# Install with default RollingUpdate strategy
helm install my-app ./chart

# Upgrade with Recreate strategy
helm upgrade my-app ./chart --set strategy.type=Recreate

# Upgrade back to RollingUpdate
helm upgrade my-app ./chart \
  --set strategy.type=RollingUpdate \
  --set strategy.rollingUpdate.maxSurge=2 \
  --set strategy.rollingUpdate.maxUnavailable=0

# Cleanup
helm uninstall my-app
```
