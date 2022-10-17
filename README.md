# iot-device-mgmt-web-config

config repo for iot-device-mgmt-web

## Required configuration

The deployment that is created from this configuration repository depends on a ConfigMap that is supposed to contain the keycloak config to use with the frontend. This config file should be copied and adapted from the default version as can be seen here: https://github.com/diwise/iot-device-mgmt-web/blob/main/diwiseweb/public/config/keycloak.json

Environment configurations that wish to use this frontend should therefore add their own ConfigMap named `devmgmt-web-config`. Example:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

namespace: my-diwise-namespace

resources:
- ssh://github.com/diwise/diwise/deployments/k8s?depth=1
# - ... and then some ...

configMapGenerator:
  - name: devmgmt-web-config
    files:
      - keycloak.json=./config/my-own-config.json
```
