# Kubernetes: Zero → Hero — A Step-by-Step Guide for Beginners

*Clear, practical, and hands-on — learn the core Kubernetes concepts and try them with simple YAML and `kubectl` commands.*

---

## Table of contents

1. Introduction
2. What you need (prerequisites)
3. Core concepts: Containers, Pods, Nodes, Cluster
4. Control plane: What keeps the cluster alive
5. Manifests & YAML — the declarative heart
6. `kubectl` essentials — the commands you'll use daily
7. Namespaces, ResourceQuota, Requests & Limits
8. Health probes: readiness and liveness
9. ConfigMaps, Secrets, and Persistent Storage (PV / PVC)
10. Services & Networking
11. Labels & selectors
12. Troubleshooting common gotchas
13. Step-by-step hands-on exercises (copy-paste ready)
14. One-page cheat sheet
15. Where to go next

---

## 1. Introduction

Kubernetes is the industry standard for running containerized applications at scale. This post walks you from zero to beginner-level confidence: you will learn the concepts, author basic YAML manifests, use `kubectl` to create and inspect resources, and run small hands-on exercises to reinforce learning.

Everything here is practical and intentionally simple — the goal is *understanding through doing*.

## 2. What you need (prerequisites)

- A running Kubernetes cluster (minikube, kind, Docker Desktop, or managed cluster).
- `kubectl` configured to talk to that cluster (`kubectl config current-context` should show your cluster).
- A terminal where you can run `kubectl` commands.

> Tip: If you’re using a new cluster, start with a single-node local cluster (minikube or kind) to experiment safely.

## 3. Core concepts: Containers → Pods → Nodes → Cluster

- **Container**: a lightweight unit that packages an application and its dependencies (e.g., Docker image).
- **Pod**: the smallest deployable unit in Kubernetes. A pod may contain one or more containers that share network and storage.
- **Node**: a machine (VM or physical) that runs pods. Nodes host the kubelet and container runtime.
- **Cluster**: a set of nodes managed together by a control plane that schedules and maintains desired state.

Understanding that Kubernetes schedules **pods** (not individual containers) is important: pods are the objects you create and manage.

## 4. Control plane: what keeps the cluster alive

- **API Server**: the front door for `kubectl` and all clients — it validates and processes requests.
- **etcd**: distributed key/value store used to persist cluster state.
- **Scheduler**: chooses which node will run a new pod.
- **Controller Manager**: runs controllers which ensure actual state matches desired state (e.g., keeping a number of replicas running).
- **kubelet**: agent on each node which makes the node follow the desired state (e.g., start containers).

If anything in the control plane fails (especially `etcd`), the cluster’s behavior will be affected.

## 5. Manifests & YAML — the declarative heart

Kubernetes uses YAML manifests to declare the objects you want. A typical manifest has these top-level fields:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx
      image: nginx:stable
