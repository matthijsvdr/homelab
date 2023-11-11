# Intel gpu support

helm install gpu intel/intel-device-plugins-gpu --namespace inteldeviceplugins-system --create-namespace --set nodeFeatureRule=true