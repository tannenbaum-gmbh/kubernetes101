# Gateway API

## Concepts

The **Gateway API** is the next generation of Kubernetes traffic routing. It is more expressive, extensible, and role-oriented than the classic `Ingress` resource.

## Key Resources

| Resource | Scope | Description |
|----------|-------|-------------|
| **GatewayClass** | Cluster | Names a controller implementation (e.g. NGINX, Envoy). Managed by infrastructure teams. |
| **Gateway** | Namespace | An instance of a GatewayClass. Describes a network endpoint and its listeners. |
| **HTTPRoute** | Namespace | Defines HTTP routing rules from a Gateway to backend Services. |

## Gateway API vs Ingress

| Feature | Ingress | Gateway API |
|---------|---------|-------------|
| Role separation | Single resource | GatewayClass / Gateway / Route |
| Protocol support | HTTP / HTTPS only | HTTP, TCP, TLS, gRPC, … |
| Header / query matching | Controller-specific annotations | Native rule matching |
| Status feedback | Basic | Structured conditions per resource |

## Setup with Minikube

```bash
# 1. Install the Gateway API standard CRDs
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.2.0/standard-install.yaml

# 2. Install NGINX Gateway Fabric (controller + CRDs)
kubectl apply -f https://raw.githubusercontent.com/nginxinc/nginx-gateway-fabric/v1.4.0/deploy/crds.yaml
kubectl apply -f https://raw.githubusercontent.com/nginxinc/nginx-gateway-fabric/v1.4.0/deploy/default/deploy.yaml

# 3. Wait for the controller to become available
kubectl wait --timeout=5m -n nginx-gateway deployment/nginx-gateway --for=condition=Available

# 4. Expose the gateway service (LoadBalancer) via minikube tunnel (keep running in a separate terminal)
minikube tunnel
```

## Exercises

```bash
# Deploy the two backend services
kubectl apply -f deployments.yaml

# Deploy the GatewayClass, Gateway, and HTTPRoute
kubectl apply -f gateway.yaml

# Check resource status
kubectl get gatewayclass nginx
kubectl get gateway app-gateway
kubectl get httproute app-httproute

# Wait until the Gateway has an address assigned
kubectl wait --timeout=2m gateway/app-gateway --for=jsonpath='{.status.addresses[0].value}'

# Retrieve the external IP assigned by minikube tunnel
GATEWAY_IP=$(kubectl get gateway app-gateway -o jsonpath='{.status.addresses[0].value}')

# Add to /etc/hosts
echo "$GATEWAY_IP app.example.local" | sudo tee -a /etc/hosts

# Test path-based routing
curl http://app.example.local/v1   # -> Hello from v1
curl http://app.example.local/v2   # -> Hello from v2

# Inspect the resources
kubectl describe gateway app-gateway
kubectl describe httproute app-httproute

# Cleanup
kubectl delete -f .
sudo sed -i '/app.example.local/d' /etc/hosts
```
