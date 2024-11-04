# Setting Up Rancher with Helm in K3s

This tutorial will guide you through the process of setting up Rancher using Helm in a K3s cluster.

## Prerequisites

- A running K3s cluster
- Helm installed on your local machine
- kubectl installed and configured to interact with your K3s cluster

## Step 0: Installing Helm

If you don't have Helm installed, you can install it by following these steps:

### On macOS

```sh
brew install helm
```

### On Windows

Download the latest Helm release from the [Helm releases page](https://github.com/helm/helm/releases) and follow the installation instructions.

### On Linux

Download the latest Helm release and install it:

```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

For more detailed instructions, refer to the [Helm installation guide](https://helm.sh/docs/intro/install/).

## Step 1: Add the Helm Repository

First, add the Rancher Helm repository:

```sh
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest
helm repo update
```

## Step 2: Create a Namespace for Rancher

Create a namespace for Rancher:

```sh
kubectl create namespace cattle-system
```

## Step 3: Install Cert-Manager

Rancher requires cert-manager to manage certificates:

```sh
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.16.1/cert-manager.yaml
```

## Step 4: Install Rancher

Install Rancher using Helm:

```sh
helm install rancher rancher-latest/rancher \
--namespace cattle-system \
--set hostname=<your-rancher-hostname>
```

Replace `<your-rancher-hostname>` with the DNS name you want to use for Rancher.

## Step 5: Verify the Installation

Check the status of the Rancher deployment:

```sh
kubectl -n cattle-system rollout status deploy/rancher
```

## Step 6: Access Rancher

Once the deployment is complete, you can access Rancher by navigating to the hostname you specified in your web browser.

## Conclusion

You have successfully set up Rancher using Helm in your K3s cluster. You can now start managing your Kubernetes clusters with Rancher.

For more information, refer to the [Rancher documentation](https://rancher.com/docs/rancher/v2.5/en/installation/).
