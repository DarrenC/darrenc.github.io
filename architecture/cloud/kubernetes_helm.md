# Kubernetes and Helm (and other stuff)

- [Kubernetes and Helm (and other stuff)](#kubernetes-and-helm-and-other-stuff)
  - [Kubernetes Articles](#kubernetes-articles)
  - [Kubernetes Tools - Basic list](#kubernetes-tools---basic-list)
    - [Kubectl and Kustomize](#kubectl-and-kustomize)
    - [Microcks - testing with Kubernetes](#microcks---testing-with-kubernetes)
  - [Kubernetes Notes](#kubernetes-notes)
    - [Kubernetes Overview](#kubernetes-overview)
    - [Components](#components)
  - [Kubernetes commands](#kubernetes-commands)
    - [Admin stuff](#admin-stuff)
    - [Getting a shell to a running container](#getting-a-shell-to-a-running-container)
  - [Inter pod communication](#inter-pod-communication)
    - [K9s Useful Commands](#k9s-useful-commands)
      - [K9s Commands cheatsheet](#k9s-commands-cheatsheet)
  - [Simple yaml for a pod](#simple-yaml-for-a-pod)
  - [Helm](#helm)
    - [Configmaps in helm](#configmaps-in-helm)
  - [Definitions](#definitions)
  - [Basic Kuberenetes Tutorial](#basic-kuberenetes-tutorial)

## Kubernetes Articles

- <https://medium.com/google-cloud/kubernetes-101-pods-nodes-containers-and-clusters-c1509e409e16>

- Kuberenetes with Nana <https://www.youtube.com/watch?v=s_o8dwzRlu4&list=PLXUDioG7XwE59TfSXWN-nDWiTlT5RwrZL&index=56&t=882s>
- Kubernetes crash loop backoff with some nice utilities for logs etc - <https://sysdig.com/blog/debug-kubernetes-crashloopbackoff/>
- Remote Debug kubernetes pod with Intellij or VSCode - <https://refactorfirst.com/how-to-remote-debug-java-application-on-kubernetes>
  - Also see the quarkus remote Dev stuff on quarkus page - [java-quarkus](../../development/java/java-quarkus.md) 

## Kubernetes Tools - Basic list

- <https://k9scli.io/> home with cheatsheets instructions etc. 
  - Installing - https://github.com/derailed/k9s#installation
    - On Ubuntu can install easily via webinstall (see page above for details)
- VSCode extension - <https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools>
- Lens - discounted due to licensing and shenanigans around the open source version currently -> to be rechecked at some point
- Validation tools
  - Basic yaml linter - <https://yamllint.readthedocs.io/en/stable/>
  - Kube and helm chart linter - <https://docs.kubelinter.io/#/>
  - Detect old dependencies - <https://github.com/FairwindsOps/pluto>
- Diagrams - <https://github.com/mingrammer/diagrams>
  - Python based tool to generate diagrams from code
  - Can generate kubernetes diagrams really easily
- <https://k8studio.io/> - K8s studio - todo - check this out
  - NB Licence free for personal use but paid for PRO

### Kubectl and Kustomize

- Kustomize - Way of customizing kubernetes config files without templates - <https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/>
- Kubectl - command line of kubernetes - <https://kubectl.docs.kubernetes.io/guides/introduction/kubectl/>

### Microcks - testing with Kubernetes

- <https://www.linkedin.com/pulse/how-microcks-fit-unify-inner-outer-loops-cloud-native-kheddache/>
- 

## Kubernetes Notes

### Kubernetes Overview

- Container Orchestration tool
- Google originally developed it
- basic tutorial <https://kubernetes.io/docs/tutorials/kubernetes-basics/>
- <https://kubernetes.io/docs/concepts/overview/components/>

### Components

- Pods - <https://kubernetes.io/docs/concepts/workloads/pods/>
  - Managing workloads - https://kubernetes.io/docs/concepts/workloads/management/
- Deployment -> Replica Set -> Pod
  - Favour Deployment over directly using a replica set since you can give declarative updates to your pods
    - <https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>
    - Deployment `describes` a desired state (in the yaml spec: section) and the Deployment Controller changes actual state to reflect desired state.
    - Replica Set aims to maintain a stable set of replica Pods running at any given time <https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>.
  - Restarting Pods 
    - listing of a few methods
      - <https://spacelift.io/blog/restart-kubernetes-pods-with-kubectl>
- Operator Pattern - https://kubernetes.io/docs/concepts/extend-kubernetes/operator/
  - https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-operator
  - https://www.cncf.io/blog/2022/06/15/kubernetes-operators-what-are-they-some-examples/
- Custom Resources - https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/

## Kubernetes commands

- Kubernetes Cheatsheet - <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

```bash
# kubectl but my alias is "k"

# Listing stuff
kubectl get pods --all-namespaces            # list pods in all namespaces not just the current one
k get pods -n kubernetes-system              # List pods in a given namespace
kubectl get pods -o wide                     # Get a lot more details
kubectl get pods -w                          # Watch (useful waiting for stuff to get running)
kubectl get pods -l some-label                # List pods with a given label
kubectl get pods -l some-label --show-labels  # Show the labels

# Adding a label
kubectl label pod <somepodname> <somelabel>=true

# all running services - get the ports!
kubectl get service --all-namespaces

# all images inside the K3S cluster (but again Lens will probably be better for it)
docker exec k3d-k3s-default-server-0 sh -c "ctr image list"
```

### Admin stuff

```bash
# Create a namespace
kubectl create namespace <namespace_name>

# Creating a rolebinding for a service account
kubectl create rolebinding -n "<somens>" edit --clusterrole=edit --serviceaccount="<somens>":<someaccount>

# Running a command as a service account or some other user to see if it is possible
kubectl --as=system:serviceaccount:"$NS":$SA auth can-i use

# kube-apiserver command
kubectl exec -it -n kube-system kube-apiserver-kind-control-plane -- kube-apiserver -h
```

- Debug - run as another user - <https://kubernetes.io/docs/reference/access-authn-authz/authentication/#user-impersonation>

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
- <https://dev.to/narasimha1997/communication-between-microservices-in-a-kubernetes-cluster-1n41>

### K9s Useful Commands

- <https://k9scli.io/topics/commands/> list of commands
- <https://blog.palark.com/k9s-the-powerful-terminal-ui-for-kubernetes/> nice tutorial with plenty of examples

#### K9s Commands cheatsheet

- The ":" is used as a command prefix and then can be followed by a command
  - :pods - see pods
  - :svc - see services
  - :deploy - see deployments
  - :sts - see stateful sets
  - :rs - see replica sets
  - :ns - see namespaces
  - :no - see nodes
  - :sec - see secrets
  - :cm - config maps
- :xray -> different views of the cluster with a tree layout

## Simple yaml for a pod

- From this page <https://downey.io/notes/dev/ubuntu-sleep-pod-yaml/>
- Pod sleeps for a week
  - Save to a file called ubuntu.yaml
  - create with - ```kubectl apply -f ubuntu.yaml```
  - connect with - ```kubectl exec -it ubuntu -- /bin/bash```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
  labels:
    app: ubuntu
spec:
  containers:
  - image: ubuntu
    command:
      - "sleep"
      - "604800"
    imagePullPolicy: IfNotPresent
    name: ubuntu
  restartPolicy: Always
```

## Helm

- Customizing the configmap name generated - [ChatGPT question - "research helm, when installing a helm chart which creates a configmap, the configmap is always named with the namespace and release name but I want only the release name"](https://chatgpt.com/c/26d6868f-8625-4414-bd34-b9d2203697c1?oai-dm=1)

### Configmaps in helm

- https://stackoverflow.com/questions/69837364/helm-configmap-in-values-yaml


## Definitions

- https://redhat-scholars.github.io/kubernetes-tutorial/kubernetes-tutorial/secrets.html
- https://stackoverflow.com/questions/61171487/what-is-the-difference-between-namespaces-and-contexts-in-kubernetes
- https://stackoverflow.com/questions/55373686/how-to-switch-namespace-in-kubernetes
- https://semaphoreci.com/blog/replicaset-statefulset-daemonset-deployments

## Basic Kuberenetes Tutorial
(SEE Also DC local files and obsidian for notes)
- <https://redhat-scholars.github.io/kubernetes-tutorial/kubernetes-tutorial/index.html>
- https://github.com/redhat-scholars/kubernetes-tutorial