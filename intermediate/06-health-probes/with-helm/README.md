# Health Probes – with Helm

## Exercises

```bash
# Install with all probes enabled (default)
helm install my-app ./chart

# Disable startup probe
helm upgrade my-app ./chart --set probes.startup.enabled=false

# Adjust liveness probe interval
helm upgrade my-app ./chart --set probes.liveness.periodSeconds=30

# Cleanup
helm uninstall my-app
```
