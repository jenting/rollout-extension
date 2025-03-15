# Rollout Extension

The project introduces the Argo Rollout dashboard into the Argo CD Web UI.

![image](https://user-images.githubusercontent.com/426437/136460261-00d3dc31-ad20-4044-a7be-091803b8678f.png)

## Install UI extension

To init container cp the JS file to `/tmp/extensions`.

### Kustomize Patch

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: argocd-server
spec:
  template:
    spec:
      initContainers:
      - command:
        - /bin/cp
        - /output/extensions-Rollout.js
        - /tmp/extensions/extensions-Rollout.js
        image: ghcr.io/jenting/rollout-extension:v0.3.7
        name: rollout-extension
        volumeMounts:
        - mountPath: /tmp/extensions/
          name: extensions
      containers:
        - name: argocd-server
          volumeMounts:
            - name: extensions
              mountPath: /tmp/extensions/
      volumes:
        - name: extensions
          emptyDir: {}
```
