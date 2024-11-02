# MySQL Kubernetes Deployment

This repository contains the necessary Kubernetes manifests to deploy a MySQL server on a Kubernetes cluster.

## Files Description

- **config-map.yml**: Defines the ConfigMap for MySQL configuration.
- **deployment.yml**: Defines the Deployment for the MySQL server.
- **mysqld-custom.cnf**: Custom MySQL configuration file.
- **namespace.yml**: Defines the Namespace for the MySQL server.
- **persistent-volume-claim.yml**: Defines the PersistentVolumeClaim for MySQL storage.
- **persistent-volume.yml**: Defines the PersistentVolume for MySQL storage.
- **service.yml**: Defines the Service for MySQL to expose it outside the cluster.

## Deployment Instructions

1. **Create Namespace**:

    ```sh
    kubectl apply -f namespace.yml
    ```

2. **Create ConfigMap**:

    ```sh
    kubectl apply -f config-map.yml
    ```

3. **Create Persistent Volume and Claim**:

    ```sh
    kubectl apply -f persistent-volume.yml
    kubectl apply -f persistent-volume-claim.yml
    ```

4. **Deploy MySQL**:

    ```sh
    kubectl apply -f deployment.yml
    ```

5. **Create Service**:

    ```sh
    kubectl apply -f service.yml
    ```

## Accessing MySQL

Once the service is created, you can access the MySQL server using the `mysql-service` service name within the cluster or the external IP if using a LoadBalancer.

## Custom Configuration

The MySQL server is configured using the `mysqld-custom.cnf` file, which is mounted as a ConfigMap. You can modify the configuration in `mysql/config-map.yml` and reapply it to update the MySQL configuration.

## Notes

- Ensure that your Kubernetes cluster has a storage class named `standard` or modify the `storageClassName` in the PersistentVolume and PersistentVolumeClaim manifests.
- The MySQL root password is set to `admin` in the deployment manifest. Change it as needed.
