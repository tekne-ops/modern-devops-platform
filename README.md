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

## Prometheus & Grafana Setup

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install kube-prometheus prometheus-community/kube-prometheus-stack
helm install loki grafana/loki-stack
```

```bash
kubectl patch svc kube-prometheus-grafana -n monitoring \
  -p '{"spec": {"type": "NodePort"}}'
```

```bash
kubectl get secret kube-prometheus-grafana -n monitoring \
  -o jsonpath="{.data.admin-password}" | base64 -d
```

## Trivy Security Scanning

```bash
sudo pacman -Sy --needed trivy
trivy config .
trivy image ghcr.io/YOUR_USER/devops-lab:latest
trivy image --severity HIGH,CRITICAL ghcr.io/tekne-ops/devops-lab:latest
```