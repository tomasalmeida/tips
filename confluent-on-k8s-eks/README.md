# Goal
Quick way to create a new EKS cluster on AWS and deploy confluent cluster on it.

## Pre-Req
- You have installed:
  - [eksctl](https://eksctl.io/introduction/#installation)
  - kubectl
  - helm
- You have exported your AWS credentials in the terminal.

## EKS management

### Creation
Before running it, customize 00-basic-cluster.yaml
  
    eksctl create cluster --config-file 00-basic-cluster.yaml --verbose 4

### Deletion
 
    eksctl delete cluster -f 00-basic-cluster.yaml --verbose 4

#### Note

If you see this message:

    recoverable pod eviction failure: "Cannot evict pod as it would violate the pod's disruption budget."

Delete the pod's with disruption budget. To do so, find the pods configured with disruption budget:

    kubectl get poddisruptionbudget -A

Then delete them :

    kubectl delete poddisruptionbudget {name} -n {namespace}

### Checks

#### Objects created in AWS

- Go to [Tag Editor](https://eu-central-1.console.aws.amazon.com/resource-groups/tag-editor/find-resources?region=eu-central-1)
- Check you are selecting all regions
- Check for any tag that you added to your cluster.

#### K8s cluster available

    kubectl get pods -A -o wide


## Confluent for Kubernetes Quickstart

Follow instructions on [Confluent for Kubernetes Quickstart](https://docs.confluent.io/operator/current/co-quickstart.html)