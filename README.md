# Weave Gitops Quickstart
It contains quickstart resources to get you started with [weave gitops enterprise](https://docs.gitops.weave.works/):

- [Quickstart Templates](./quickstart-templates): a set of [weave gitops templates]((https://docs.gitops.weave.works/docs/gitops-templates/templates/))
  to get started using weave gitops enterprise.

## Requirements

- You have [weave gitops enterprise](https://www.weave.works/product/gitops-enterprise/)

## Getting Started

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

