# Kubernetes and Helm (and other stuff)

- [Kubernetes and Helm (and other stuff)](#kubernetes-and-helm-and-other-stuff)
  - [Kubernetes Articles](#kubernetes-articles)
  - [Kubernetes Tools](#kubernetes-tools)
  - [Kubernetes Notes](#kubernetes-notes)
    - [Kubernetes Overview](#kubernetes-overview)
    - [Components](#components)
  - [Kubernetes commands](#kubernetes-commands)
    - [Getting a shell to a running container](#getting-a-shell-to-a-running-container)
  - [Inter pod communication](#inter-pod-communication)

## Kubernetes Articles

- <https://medium.com/google-cloud/kubernetes-101-pods-nodes-containers-and-clusters-c1509e409e16>
- <https://kubernetes.io/docs/concepts/workloads/pods/>

- Kuberenetes with Nana <https://www.youtube.com/watch?v=s_o8dwzRlu4&list=PLXUDioG7XwE59TfSXWN-nDWiTlT5RwrZL&index=56&t=882s>
- Kubernetes crash loop backoff with some nice utilities for logs etc - <https://sysdig.com/blog/debug-kubernetes-crashloopbackoff/>
- Remote Debug kubernetes pod with Intellij or VSCode - <https://refactorfirst.com/how-to-remote-debug-java-application-on-kubernetes>

## Kubernetes Tools

- <https://k9scli.io/> home with cheatsheets instructions etc. 
  - Installing - https://github.com/derailed/k9s#installation
    - On Ubuntu can install easily via webinstall (see page above for details)
- VSCode extension - <https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools>
- Lens - discounted due to licensing and shenanigans around the open source version currently -> to be rechecked at some point
- Validation tools
  - Basic yaml linter - <https://yamllint.readthedocs.io/en/stable/>
  - Kube and helm chart linter - <https://docs.kubelinter.io/#/>
  - Detect old dependencies - <https://github.com/FairwindsOps/pluto>

## Kubernetes Notes

### Kubernetes Overview

- Container Orchestration tool
- Google originally developed it
- basic tutorial <https://kubernetes.io/docs/tutorials/kubernetes-basics/>
- <https://kubernetes.io/docs/concepts/overview/components/>

### Components

- Deployment -> Replica Set -> Pod
  - Favour Deployment over directly using a replica set since you can give declarative updates to your pods
    - <https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>
    - Deployment `describes` a desired state (in the yaml spec: section) and the Deployment Controller changes actual state to reflect desired state.
    - Replica Set aims to maintain a stable set of replica Pods running at any given time <https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>.

## Kubernetes commands

- Kubernetes Cheatsheet - <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

```bash
# kubectl but my alias is "k"

# Listing stuff
kubectl get pods --all-namespaces            # list pods in all namespaces not just the current one
k get pods -n kubernetes-system              # List pods in a given namespace
kubectl get pods -o wide                     # Get a lot more details
kubectl get pods -w                          # Watch (useful waiting for stuff to get running)

# all running services - get the ports!
kubectl get service --all-namespaces

# all images inside the K3S cluster (but again Lens will probably be better for it)
docker exec k3d-k3s-default-server-0 sh -c "ctr image list"
```

### Getting a shell to a running container

- <https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/>

```bash

# Basic form
kubectl exec --stdin --tty shell-demo -- /bin/bash
```

## Inter pod communication

- <https://www.tutorialworks.com/kubernetes-pod-communication/>
  - THis is part of the learning list so I'll add notes here once done
- <https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/>
