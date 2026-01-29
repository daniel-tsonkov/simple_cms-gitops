# Simple CMS GitOps Repository
k8s/
├── namespace.yaml       # Namespace definition
├── deployment.yaml      # Application deployments (auto-updated by CI/CD)
├── service.yaml         # Kubernetes services
└── servicemonitor.yaml  # Prometheus monitoring configuration

## 🔄 GitOps Workflow

1. **CI/CD Pipeline** (in `daniel-tsonkov/simple_cms`):
   - Builds and tests the application
   - Creates Docker images
   - Scans for vulnerabilities
   - Updates `deployment.yaml` in this repository with new image tags

2. **ArgoCD**:
   - Monitors this repository for changes
   - Automatically syncs changes to the Kubernetes cluster
   - Provides rollback capabilities

## 🚀 Deployment

The application is deployed using ArgoCD. See the ArgoCD Application manifest in the main repository:
`daniel-tsonkov/simple_cms/argocd/application.yaml`

## 📝 Making Changes

### Automated Updates (Recommended)
Image tags in `deployment.yaml` are automatically updated by the CI/CD pipeline when new versions are built.

### Manual Updates
If you need to make manual changes:
```bash
# Clone the repository
git clone https://github.com/daniel-tsonkov/simple_cms-gitops.git
cd simple_cms-gitops

# Make your changes
vi k8s/deployment.yaml

# Commit and push
git add k8s/
git commit -m "Update: description of changes"
git push origin main
```

ArgoCD will detect the changes and sync them to the cluster.

## 🔍 Monitoring

- **Namespace**: `simple-cms`
- **Services**:
  - `simple-cms-backend`: Backend API service
  - `simple-cms-frontend`: Frontend web interface
- **Metrics**: Exposed via ServiceMonitor for Prometheus

## 🔗 Related Repositories

- **Main Application**: [daniel-tsonkov/simple_cms](https://github.com/daniel-tsonkov/simple_cms)
- **GitOps Repo**: [daniel-tsonkov/simple_cms-gitops](https://github.com/daniel-tsonkov/simple_cms-gitops) (this repository)

## ⚠️ Important Notes

- **Do NOT edit `deployment.yaml` manually** unless you know what you're doing
- Image tags are managed by the CI/CD pipeline
- All changes should be committed through Git (GitOps principle)
- ArgoCD provides automatic rollback if deployment fails

## 📚 Documentation

For more information about the complete DevOps pipeline, see the main repository documentation.
EOF

# Commit and push
git add .
git commit -m "Initial commit: Kubernetes manifests for GitOps deployment"
git push origin main