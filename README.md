# amazon-eks-gpu-ami

## Requirements
- AWS CLI
- [Packer](https://developer.hashicorp.com/packer/downloads)

## Usage
1. Edit amazon-eks-gpu-ami. The following two need editing according to the EKS version:
```
      "source_ami_filter": {
        "filters": {
          "name": "amazon-eks-node-1.25-v*"
        },
```

```
      "ami_name": "amazon-eks-gpu-node-1.25-{{timestamp}}",
```

2. Build.
```
$ packer build amazon-eks-gpu-ami.json
```

3. Specify the cluster name in userdata and bootstrap at node startup.
```
#!/usr/bin/env bash

/etc/eks/bootstrap.sh {ClusterName} --container-runtime containerd
```
