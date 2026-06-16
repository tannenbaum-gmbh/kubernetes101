# Networking Services

## Service Types

| Type | Accessibility | Use Case |
|------|--------------|----------|
| `ClusterIP` | Internal only | Microservice communication |
| `NodePort` | External via Node IP + port | Dev/test access |
| `LoadBalancer` | External via cloud LB | Production external exposure |
| `ExternalName` | DNS alias to external service | Abstracting external services |

## Exercises

```bash
# Apply the Deployment and all Services
kubectl apply -f deployment.yaml
kubectl apply -f service-clusterip.yaml
kubectl apply -f service-nodeport.yaml
kubectl apply -f service-loadbalancer.yaml

# List services
kubectl get services

# Test ClusterIP from within the cluster
kubectl run curl --image=curlimages/curl -it --rm -- sh
# Inside the Pod:
# curl http://nginx-clusterip

# Test NodePort (minikube)
minikube service nginx-nodeport --url
curl $(minikube service nginx-nodeport --url)

# Test LoadBalancer (minikube requires tunnel)
minikube tunnel  # Run in another terminal
kubectl get service nginx-loadbalancer  # Wait for EXTERNAL-IP

# Inspect endpoints
kubectl get endpoints

# Cleanup
kubectl delete -f .
```
