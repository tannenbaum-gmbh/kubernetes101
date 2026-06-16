# Kubernetes 101

Training content for Kubernetes core and intermediate concepts, with and without Helm.

## Getting Started

### Devcontainer (Recommended)

This repository includes a [Dev Container](https://containers.dev/) configuration based on the [kubernetes-helm-minikube template](https://github.com/devcontainers/templates/tree/main/src/kubernetes-helm-minikube).

**Tools included:**
- `kubectl` – Kubernetes CLI
- `helm` – Kubernetes Package Manager
- `minikube` – Local Kubernetes cluster
- `k9s` – Terminal UI for Kubernetes
- Docker-in-Docker

**Start the cluster after opening the devcontainer:**
```bash
minikube start
kubectl get nodes
```

### Prerequisites (without devcontainer)

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/) or access to a Kubernetes cluster
- [helm](https://helm.sh/docs/intro/install/)
- [k9s](https://k9scli.io/topics/install/) (optional)

---

## Course Structure

### Core Kubernetes Principles

| # | Topic | Without Helm | With Helm |
|---|-------|-------------|-----------|
| 1 | [Pods, ReplicaSets and Deployments](core/01-pods-replicasets-deployments) | [without-helm](core/01-pods-replicasets-deployments/without-helm) | [with-helm](core/01-pods-replicasets-deployments/with-helm) |
| 2 | [Deployment Strategies](core/02-deployment-strategies) | [without-helm](core/02-deployment-strategies/without-helm) | [with-helm](core/02-deployment-strategies/with-helm) |
| 3 | [Networking Services](core/03-networking-services) | [without-helm](core/03-networking-services/without-helm) | [with-helm](core/03-networking-services/with-helm) |
| 4 | [ConfigMaps and Secrets](core/04-configmaps-secrets) | [without-helm](core/04-configmaps-secrets/without-helm) | [with-helm](core/04-configmaps-secrets/with-helm) |
| 5 | [Namespaces](core/05-namespaces) | [without-helm](core/05-namespaces/without-helm) | [with-helm](core/05-namespaces/with-helm) |

### Intermediate Kubernetes Topics

| # | Topic | Without Helm | With Helm |
|---|-------|-------------|-----------|
| 1 | [Volumes and Persistence](intermediate/01-volumes-persistence) | [without-helm](intermediate/01-volumes-persistence/without-helm) | [with-helm](intermediate/01-volumes-persistence/with-helm) |
| 2 | [Multi-Container Pods and Init Containers](intermediate/02-multi-container-pods) | [without-helm](intermediate/02-multi-container-pods/without-helm) | [with-helm](intermediate/02-multi-container-pods/with-helm) |
| 3 | [Ingress](intermediate/03-ingress) | [without-helm](intermediate/03-ingress/without-helm) | [with-helm](intermediate/03-ingress/with-helm) |
| 4 | [Jobs and CronJobs](intermediate/04-jobs-cronjobs) | [without-helm](intermediate/04-jobs-cronjobs/without-helm) | [with-helm](intermediate/04-jobs-cronjobs/with-helm) |
| 5 | [DaemonSets](intermediate/05-daemonsets) | [without-helm](intermediate/05-daemonsets/without-helm) | [with-helm](intermediate/05-daemonsets/with-helm) |
| 6 | [Health Probes](intermediate/06-health-probes) | [without-helm](intermediate/06-health-probes/without-helm) | [with-helm](intermediate/06-health-probes/with-helm) |
| 7 | [Helm Package Manager](intermediate/07-helm-package-manager) | – | [full-chart](intermediate/07-helm-package-manager/full-chart) |

---

## Quick Reference

```bash
# Cluster status
kubectl cluster-info
kubectl get nodes

# List resources
kubectl get pods,deployments,services

# Inspect a resource
kubectl describe pod <pod-name>

# Apply a manifest
kubectl apply -f <file.yaml>

# Delete a resource
kubectl delete -f <file.yaml>

# Port-forward to a service
kubectl port-forward service/<svc-name> 8080:80

# Execute command in a Pod
kubectl exec -it <pod-name> -- bash

# View logs
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>   # multi-container

# k9s
k9s   # Opens interactive TUI
```
Training for kubernetes core concepts
