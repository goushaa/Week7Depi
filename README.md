# Kubernetes Blog Application Deployment

This project demonstrates the deployment of a simple blog application on a Kubernetes cluster using Minikube. The application consists of a frontend served by Nginx and a backend using MySQL, with features such as autoscaling and persistent storage.

## Project Overview

The deployment includes the following components:
- **Namespace**: All resources are organized within a dedicated namespace.
- **MySQL Backend**: Includes configuration, persistent storage, secrets management, and service exposure.
- **Nginx Frontend**: Manages the deployment of static content, service exposure, and external access through Ingress.
- **Autoscaling**: The frontend deployment is configured to automatically scale based on CPU utilization.

## Project Files

### 1. `blog-namespace.yaml`
Defines a Kubernetes namespace for the blog application, ensuring isolation and organization of resources.

### 2. `mysql-config.yaml`
Stores configuration data for the MySQL database, including database name and user credentials.

### 3. `mysql-pvc.yaml`
Requests persistent storage for the MySQL database, ensuring data retention across pod restarts.

### 4. `mysql-secret.yaml`
Secures sensitive information, such as the MySQL root password, using Kubernetes Secrets.

### 5. `mysql-service.yaml`
Exposes the MySQL database internally within the Kubernetes cluster via a ClusterIP service.

### 6. `mysql.yaml`
Describes the StatefulSet for deploying MySQL, ensuring stable network identities and persistent storage.

### 7. `frontend-config.yaml`
Contains configurations or static content for the Nginx frontend, managed via a ConfigMap.

### 8. `frontend-hpa.yaml`
Implements a Horizontal Pod Autoscaler (HPA) for the frontend deployment, scaling the number of replicas based on CPU utilization.

### 9. `frontend-ingress.yaml`
Configures an Ingress resource to expose the frontend service externally, routing traffic to the application.

### 10. `frontend-service.yaml`
Exposes the frontend deployment internally within the Kubernetes cluster via a ClusterIP service.

### 11. `frontend.yaml`
Describes the deployment of the Nginx frontend, including replica management and volume mounts for serving static content.

## Deployment Steps

1. **Start Minikube**:
   Initialize Minikube to create a local Kubernetes cluster.

2. **Enable Addons**:
   Enable the Ingress controller and Metrics Server within Minikube to support external routing and autoscaling.

3. **Create Namespace**:
   Apply the namespace configuration to organize all resources under the `blog` namespace.

4. **Deploy MySQL Backend**:
   Deploy the MySQL StatefulSet, along with its associated storage, configuration, and secrets.

5. **Deploy Nginx Frontend**:
   Deploy the frontend application, configure autoscaling, and expose it externally using Ingress.

6. **Configure Local Access**:
   Map a local domain to the Minikube IP in your `/etc/hosts` file to access the application through a browser.

## Managing the Application

- **Monitor HPA**: Check the status of the Horizontal Pod Autoscaler to ensure the frontend scales as expected.
- **Access Logs**: Use `kubectl` commands to view logs from the pods for troubleshooting and monitoring.
- **Scale Manually**: If needed, adjust the number of replicas for the frontend deployment manually.

## Cleanup

To delete all resources and clean up the cluster, delete the namespace:

```bash
kubectl delete namespace blog
```

## Notes
- Ensure that your /etc/hosts file is properly configured for local access in Minikube.
- This setup is tailored for local development and testing using Minikube. Adjust configurations as necessary for production environments.