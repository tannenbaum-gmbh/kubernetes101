# ConfigMaps and Secrets

## Concepts

- **ConfigMap**: Stores non-confidential configuration data as key-value pairs. Can be consumed as environment variables or mounted as files.
- **Secret**: Stores sensitive data (passwords, tokens, keys). Data is base64-encoded (not encrypted by default – use encryption at rest in production).

## Secret Types

| Type | Description |
|------|-------------|
| `Opaque` | Arbitrary user-defined data |
| `kubernetes.io/tls` | TLS certificate and key |
| `kubernetes.io/dockerconfigjson` | Docker registry credentials |
| `kubernetes.io/service-account-token` | Service account token |

## Files

| File | Description |
|------|-------------|
| `configmap.yaml` | ConfigMap with key-value pairs and a file entry |
| `secret.yaml` | Secret with base64-encoded credentials |
| `pod-with-config.yaml` | Pod consuming both ConfigMap and Secret |

## Exercises

```bash
# Create ConfigMap and Secret
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml

# Inspect
kubectl describe configmap app-config
kubectl get secret app-secret -o yaml

# Decode a secret value
kubectl get secret app-secret -o jsonpath='{.data.DB_PASSWORD}' | base64 --decode

# Create Pod that uses them
kubectl apply -f pod-with-config.yaml
kubectl exec app-pod -- env | grep -E 'APP_ENV|DB_'

# Create ConfigMap imperatively
kubectl create configmap env-config --from-literal=LOG_LEVEL=debug

# Create Secret imperatively
kubectl create secret generic db-creds \
  --from-literal=username=admin \
  --from-literal=******

# Cleanup
kubectl delete -f .
```
