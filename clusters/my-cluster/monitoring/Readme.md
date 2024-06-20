# Dependency workaround

PodMonitor trying to be installed before the prom stack - dependency [issue](https://github.com/fluxcd/flux2/discussions/3108)

Solution

- skip PodMonitor for first iteration by adding annotation to PodMonitor manifest
```apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: flux-system
  labels:
    app.kubernetes.io/part-of: flux
    app.kubernetes.io/component: monitoring
  annotations:
    kustomize.toolkit.fluxcd.io/ssa: Ignore
```
- wait for the full stack
- remove annotation