```

Key points:
- YAML indentation matters — it defines structure.
- `apiVersion` and `kind` are essential and must match the resource you intend to create.
- Use declarative workflows: `kubectl apply -f` and keep your manifest files in version control.

## 6. `kubectl` essentials — the commands you'll use daily

- `kubectl get <resource>` — list resources (e.g., `kubectl get pods`).
- `kubectl apply -f <file>` — create or update objects from YAML.
- `kubectl describe <resource> <name>` — detailed info plus **events** (first place to look when troubleshooting).
- `kubectl delete -f <file>` — remove objects declared in a file.
- `kubectl exec -it <pod> -- sh` — open a shell inside a container.
- `kubectl logs <pod>` — stream a container’s stdout/stderr.
- `kubectl port-forward pod/<pod> 8080:80` — forward pod port to localhost for quick testing.
- `kubectl cp` — copy files to/from a pod.
- `kubectl label` — add or change labels on objects.
- `kubectl expose` — create a Service (ClusterIP, NodePort, etc.).

Always check the **namespace**: if you see "no resources found," confirm `-n <namespace>` or `--all-namespaces`.

## 7. Namespaces, ResourceQuota, Requests & Limits

- **Namespaces**: provide logical separation inside a single cluster (useful for teams, dev/test/prod isolation, or exams).
- **ResourceQuota**: set limits for a namespace (e.g., total CPU, memory, or number of objects). If quota is reached, new pod creation will be denied.

**Requests vs Limits**:
- **Request**: guaranteed minimum resources for scheduling.
- **Limit**: maximum resources the container may use.

Example snippet inside a container spec:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

Set both requests and limits to avoid noisy-neighbor problems and to make scheduling predictable.

## 8. Health probes: readiness vs liveness

- **Liveness probe**: if failing continuously, the kubelet will kill and restart the container. It detects crashed or stuck applications.
- **Readiness probe**: if failing, the pod is removed from service endpoints and will not receive traffic until it becomes ready again.

Example of adding simple HTTP probes:

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5

readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

Tune `initialDelaySeconds`, `periodSeconds`, and `failureThreshold` carefully: probes that are too aggressive can cause false restarts; probes that are too lax delay detection.

## 9. ConfigMaps, Secrets, and Persistent Storage (PV / PVC)

- **ConfigMap**: store non-sensitive configuration outside the container and mount it as files or environment variables.
- **Secret**: store sensitive data (passwords, tokens). Be cautious: in default clusters secrets may not be encrypted at rest unless explicitly configured.
- **PersistentVolume (PV)**: the actual storage resource (backed by disk, cloud storage, etc.).
- **PersistentVolumeClaim (PVC)**: a request for storage from a pod — the PVC is bound to a PV and then mounted into a pod.

Create examples (imperative):

```bash
kubectl create configmap my-config --from-literal=APP_ENV=dev -n demo
kubectl create secret generic my-secret --from-literal=DB_PASS=s3cr3t -n demo
```

For storage, use a `PersistentVolume` and `PersistentVolumeClaim` in YAML. For dynamic provisioning, clusters use `StorageClass` to provision PVs automatically.

## 10. Services & Networking

Kubernetes Services expose pods to the network and provide stable endpoints.

Types:
- **ClusterIP**: default, reachable only inside the cluster.
- **NodePort**: opens a port on every node so you can reach the service at `<nodeIP>:<nodePort>`.
- **LoadBalancer**: requests a cloud load balancer (when on supported cloud providers).

Example: expose a pod as a NodePort service (quick test scenario):

```bash
kubectl expose pod my-pod --type=NodePort --name=my-pod-svc -n demo
kubectl get svc -n demo
# then curl nodeIP:nodePort from any node
```

Kube-proxy and the service abstraction ensure traffic to the node port is routed to the right pod regardless of which node actually runs that pod.

## 11. Labels & selectors

- **Labels** are key:value pairs attached to objects (`app: web`, `tier: frontend`).
- Services, ReplicaSets, and other controllers use **selectors** to identify which pods to manage.

Add a label:

```bash
kubectl label pod my-pod env=dev -n demo
```

Use selectors in manifests or commands to act on groups of objects.

## 12. Troubleshooting common gotchas

- **Wrong namespace** — often the reason you "can’t see" resources. Use `-n <namespace>` or `--all-namespaces`.
- **Image typos** — a wrong image name prevents pod creation or causes ImagePullBackOff errors.
- **Edits inside containers are ephemeral** — if a pod restarts you lose manual changes. Use ConfigMaps or mounts for persistent configuration.
- **`kubectl top` requires metrics** — install metrics-server (or equivalent) so resource metrics are available.
- **ResourceQuota rejections** — when quota is exhausted, new resource creation will be denied; inspect `kubectl describe quota`.

When troubleshooting, `kubectl describe <resource> <name>` is your friend — it shows events that often point to the root cause.

## 13. Step-by-step hands-on exercises (copy-paste ready)

> Create a folder for practice manifests and copy these examples into files like `pod.yaml`, `svc-nodeport.yaml`, `configmap.yaml`, etc.

### A. Create a namespace for practice

```bash
kubectl create namespace demo
```

### B. Create a simple pod (save as `pod.yaml`)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-demo
  labels:
    app: nginx-demo
spec:
  containers:
    - name: nginx
      image: nginx:stable
      ports:
        - containerPort: 80
```\`

Apply it and inspect:

```bash
kubectl apply -f pod.yaml -n demo
kubectl get pods -n demo
kubectl describe pod nginx-demo -n demo
kubectl logs nginx-demo -n demo
kubectl exec -it nginx-demo -n demo -- sh
```

Use port-forward to test the web server locally:

```bash
kubectl port-forward pod/nginx-demo 8080:80 -n demo
# then open http://localhost:8080
```

### C. Expose the pod as NodePort (quick cluster test)

```bash
kubectl expose pod nginx-demo --type=NodePort --name=nginx-demo-svc -n demo
kubectl get svc -n demo
# find the nodePort and curl <nodeIP>:<nodePort>
```

### D. Create a ConfigMap and mount/use it (imperative example)

```bash
kubectl create configmap web-config --from-literal=WELCOME_MSG="Hello from ConfigMap" -n demo
```

You can also write a full manifest to mount the configmap as a file into a container.

### E. Create a Secret (imperative example)

```bash
kubectl create secret generic db-secret --from-literal=password=pa55w0rd -n demo
```

> Reminder: default clusters may not encrypt secrets at rest. Treat them carefully.

### F. Add readiness & liveness probes to your pod manifest

Update `pod.yaml` to include the `livenessProbe` and `readinessProbe` blocks shown earlier, then `kubectl apply -f pod.yaml -n demo` and observe how the pod moves in/out of service.

### G. Check resource usage (after installing metrics components)

```bash
kubectl top nodes
kubectl top pods -n demo
```

If `kubectl top` reports errors, install the cluster metrics components (see official docs for the exact manifest to apply for your cluster type).

## 14. One-page cheat sheet

- `kubectl get pods` — list pods
- `kubectl describe pod <name>` — inspect pod + events
- `kubectl apply -f <file>` — create/update from manifest
- `kubectl delete -f <file>` — delete resources in file
- `kubectl logs <pod>` — container logs
- `kubectl exec -it <pod> -- sh` — open shell in pod
- `kubectl port-forward pod/<pod> 8080:80` — forward pod port to localhost
- `kubectl create configmap` / `kubectl create secret` — quick creation
- `kubectl expose` — create a Service

## 15. Where to go next

- Practice writing and editing manifests (Pods → Deployments → Services).
- Learn Deployments and ReplicaSets to handle scaling and rolling updates.
- Practice resource requests/limits and set up a ResourceQuota for a namespace.
- Explore persistent storage in your environment (PV/PVC/StorageClass) and how it is provisioned.

---

*This post is intentionally practical: create a demo namespace, try the manifests, and use `kubectl describe` + `kubectl logs` to learn how Kubernetes reports problems. Repeat the exercises until the flow from manifest → `kubectl apply` → pod running → service reachable becomes second nature.*

