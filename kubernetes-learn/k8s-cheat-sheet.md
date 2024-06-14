# kubernetes cheat sheet 
```
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

🚀 Kubernetes Commands Cheat Sheet 🚀
Are you working with Kubernetes and need quick access to commonly used commands? Look no further! Here's a cheat sheet of essential Kubernetes commands to help you navigate the container orchestration world like a pro:
Here are some common Kubernetes commands:

1.kubectl get: Retrieve information about resources in the cluster.
kubectl get pods: List all pods.
kubectl get deployments: List all deployments.
kubectl get services: List all services.
kubectl get nodes: List all nodes in the cluster.

2.kubectl describe: Provide detailed information about a specific resource.
kubectl describe pod <pod-name>: Get detailed information about a pod.
kubectl describe deployment <deployment-name>: Get detailed information about a deployment.
kubectl describe service <service-name>: Get detailed information about a service.

3.kubectl create: Create a resource from a YAML or JSON file.
kubectl create -f <filename.yaml>: Create a resource from a YAML file.
kubectl create deployment <deployment-name> --image=<image-name>: Create a deployment using a specified image.

4.kubectl delete: Delete a resource.
kubectl delete pod <pod-name>: Delete a pod.
kubectl delete deployment <deployment-name>: Delete a deployment.
kubectl delete service <service-name>: Delete a service.

5.kubectl scale: Scale the number of replicas in a deployment.
kubectl scale deployment <deployment-name> --replicas=<number>: Scale the number of replicas for a deployment.

6.kubectl logs: Print the logs of a pod.
kubectl logs <pod-name>: Print the logs of a pod.

7.kubectl exec: Execute a command on a pod.
kubectl exec -it <pod-name> -- <command>: Execute a command on a pod interactively.

8.kubectl apply: Apply changes to a resource defined in a YAML or JSON file.
kubectl apply -f <filename.yaml>: Apply changes to a resource using a YAML file.
```
K8s 
```
Kubectl is a command-line tool used to interact with Kubernetes clusters. It allows you to deploy and manage applications, inspect and modify cluster resources, and perform various administrative tasks. Here are some basic kubectl commands:

    kubectl get: Retrieve information about resources in the cluster.
        kubectl get pods: List all pods in the cluster.
        kubectl get deployments: List all deployments in the cluster.
        kubectl get services: List all services in the cluster.
        kubectl get nodes: List all nodes in the cluster.

    kubectl describe: Get detailed information about a specific resource.
        kubectl describe pod <pod-name>: Show detailed information about a specific pod.
        kubectl describe deployment <deployment-name>: Show detailed information about a specific deployment.
        kubectl describe service <service-name>: Show detailed information about a specific service.

    kubectl create: Create a resource from a file or inline definition.
        kubectl create -f <file.yaml>: Create a resource defined in a YAML file.
        kubectl create deployment <deployment-name> --image=<image-name>: Create a deployment from a specified container image.

    kubectl delete: Delete a resource.
        kubectl delete pod <pod-name>: Delete a specific pod.
        kubectl delete deployment <deployment-name>: Delete a specific deployment.
        kubectl delete service <service-name>: Delete a specific service.

    kubectl apply: Apply changes to a resource.
        kubectl apply -f <file.yaml>: Apply changes to a resource defined in a YAML file.
        kubectl apply -f <dir>: Apply changes to all resources defined in a directory.

    kubectl logs: View the logs of a pod.
        kubectl logs <pod-name>: Print the logs of a specific pod.

    kubectl exec: Execute a command inside a container of a pod.
        kubectl exec -it <pod-name> -- <command>: Run an interactive shell in a specific pod.

    kubectl port-forward: Forward local ports to a pod.
        kubectl port-forward <pod-name> <local-port>:<pod-port>: Forward a local port to a specific pod.

These are just a few examples of the most commonly used kubectl commands. There are many more commands available, and you can explore additional options and parameters in the Kubernetes documentation or by using kubectl --help.
```
