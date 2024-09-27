## Installation

# on your local machine, if you want use gui for observing kubernetes cluster

1. Install Open Lens. You can download it from [here](https://github.com/MuhammedKalkan/OpenLens).

2. Install Aws CLI version 2. You can download it from [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

# Inside dev container

3. Open Solution in dev container

4. Configure AWS CLI. If you haven't done this before, you can do it by running the following command and following the prompts:
```bash
aws configure
```

If you dont have credentials ask your aws admin.

5. Run this command
```bash
aws eks update-kubeconfig --region eu-central-1 --name sf-cluster-guard --role-arn your-arn-role --alias sf-cluster-guard
```

## How to use for fast proptotyping and changes

1. Ensure that you are using right cluster.

```bash
kubectx
kubectx nameOfCluster # to switch cluster
```

2. Go to guard folder. And run.

```bash
helm upgrade --install guard . --namespace guard
```