# modern-devops-platform

## Docker Build & Push

```bash
cd app/
docker build -t ghcr.io/tekne-ops/devops-lab:latest .
```

```bash
echo "YOUR_GITHUB_PAT" | docker login ghcr.io -u dvaliente-tekne --password-stdin
```

```bash
docker push ghcr.io/tekne-ops/devops-lab:latest
```

## Helm Setup

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

## ArgoCD Setup

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

**Credentials:** username is `admin`, password:

```bash
kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath="{.data.password}" | base64 -d
```