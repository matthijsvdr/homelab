
# Rancher cluster
## Ansible
See the generic [readme](../README.MD#ansible)

# Traefik

```bash
helm install traefik traefik/traefik --namespace=traefik --create-namespace  --values=kube-clusters/rancher-cluster/traefik/helm-values.yaml

kubectl apply -f kube-clusters/rancher-cluster/traefik/default-headers.yaml
kubectl apply -f kube-clusters/rancher-cluster/traefik/dashboard/secret-dashboard.yaml
kubectl apply -f kube-clusters/rancher-cluster/traefik/dashboard/middleware.yaml
kubectl apply -f kube-clusters/rancher-cluster/traefik/dashboard/ingress.yaml
# To make changes
helm upgrade traefik traefik/traefik --namespace=traefik --values=kube-clusters/rancher-cluster/traefik/helm-values.yaml
```

## cert-manager

See the generic [readme](../README.MD#cert-manager)

## rancher

```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable

kubectl create namespace cattle-system
kubectl apply -f kube-clusters/rancher-cluster/cert-manager/certificates/production/rancher-local-mvd.yaml
kubectl apply -f kube-clusters/rancher-cluster/rancher/ingress.yaml
helm install rancher rancher-stable/rancher --namespace cattle-system --values=kube-clusters/rancher-cluster/rancher/values.yaml


kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{ .data.bootstrapPassword|base64decode}}{{ "\n" }}'

```