# 1Password

## 1password connect and operator

```bash

helm repo add 1password https://1password.github.io/connect-helm-charts/

helm install 1password 1password/connect --namespace security --create-namespace --set-file connect.credentials=/Users/matthijs/Downloads/1password-credentials.json  --set operator.create=true --set operator.token.value=MAKE_TOKEN_ON_1P_SITE

```

## Example secret creation

```yaml
apiVersion: onepassword.com/v1
kind: OnePasswordItem
metadata:
  name: super-test
spec:
  itemPath: "vaults/Kubernetes/items/super-test"
```

