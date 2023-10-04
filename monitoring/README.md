# Monitoring

The monitoring stack is deployed as [Flux Kustomization](https://github.com/weaveworks/weave-gitops-quickstart/tree/add-monitoring) that includes:

- Prometheus
- Grafana
- Kubernetes Dashboards
- Flux Dashboards
- Weave Gitops Grafana dashboards

## Requirements

- You have [Weave GitOps Enterprise](https://www.weave.works/product/gitops-enterprise/) installed on a cluster.
- You have [Weave GitOps Enterprise](https://www.weave.works/product/gitops-enterprise/) installed on a cluster.

## Getting Started

Deploy the following resources 

```yaml
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: weave-gitops-quickstart
  namespace: flux-system
spec:
  interval: 1m0s
  ref:
    branch: add-monitoring
  url: https://github.com/weaveworks/weave-gitops-quickstart
---
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: monitoring-config
  namespace: flux-system
spec:
  interval: 1m0s
  sourceRef:
    kind: GitRepository
    name: weave-gitops-quickstart-monitoring
  path: ./monitoring
  prune: true
 
```
### Quickstart Templates

Deploy the templates using flux with the following manifests.

```
apiVersion: source.toolkit.fluxcd.io/v1beta2
kind: GitRepository
metadata:
  name: weave-gitops-quickstart
  namespace: flux-system
spec:
  interval: 10m0s
  ref:
    branch: main
  url: https://github.com/weaveworks/weave-gitops-quickstart
---
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: quickstart-templates
  namespace: flux-system
spec:
  chart:
    spec:
      chart: "quickstart-templates"
      version: ">=0.1.0"
      sourceRef:
        kind: GitRepository
        name: weave-gitops-quickstart
        namespace: flux-system
  interval: 10m0s
```

## Contributing

Just use this repo to open issues and contribute code via pull requests. 

