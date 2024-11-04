# Setting Up MySQL Server on K3s

This tutorial will guide you through the steps to set up a MySQL server on a K3s cluster using a YAML configuration file.

## Prerequisites

- A running K3s cluster
- `kubectl` installed and configured to interact with your K3s cluster
- A YAML configuration file for MySQL server (`mysql-server.yml`)

## Steps

1. **Create the MySQL Server YAML Configuration**

    Create a file named `mysql-server.yml` with the following content:

    ```yaml
    apiVersion: v1
    kind: Namespace

    metadata:
      name: mysql-server

    ---

    apiVersion: v1
    kind: PersistentVolumeClaim

    metadata:
      name: mysql-pvc
      namespace: mysql-server

    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
    ---

    apiVersion: apps/v1
    kind: Deployment

    metadata:
      name: mysql
      namespace: mysql-server

    spec:
      selector:
        matchLabels:
          app: mysql
      strategy:
        type: Recreate
      template:
        metadata:
          labels:
            app: mysql
        spec:
          containers:
          - image: mysql:8.0
            name: mysql
            env:
            - name: MYSQL_ROOT_PASSWORD
              value: "admin"
            ports:
            - containerPort: 3306
              name: mysql
            volumeMounts:
            - name: mysql-persistent-storage
              mountPath: /var/lib/mysql
          volumes:
          - name: mysql-persistent-storage
            persistentVolumeClaim:
              claimName: mysql-pvc
    ---

    apiVersion: v1
    kind: Service

    metadata:
      name: mysql-service
      namespace: mysql-server

    spec:
      ports:
      - port: 3306
        targetPort: 3306
      selector:
        app: mysql
      type: ClusterIP

    ```

2. **Apply the Configuration**

    Use `kubectl` to apply the configuration file to your K3s cluster:

    ```sh
    kubectl apply -f ./mysql-server.yml
    ```

3. **Verify the Deployment**

    Check the status of the MySQL deployment:

    ```sh
    kubectl get pods
    ```

4. **Access the MySQL Server**

    You can now connect to the MySQL server using a MySQL client on your local machine:

    ```sh
    mysql -h <Cluster-IP> -P 3306 -u root -p
    ```

    Enter the MySQL root password (`admin` as specified in the YAML configuration) when prompted.

## Conclusion

You have successfully set up a MySQL server on your K3s cluster using a YAML configuration file. You can now use this MySQL server for your applications running on the K3s cluster.