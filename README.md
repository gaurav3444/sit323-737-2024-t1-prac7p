# Cloud Native Application Development 9.1P: Adding a Database to Your Application

This guide outlines the steps to add a MongoDB database to your Kubernetes cluster.


## Steps

1. **Create Storage Class:**

    A StorageClass in Kubernetes is used to define different types of storage available in your cluster. This step involves creating a StorageClass to provision storage for MongoDB.

    ```bash
    kubectl apply -f createStorageClass.yaml
    ```

2. **Deploy Persistent Volume:**

    PVs in Kubernetes are storage resources provisioned by an administrator. This step deploys a PersistentVolume, which is a piece of storage in the cluster that has been provisioned by an administrator.

    ```bash
    kubectl apply -f createPersistentVolume.yaml
    ```

3. **Deploy Persistent Volume Claim:**

    PersistentVolumeClaims (PVCs) are requests for storage by a user. This step deploys a PersistentVolumeClaim, which is a request for storage by a user. PVCs consume PV resources and are used by pods.

    ```bash
    kubectl apply -f createPersistentVolumeClaim.yaml
    ```

4. **Install MongoDB:**

    This step involves deploying MongoDB onto the Kubernetes cluster. You can either set it up as a standalone instance or as a replica set, depending on your requirements. The YAML file (createDeployment.yaml) should contain the necessary configurations for MongoDB deployment.

    ```bash
    kubectl apply -f createDeployment.yaml
    ```

5. **Deploy Service:**

    Services in Kubernetes provide a way to expose your application to external traffic or other applications within the cluster. This step deploys a Service for MongoDB to allow other parts of your application to communicate with the database.

    ```bash
    kubectl apply -f createService.yaml
    ```

6. **Check the Database:**

   After deploying MongoDB, it's crucial to ensure its proper functionality. A common method to verify this is by accessing the MongoDB instance through tools such as MongoDB Compass. 
   The login credentials (username and password) specified in the deployment file, along with the designated port (32000) outlined in the service file, should be utilized for authentication and connection. 
   This process allows us to confirm the database's operational status and ensure it's ready for use by your application.

7. **Deploy Configuration and Secrets:**

   Configuration files and secrets are essential for managing the settings and sensitive information needed by your application. This step involves deploying a ConfigMap and a Secret to provide configuration settings and credentials for MongoDB.

    ```bash
    kubectl apply -f createConfigMap.yaml
    ```
    
    ```bash
    kubectl apply -f createMongoDbSecret.yaml
    ```

8. **Deploy StatefulSet (Optional):**

    A StatefulSet in Kubernetes is used for managing stateful applications, like databases. This step involves deploying a StatefulSet for MongoDB, which defines a replica set with multiple pods running MongoDB instances. This ensures high availability and data redundancy.

    ```bash
    kubectl apply -f createStatefulSet.yaml
    ```

9. **Deploy Headless Service (Optional):**

    A headless Service in Kubernetes is used when you don't need load balancing or a single stable IP. This step is optional and involves deploying a headless Service for MongoDB if needed.

    ```bash
    kubectl apply -f createHeadlessService.yaml
    ```

10. **Verification:**

    After deploying all the components, it's crucial to verify that everything is working as expected. Check the status of pods using kubectl get pods. All replicas of MongoDB should be running without any issues. This ensures that your MongoDB deployment is successful and ready to be used by your application.

    ```bash
    kubectl get pods
    ```

    Ensure all MongoDB replicas are running without issues.

## Conclusion

Following these steps, you should have a MongoDB database deployed and ready to be used by your application within your Kubernetes cluster.

Feel free to modify configurations and YAML files as per your requirements.

