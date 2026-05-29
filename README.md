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