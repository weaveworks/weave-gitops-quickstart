# Pipeline Promotions Security 

This folder contains a set of resources to use to verify the security setup indicated for 
[pull request promotions](https://docs.gitops.weave.works/docs/next/pipelines/promoting-applications/#pull-request)

## Getting Started

Deploy [podinfo](./podinfo) that contains a pipeline application to test the setup:

```
apiVersion: source.toolkit.fluxcd.io/v1
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
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: pipelines-promotions-security-podinfo
  namespace: flux-system
spec:
  interval: 10m0s
  sourceRef:
    kind: GitRepository
    name: weave-gitops-quickstart
  path: ./pipelines-promotions-security/podinfo
  prune: true
```

Once the application has been reconciled, try to run the test cases within [tests](./tests) to 
create a set of kubernetes resources that would try to read the pipeline secret by different escalations.

```bash 
kubectl apply -f tests --recursive
```

You should see that the resources have been blocked. Weave Gitops UI cluster violations would look similar to: 

![pipeline-security-violations.png](imgs%2Fpipeline-security-violations.png)





