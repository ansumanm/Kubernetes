To cover about 80% of the most common tasks in Kubernetes using `kubectl`, you'll want to familiarize yourself with a set of essential commands. Here's a list that should cover most of your needs:

1. **Get Resources:**
   - `kubectl get pods` - List all pods in the current namespace.
   - `kubectl get services` - List all services in the current namespace.
   - `kubectl get deployments` - List all deployments in the current namespace.
   - `kubectl get nodes` - List all nodes in the cluster.

2. **Describe Resources:**
   - `kubectl describe pod [pod-name]` - Show detailed information about a specific pod.
   - `kubectl describe service [service-name]` - Show detailed information about a specific service.
   - `kubectl describe deployment [deployment-name]` - Show detailed information about a specific deployment.

3. **Create and Apply Resources:**
   - `kubectl create -f [file.yaml]` - Create a resource from a YAML file.
   - `kubectl apply -f [file.yaml]` - Apply changes to a resource from a YAML file.

4. **Delete Resources:**
   - `kubectl delete pod [pod-name]` - Delete a specific pod.
   - `kubectl delete -f [file.yaml]` - Delete resources defined in a YAML file.

5. **Debugging and Diagnostics:**
   - `kubectl logs [pod-name]` - Print the logs from a container in a pod.
   - `kubectl exec -it [pod-name] -- /bin/bash` - Execute an interactive bash shell on a specific pod.

6. **Manage Configurations:**
   - `kubectl config view` - Display merged kubeconfig settings.
   - `kubectl config current-context` - Display the current-context.

7. **Scaling and Updating Applications:**
   - `kubectl scale deployment [deployment-name] --replicas=[n]` - Scale a deployment to n replicas.
   - `kubectl rollout status deployment/[deployment-name]` - Watch the status of the latest rollout until it's done.
   - `kubectl rollout undo deployment/[deployment-name]` - Rollback to the previous deployment.

8. **Namespace Management:**
   - `kubectl get namespaces` - List all namespaces.
   - `kubectl create namespace [namespace-name]` - Create a new namespace.

9. **Resource Inspection and Cluster Monitoring:**
   - `kubectl top pod` - Show metrics for pods.
   - `kubectl cluster-info` - Display cluster info.

These commands are a solid foundation for most of the tasks you'll encounter when managing Kubernetes resources. Remember, Kubernetes is vast, and there are many more specific commands and flags, but knowing these should cover a significant portion of your daily tasks.
