# Basic Commands

### Notes on Kubernetes (K8s) Orchestration Platform

#### Overview

* **Kubernetes (K8s)**: An orchestration platform designed to integrate and extend the capabilities of other products like Docker.
* **Goal**: To provide a scalable, efficient, and flexible solution for managing containerized applications and services.

#### Key Features and Capabilities

1. **Horizontal Scaling**:
   * Adds more devices/machines to handle increased workload instead of adding more resources (CPU/RAM) to existing machines.
2. **Extensibility**:
   * Allows dynamic modification of clusters without affecting other containers outside the intended group.
3. **Self-Healing**:
   * Automatically restarts, replaces, reschedules, and kills containers based on user-defined health checks to maintain functionality.
4. **Automated Rollouts and Rollbacks**:
   * Gradually rolls out changes to containers, monitors application health during the process, and decides whether to continue the rollout or rollback changes to ensure constant uptime.

#### Basic Commands for Cluster Management

1. **Starting Clusters**:
   *   Ensure all clusters are started using:

       ```sql
       minikube start
       ```
2. **Checking Running Pods**:
   *   Command to list all running pods:

       ```arduino
       kubectl get pods
       ```
3. **Getting Deployment Name**:
   *   Command to list the deployment name:

       ```arduino
       kubectl get deployment
       ```
4. **Exposed Port of Service**:
   *   Command to find the port exposed by a service:

       ```arduino
       kubectl get services
       ```
5. **Checking Replica Sets**:
   *   Command to list all replica sets deployed in the cluster:

       ```arduino
       kubectl get rs
       ```
6. **Deleting a Deployment**:
   *   Command to delete a specific deployment:

       ```arduino
       kubectl delete deployment <deployment name>
       ```





***

## References

* [https://minikube.sigs.k8s.io/docs/tutorials/](https://minikube.sigs.k8s.io/docs/tutorials/)
* [https://kubernetes.io/docs/reference/kubectl/quick-reference/](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

