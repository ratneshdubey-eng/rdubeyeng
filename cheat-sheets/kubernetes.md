### Kubernetes Cheat Sheet

#### **Table of Contents**
1. [Management Commands](#management-commands)
2. [Pod Management Commands](#pod-management-commands)
3. [Service Management Commands](#service-management-commands)
4. [Deployment Management Commands](#deployment-management-commands)
5. [Namespace Commands](#namespace-commands)
6. [Node Management Commands](#node-management-commands)
7. [ConfigMap & Secret Commands](#configmap--secret-commands)
8. [Logging & Debugging](#logging--debugging)
9. [Other Useful Commands](#other-useful-commands)

---

### 1. **Management Commands**
| Command                                                       | Description                                     |
|---------------------------------------------------------------|-------------------------------------------------|
| `kubectl create <resource> <name>`                             | Create a resource (e.g., `pod`, `deployment`, `service`). |
| `kubectl apply -f <filename>`                                  | Apply a configuration file to create/update resources. |
| `kubectl delete <resource> <name>`                             | Delete a resource by name.                      |
| `kubectl delete -f <filename>`                                 | Delete resources defined in a file.             |
| `kubectl replace -f <filename>`                                | Replace an existing resource with the new definition. |
| `kubectl edit <resource> <name>`                               | Edit the configuration of a resource.           |
| `kubectl get <resource>`                                       | List one or more resources.                     |
| `kubectl get <resource> -o yaml/json`                          | Output resource information in YAML/JSON format. |
| `kubectl get <resource> -w`                                    | Watch a resource for changes.                   |
| `kubectl describe <resource> <name>`                           | Show detailed information about a resource.     |
| `kubectl get all`                                              | List all resources in the namespace.            |
| `kubectl delete all --all`                                     | Delete all resources in the namespace.          |

### 2. **Pod Management Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get pods`                                             | List all pods in the current namespace.           |
| `kubectl get pods -A`                                          | List all pods in all namespaces.                  |
| `kubectl delete pod <pod-name>`                                | Delete a pod by name.                             |
| `kubectl create -f <pod-definition.yml>`                       | Create a pod using a YAML definition.             |
| `kubectl exec <pod-name> -- <command>`                         | Run a command inside a specific pod.              |
| `kubectl exec -it <pod-name> -- /bin/bash`                     | Start a Bash session in a running pod.            |
| `kubectl logs <pod-name>`                                      | View logs for a specific pod.                     |
| `kubectl logs <pod-name> -c <container-name>`                  | View logs for a specific container in a pod.      |
| `kubectl port-forward <pod-name> <local-port>:<pod-port>`      | Forward one or more local ports to a pod.         |
| `kubectl cp <local-path> <pod-name>:<remote-path>`             | Copy files from local system to a pod.            |
| `kubectl get pod <pod-name> -o yaml`                           | Display a pod definition in YAML format.          |
| `kubectl top pod <pod-name>`                                   | Show resource (CPU/Memory) usage for a specific pod. |

### 3. **Service Management Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get svc`                                              | List all services in the current namespace.       |
| `kubectl describe svc <service-name>`                          | Show detailed information about a service.        |
| `kubectl expose pod <pod-name> --port=<port> --target-port=<target-port>` | Expose a pod as a service.                        |
| `kubectl delete svc <service-name>`                            | Delete a service by name.                         |
| `kubectl apply -f <service-definition.yml>`                    | Create/update a service from a YAML definition.   |

### 4. **Deployment Management Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get deployments`                                      | List all deployments in the current namespace.    |
| `kubectl describe deployment <deployment-name>`                | Show detailed information about a deployment.     |
| `kubectl rollout status deployment/<deployment-name>`          | Check the rollout status of a deployment.         |
| `kubectl scale deployment <deployment-name> --replicas=<num>`  | Scale a deployment to the desired number of replicas. |
| `kubectl set image deployment/<deployment-name> <container-name>=<new-image>` | Update the image of a container in a deployment. |
| `kubectl rollout undo deployment/<deployment-name>`            | Roll back to the previous version of a deployment.|
| `kubectl delete deployment <deployment-name>`                  | Delete a deployment by name.                      |

### 5. **Namespace Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get namespaces`                                       | List all namespaces in the cluster.               |
| `kubectl create namespace <namespace-name>`                    | Create a new namespace.                           |
| `kubectl delete namespace <namespace-name>`                    | Delete a namespace by name.                       |
| `kubectl config set-context --current --namespace=<namespace>` | Set the default namespace for the current context.|
| `kubectl get pods --namespace=<namespace>`                     | Get pods in a specific namespace.                 |

### 6. **Node Management Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get nodes`                                            | List all nodes in the cluster.                    |
| `kubectl describe node <node-name>`                            | Show detailed information about a node.           |
| `kubectl cordon <node-name>`                                   | Mark a node as unschedulable.                     |
| `kubectl drain <node-name>`                                    | Safely evict all pods from a node.                |
| `kubectl uncordon <node-name>`                                 | Mark a node as schedulable again.                 |

### 7. **ConfigMap & Secret Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl create configmap <configmap-name> --from-file=<file>` | Create a ConfigMap from a file.                   |
| `kubectl get configmap`                                        | List all ConfigMaps in the current namespace.     |
| `kubectl describe configmap <configmap-name>`                  | Show detailed information about a ConfigMap.      |
| `kubectl create secret generic <secret-name> --from-literal=<key>=<value>` | Create a secret from literal values.            |
| `kubectl get secrets`                                          | List all secrets in the current namespace.        |
| `kubectl describe secret <secret-name>`                        | Show detailed information about a secret.         |

### 8. **Logging & Debugging**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl logs <pod-name>`                                      | View logs of a specific pod.                      |
| `kubectl logs <pod-name> -f`                                   | Stream logs of a specific pod.                    |
| `kubectl get events`                                           | Show all cluster events.                          |
| `kubectl describe <resource> <name>`                           | Describe a resource in detail.                    |
| `kubectl exec <pod-name> -- <command>`                         | Run a command in a specific pod.                  |
| `kubectl exec -it <pod-name> -- /bin/bash`                     | Start a Bash session in a running pod.            |
| `kubectl port-forward <pod-name> <local-port>:<pod-port>`      | Forward a local port to a pod.                    |

### 9. **Other Useful Commands**
| Command                                                       | Description                                      |
|---------------------------------------------------------------|--------------------------------------------------|
| `kubectl get --help`                                           | Display help for the `get` command.               |
| `kubectl version`                                              | Show the Kubernetes client and server versions.   |
| `kubectl config view`                                          | Display the current kubeconfig settings.          |
| `kubectl cluster-info`                                         | Display cluster info.                             |
| `kubectl config get-contexts`                                  | List all configured contexts.                     |
| `kubectl config use-context <context-name>`                    | Switch to a specific context.                     |

