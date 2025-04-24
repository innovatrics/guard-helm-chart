# Installation

This is guide is about how to create infrastructure for guard application from scratch.
(Currently a lot of part is missing, and We will add them when needed)

## Creation of Firebase

1. When you run terraform you also created firebase application and some of firebase configuration was stored in kubernetes secret `firebase-secret-terraform`. However in time we were doing this infrastrucute as a code, somethings were not possible to automate. Becouse of that you need do this steps manually.
2. Log to your firebase account and go to your firebase project. Then navigate in left menu to project settings. (Settings icon next to Project Overview).
3. In the project settings navigate to Cloud Messaging section. At bottom on the screen is section Web configuration. Click on Generate key pair. Private and public key was genareted.
4. Copy the public key value and use it in values when installing helm. Under section:
```bash
    firebase:
        vapidPublicKey: <Vapid public key placeholder>
```
5. Then navigate to Project settings/Service Accounts
6. Firebase Admin SDK should be selected. Click on the Generate new private key and download json with values.
7. Supply your helm values with values from json file you downloaded.
```bash
    firebase:
        vapidPublicKey: <value placeholder>
        projectId: <value placeholder>
        privateKeyId: <value placeholder>
        clientEmail: <value placeholder>
        clientId: <value placeholder>
        authUri: <value placeholder>
        tokenUri: <value placeholder>
        authProviderx509CertUrl: <value placeholder>
        clientx509CertUrl: <value placeholder>
        universe_domain: <value placeholder>
```
8. When installing helm chart add those helm values

## For innovatrics dev section

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
helm upgrade --install guard . --namespace guard -f values.yaml -f guard.values.yaml
```
