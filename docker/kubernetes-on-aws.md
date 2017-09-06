# Kubernetes on AWS



[Kops](https://github.com/kubernetes/kops) is a great tool to get production grade Kubernetes cluster up and running. AWS is currently officially supported, with GCE and VMware vSphere in alpha and other platforms planned.

Kops tutorial for setting up Kubernetes cluster on AWS can be found [here](https://github.com/kubernetes/kops/blob/master/docs/aws.md).

To set `kubectl` context to an existing Kubernetes cluster:

```bash
> kops export kubecfg cluster-name.example.com
Kops has set your kubectl context to cluster-name.example.com
```



Other random AWS tips:

- Use awscli to list buckets: `aws s3api list-buckets`
- Run `aws` commands without specify the profile: `export AWS_PROFILE=<profile user>`

