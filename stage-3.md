# ☸️ DevOps Roadmap – Stage 3: Kubernetes (Container Orchestration)

Kubernetes (K8s) helps you deploy, scale, and manage containerized applications in production reliably and efficiently.

## 🧠 1. What is Kubernetes?

Kubernetes is an open-source platform for orchestrating containers. It automates:

- Deployment of containers
- Scaling (up/down)
- Networking between services
- High availability
- Self-healing (auto-restarts and reschedules)

## 🧩 2. Core Kubernetes Concepts

| Term | Description |
| ---- | ----------- |
| Pod | Smallest unit; wraps one or more containers |
| Node | Worker machine (VM or physical) that runs pods |
| Cluster | A group of nodes |
| Deployment | Manages pod lifecycle and replicas |
| Service | Exposes a set of pods as a network service |
| ConfigMap/Secret | External configuration or credentials |
| Namespace | Virtual cluster within a cluster |
| Volume | Persistent storage for pods |
| Ingress | HTTP gateway for external access |

## 🔧 3. Set Up a Local Kubernetes Environment

**Option A:** Minikube (for beginners)

```bash
minikube start
kubectl get nodes
```

- [🧪 Minikube Guide](https://minikube.sigs.k8s.io/docs/start/)

**Option B:** Kind (Kubernetes in Docker)

```bash
kind create cluster
kubectl cluster-info
```

- [🧪 Kind Getting Started](https://kind.sigs.k8s.io/docs/user/quick-start/)

**Install kubectl (Kubernetes CLI):**

```bash
sudo apt install kubectl
# or use brew or curl method
```

🔹 Install kubectl (CLI):

- [📖 Install guide](https://kubernetes.io/docs/tasks/tools/)

## 🧭 4. Deploy Your First Nginx App

Create a YAML manifest `nginx-deployment.yaml`:

```yaml
# nginx-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80
```

Apply it:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl get pods
```

## 🌐 5. Expose Your App

```bash
kubectl expose deployment nginx-deployment --type=NodePort --port=80
kubectl get svc
```

Then access using:

```bash
minikube service nginx-deployment
```

## 🔍 6. Inspect, Debug, and Access Pods

```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/sh
```

## ⚙️ 7. Common Resources and YAML Templates

| Resource | Command |
| -------- | ------- |
| Pod | kubectl run / kubectl apply -f pod.yaml |
| Deployment | kubectl create deployment |
| Service | kubectl expose deployment |
| Namespace | kubectl create ns <name> |
| ConfigMap | kubectl create configmap mycfg --from-literal=key=value |

## 📁 8. Configuration & Secrets

```yaml
# config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  LOG_LEVEL: debug
```

```bash
kubectl apply -f config.yaml
kubectl describe configmap my-config
```

[Configmap Docs](https://kubernetes.io/docs/concepts/configuration/configmap/)

```yaml
# secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: cGFzc3dvcmQ=  # base64 encoded
```

[Secret Docs](https://kubernetes.io/docs/concepts/configuration/secret/)

Use in pod as environment variable or volume.

## 📈 9. Health Checks (Readiness & Liveness)

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```

**Liveness Probe:** Restart if unhealthy

**Readiness Probe:** Don't send traffic if unready

[Probes Docs](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

## 🛠 10. Practice Tasks

01. Deploy nginx, expose it as a NodePort, and access via browser.
02. Create a ConfigMap for app configuration and mount it.
03. Simulate a crash in a pod and watch Kubernetes restart it.
04. Use labels/selectors to group and query pods.

## 🧪 Self-Check Questions

- What happens when a pod crashes?
- How do you scale your deployment from 2 to 5 pods?
- What’s the difference between a Service and Ingress?
- When should you use a ConfigMap vs a Secret?

## Learning Resources

| Topic                              | Resource                                                                                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Official Kubernetes Docs           | [https://kubernetes.io/docs/](https://kubernetes.io/docs/)                                                               |
| Minikube (local cluster)           | [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)                                     |
| Kind (Kubernetes-in-Docker)        | [https://kind.sigs.k8s.io/](https://kind.sigs.k8s.io/)                                                                   |
| Katacoda Scenarios (Archived)      | [https://www.katacoda.com/courses/kubernetes](https://www.katacoda.com/courses/kubernetes)                               |
| Learnk8s Tutorials                 | [https://learnk8s.io/](https://learnk8s.io/)                                                                             |
| Kubernetes the Hard Way (Advanced) | [https://github.com/kelseyhightower/kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way) |
| Kubernetes Hands-on Labs           | [https://www.kodekloud.com/courses/devops-practice-labs/](https://www.kodekloud.com/courses/devops-practice-labs/)       |

## 📚 Resources

- [Kubernetes Docs](https://kubernetes.io/docs/home/)
- [Play with Kubernetes (Labs)](https://labs.play-with-k8s.com/)
- [Katacoda Kubernetes Scenarios (Archived but useful)](https://www.katacoda.com/courses/kubernetes)
- [Learnk8s Tutorials](https://learnk8s.io/)
