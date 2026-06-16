# ConfigMaps and Secrets – with Helm

The chart creates a ConfigMap and Secret from `values.yaml` entries. Pod annotations with `sha256sum` checksums ensure Pods restart automatically when config changes.

## Exercises

```bash
# Install the chart
helm install my-app ./chart

# Verify the ConfigMap and Secret were created
kubectl get configmap my-app-config -o yaml
kubectl get secret my-app-secret -o yaml

# Update a config value (Pod will restart due to checksum annotation)
helm upgrade my-app ./chart --set config.APP_ENV=staging

# Cleanup
helm uninstall my-app
```
