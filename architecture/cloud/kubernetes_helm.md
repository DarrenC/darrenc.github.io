# Kubernetes and Helm (and other stuff)

- [Kubernetes and Helm (and other stuff)](#kubernetes-and-helm-and-other-stuff)
  - [Kubernetes Articles](#kubernetes-articles)
  - [Kubernetes Notes](#kubernetes-notes)
    - [Kubernetes Overview](#kubernetes-overview)
  - [Kubernetes commands](#kubernetes-commands)

## Kubernetes Articles

- <https://medium.com/google-cloud/kubernetes-101-pods-nodes-containers-and-clusters-c1509e409e16>
- <https://kubernetes.io/docs/concepts/workloads/pods/>

- Kuberenetes with Nana <https://www.youtube.com/watch?v=s_o8dwzRlu4&list=PLXUDioG7XwE59TfSXWN-nDWiTlT5RwrZL&index=56&t=882s>
- Kubernetes crash loop backoff with some nice utilities for logs etc - <https://sysdig.com/blog/debug-kubernetes-crashloopbackoff/>

## Kubernetes Notes

### Kubernetes Overview

- Container Orchestration tool
- Google originally developed it
- basic tutorial <https://kubernetes.io/docs/tutorials/kubernetes-basics/>

## Kubernetes commands

- Kubernetes Cheatsheet - <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

```bash
# kubectl but my alias is "k"

# Listing stuff
kubectl get pods --all-namespaces
kubectl get pods -o wide                     # Get a lot more details
kubectl get pods -w                          # Watch (useful waiting for stuff to get running)

# all running services - get the ports!
kubectl get service --all-namespaces

# all images inside the K3S cluster (but again Lens will probably be better for it)
docker exec k3d-k3s-default-server-0 sh -c "ctr image list"
```