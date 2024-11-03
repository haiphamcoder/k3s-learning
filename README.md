# k3s-learning

## Installing k3s on Local Machine

k3s is a lightweight Kubernetes distribution by Rancher. Follow these steps to install k3s on your local machine.

### Prerequisites

- A machine with a supported operating system (Linux, macOS, or Windows with WSL2).
- `curl` installed on your machine.

### Installation Steps

1. **Install k3s**:

    Run the following command to install k3s:

    ```sh
    curl -sfL https://get.k3s.io | sh -
    ```

2. **Verify Installation**:

    Check the status of k3s to ensure it is running:

    ```sh
    sudo systemctl status k3s
    ```

3. **Configure kubectl**:

    By default, k3s installs `kubectl` and sets up the configuration file. You can verify the configuration by running:

    ```sh
    kubectl get nodes
    ```

    This should list your local machine as a node in the k3s cluster.

4. **Accessing the Cluster**:

    The `kubeconfig` file for k3s is located at `/etc/rancher/k3s/k3s.yaml`. You can use this file to configure `kubectl`:

    ```sh
    export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
    ```

5. **Uninstalling k3s**:

    If you need to uninstall k3s, run the following command:

    ```sh
    /usr/local/bin/k3s-uninstall.sh
    ```

### Additional Resources

- [k3s Documentation](https://rancher.com/docs/k3s/latest/en/)
- [k3s GitHub Repository](https://github.com/k3s-io/k3s)

By following these steps, you should have a working k3s installation on your local machine. You can now start deploying applications and learning Kubernetes with k3s.
