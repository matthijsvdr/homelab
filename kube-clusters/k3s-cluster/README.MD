# k3s cluster

## Nodes
The nodes where installed with ubuntu 22.04 LTS
The network interfaces where bonded together into `bond0` with a `balance-xor`` config.
The ipv4 address where set static see [hosts.ini](hosts.ini)

For longhorn the nfs client was installed `sudo apt-get install nfs-common`

The larger ssd was mounted on `/mnt/data/`
m.2 nvme drive was used for the os

## Ansible
Api endpoint
10.20.10.1
See the generic [readme](../README.MD#ansible)

## cert-manager
See the generic [readme](../README.MD#cert-manager)

## Traefik
To create a username and password run the following and replace the secret <br>
`htpasswd -nb username password | openssl base64`

```bash
helm install traefik traefik/traefik --namespace=traefik --create-namespace  --values=kube-clusters/k3s-cluster/traefik/helm-values.yaml

kubectl apply -f kube-clusters/k3s-cluster/traefik/default-headers.yaml
kubectl apply -f kube-clusters/k3s-cluster/traefik/dashboard.yaml
# To make changes
helm upgrade traefik traefik/traefik --namespace=traefik --values=kube-clusters/k3s-cluster/traefik/helm-values.yaml
```

## Rancher

Import the cluster via rancher and follow the instructions

## Longhorn

Longhorn was installed via the rancher market place.

The default datapath was changed to `/mnt/data/longhorn`