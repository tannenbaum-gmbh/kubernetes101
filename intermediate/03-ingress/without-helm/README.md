# Ingress

## Concepts

Ingress exposes HTTP/HTTPS routes from outside the cluster to services within the cluster. An **Ingress Controller** (e.g., nginx, Traefik) must be running to handle Ingress resources.

## Routing Types

| Type | Description |
|------|-------------|
| **Host-based** | Route by hostname (`app.example.com`) |
| **Path-based** | Route by URL path (`/api`, `/web`) |
| **TLS termination** | Terminate HTTPS at the Ingress |

## Setup with Minikube

```bash
# Enable the nginx Ingress addon
minikube addons enable ingress

# Verify the controller is running
kubectl get pods -n ingress-nginx
```

## Exercises

```bash
# Enable Ingress in minikube
minikube addons enable ingress

# Deploy backends and ingress
kubectl apply -f deployments.yaml
kubectl apply -f ingress.yaml

# Get minikube IP
minikube ip

# Add to /etc/hosts (replace <MINIKUBE_IP>)
echo "<MINIKUBE_IP> app.example.local" | sudo tee -a /etc/hosts

# Test routing
curl http://app.example.local/v1   # -> Hello from v1
curl http://app.example.local/v2   # -> Hello from v2

# Describe ingress
kubectl describe ingress app-ingress

# Cleanup
kubectl delete -f .
sudo sed -i '/app.example.local/d' /etc/hosts
```
