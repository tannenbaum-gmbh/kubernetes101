# Gateway API – with Helm

## Exercises

```bash
# Install the Gateway API CRDs and NGINX Gateway Fabric controller (once per cluster)
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.2.0/standard-install.yaml
kubectl apply -f https://raw.githubusercontent.com/nginxinc/nginx-gateway-fabric/v1.4.0/deploy/crds.yaml
kubectl apply -f https://raw.githubusercontent.com/nginxinc/nginx-gateway-fabric/v1.4.0/deploy/default/deploy.yaml
kubectl wait --timeout=5m -n nginx-gateway deployment/nginx-gateway --for=condition=Available

# Start minikube tunnel to expose the LoadBalancer (keep running in a separate terminal)
minikube tunnel

# Install the chart (creates GatewayClass, Gateway, HTTPRoute, Deployment, Service)
helm install my-app ./chart

# Override hostname and response text
helm upgrade my-app ./chart \
  --set gateway.host=myapp.local \
  --set appText="Hello from my Helm Gateway release!"

# Skip GatewayClass creation if it already exists in the cluster
helm upgrade my-app ./chart --set gateway.createGatewayClass=false

# Check Gateway status
kubectl get gateway my-app-gateway
kubectl get httproute my-app-httproute

# Cleanup
helm uninstall my-app
```
