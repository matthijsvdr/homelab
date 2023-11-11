# Generic steps for all clusters

## Ansible

- Run the playbook from the k3s-ansible repo
- Steps are generic but update the correct ip's
- Update the ansible.cfg to point to the right inventory

```bash

ansible-playbook ./site.yml --private-key ~/.ssh/k8s.pub

# k3s
scp -i ~/.ssh/k8s.pub root@10.20.10.1:~/.kube/config ~/.kube/config-k3s
# rancher
scp -i ~/.ssh/k8s.pub root@10.20.20.1:~/.kube/config ~/.kube/config-rancher

```

## cert-manager

Custom Resource Definitions are needed 
```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.2/cert-manager.crds.yaml

helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --values=kube-clusters/cert-manager/helm-values.yaml --version v1.13.2

kubectl apply -f kube-clusters/cert-manager/secret-cf-token.yaml

kubectl apply -f kube-clusters/cert-manager/letsencrypt-staging.yaml

kubectl apply -f kube-clusters/cert-manager/letsencrypt-production.yaml

#to test
kubectl apply -f kube-clusters/cert-manager/certificates/staging/local-example-com.yaml


```