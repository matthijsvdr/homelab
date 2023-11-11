
## MQTT 

helm repo add emqx https://repos.emqx.io/charts 

helm repo update
helm upgrade --install emqx-operator emqx/emqx-operator \
  --namespace emqx-operator-system \
  --create-namespace


  