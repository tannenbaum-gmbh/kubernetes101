# Ingress – with Helm

## Exercises

```bash
# Enable ingress in minikube first
minikube addons enable ingress

# Install with Ingress enabled (default)
helm install my-app ./chart

# Override host and text
helm upgrade my-app ./chart \
  --set ingress.host=myapp.local \
  --set appText="Hello from my custom release!"

# Disable ingress
helm upgrade my-app ./chart --set ingress.enabled=false

# Cleanup
helm uninstall my-app
```
