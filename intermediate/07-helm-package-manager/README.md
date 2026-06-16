# Helm Package Manager

## What is Helm?

Helm is the **package manager for Kubernetes**. It allows you to define, install, and upgrade even the most complex Kubernetes applications using **Charts** – packages of pre-configured Kubernetes resources.

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Chart** | A collection of files describing a Kubernetes application |
| **Release** | An instance of a chart deployed to a cluster |
| **Repository** | A collection of charts (like a Helm "app store") |
| **Values** | Configuration parameters that customize a chart |
| **Template** | Go template files that generate Kubernetes manifests |

## Chart Directory Structure

```
my-chart/
├── Chart.yaml          # Chart metadata (name, version, description)
├── values.yaml         # Default configuration values
├── charts/             # Dependencies (sub-charts)
├── templates/          # Kubernetes manifest templates
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── configmap.yaml
│   ├── _helpers.tpl    # Template helpers and partials
│   └── NOTES.txt       # Post-install instructions
└── .helmignore         # Files to ignore when packaging
```

## Essential Commands

### Repository Management
```bash
# Add a chart repository
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add stable https://charts.helm.sh/stable

# Update repository metadata
helm repo update

# Search for charts
helm search repo nginx
helm search hub wordpress    # Search Artifact Hub
```

### Installation and Management
```bash
# Install a chart (creates a release)
helm install my-release bitnami/nginx

# Install with custom values
helm install my-release bitnami/nginx -f my-values.yaml

# Install with inline overrides
helm install my-release bitnami/nginx \
  --set replicaCount=3 \
  --set service.type=LoadBalancer

# Install in a specific namespace
helm install my-release bitnami/nginx \
  --namespace my-namespace \
  --create-namespace

# List all releases
helm list
helm list --all-namespaces

# Upgrade a release
helm upgrade my-release bitnami/nginx --set replicaCount=5

# Rollback to a previous revision
helm rollback my-release 1

# View release history
helm history my-release

# Uninstall a release
helm uninstall my-release
```

### Chart Development
```bash
# Create a new chart scaffold
helm create my-chart

# Render templates (dry-run without applying)
helm template my-release ./my-chart

# Validate chart syntax
helm lint ./my-chart

# Package a chart into a .tgz archive
helm package ./my-chart

# Install with debug output
helm install my-release ./my-chart --debug --dry-run
```

### Inspecting Charts and Releases
```bash
# Show chart values
helm show values bitnami/nginx

# Show all chart info
helm show all bitnami/nginx

# Get rendered manifests of a release
helm get manifest my-release

# Get values used in a release
helm get values my-release

# Get status of a release
helm status my-release
```

## Full-Featured Example Chart

See the `full-chart/` directory for a production-ready chart demonstrating:
- `_helpers.tpl` for reusable template partials
- Conditional rendering with `if`/`else`
- Range loops for environment variables
- `NOTES.txt` for post-install messages
- Named templates and includes
