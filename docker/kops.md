# Kops

> Kops is a command line tool that helps create, destroy, upgrade and maintain Kubernetes cluster on AWS and other platform.

The tutorial for deploying Kubernetes on AWS with kops can be found [here](https://github.com/kubernetes/kops/blob/master/docs/aws.md).

### prerequisite for deploying Kubernetes to AWS

- setup AWS account and environment, aws CLI tools
- configure DNS

### Creating Kubernetes cluster

```bash
export NAME=myfirstcluster.example.com
export KOPS_STATE_STORE=s3://prefix-example-com-state-store

# create cluster config
kops create cluster \
    --zones us-west-2a \
    ${NAME}

# customize cluster config
kops edit cluster ${NAME}

# build the cluster
kops update cluster ${NAME} --yes
```
