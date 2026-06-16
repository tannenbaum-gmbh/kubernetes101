# Networking Services – with Helm

## Exercises

```bash
# Install with ClusterIP (default)
helm install my-svc ./chart

# Upgrade to NodePort
helm upgrade my-svc ./chart --set service.type=NodePort --set service.nodePort=30080

# Upgrade to LoadBalancer
helm upgrade my-svc ./chart --set service.type=LoadBalancer

# Cleanup
helm uninstall my-svc
```
