# Goal
Quick way to create a new k8s cluster and deploy confluent cluster on it.

### General Pre-Req
- You have installed:
  - kubectl
  - helm

## EKS
Amazon EKS (Elastic Kubernetes Service) is the managed kubernetes cluster provided by aws.

### Pre-Req
- You have installed:
  - [eksctl](https://eksctl.io/introduction/#installation)
- You have exported your AWS credentials in the terminal.

### EKS management

#### Creation
Before running it, customize eksctl-basic-cluster.yaml
  
    eksctl create cluster --config-file eksctl-basic-cluster.yaml --verbose 4

#### Set kube config

    eksctl utils write-kubeconfig -f eksctl-basic-cluster.yaml

#### Deletion
 
    eksctl delete cluster -f eksctl-basic-cluster.yaml --verbose 4

##### Note

If you see this message:

    recoverable pod eviction failure: "Cannot evict pod as it would violate the pod's disruption budget."

Delete the pod's with disruption budget. To do so, find the pods configured with disruption budget:

    kubectl get poddisruptionbudget -A

Then delete them :

    kubectl delete poddisruptionbudget {name} -n {namespace}

#### Checks

*Objects created in AWS*

- Go to [Tag Editor](https://eu-central-1.console.aws.amazon.com/resource-groups/tag-editor/find-resources?region=eu-central-1)
- Check you are selecting all regions
- Check for any tag that you added to your cluster.

## Kind

According to their [page](https://kind.sigs.k8s.io/)

    kind is a tool for running local Kubernetes clusters using Docker container “nodes”. kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI

### Pre-Req
- You have installed:
  - [kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

### Kind management

#### Creation
Before running it, customize kind-basic-cluster.yaml
  
    kind create cluster --config kind-basic-cluster.yaml

#### Set kube config

    kubectl config use-context kind-kind

#### Deletion
 
    kind delete cluster

## Confluent for Kubernetes Quickstart

### K8s cluster available

    kubectl get pods -A -o wide

### Instructions
Follow instructions on [Confluent for Kubernetes Quickstart](https://docs.confluent.io/operator/current/co-quickstart.html)