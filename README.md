# Portfolio Helm Charts

## Structure
- `catalog-service/`, `users-service/`, `orders-service/`: individual charts for each microservicio.
- `portfolio-stack/`: umbrella chart that pulls the three services as dependencies.
- `values-dev.yaml`, `values-prod.yaml`: sample overlays for dev/prod registries.
- `install-all.ps1`: helper script that runs `helm dependency update` and installs `portfolio-stack`.

## Quick Start
```powershell
cd helm
./install-all.ps1 -Namespace portfolio
```
This updates dependencies and deploys the umbrella chart using `values-dev.yaml`.

To override container tags:
```bash
helm upgrade --install portfolio-stack ./portfolio-stack \
  --namespace portfolio \
  --set catalog-service.image.tag=2025.11.06 \
  --set users-service.image.tag=2025.11.06 \
  --set orders-service.image.tag=2025.11.06
```

## Publishing
1. Initialize a Git repository in this folder (`git init`, add remote `https://github.com/rrajo-portfolio/helm.git`).
2. `git add . && git commit -m "feat: add portfolio stack chart"`.
3. Push once the remote repository exists: `git push -u origin main`.
