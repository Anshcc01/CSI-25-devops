
# Kubernetes / AKS Assignment Guide

This guide covers the complete steps to:

- Create Kubernetes clusters using Minikube and Kubeadm  
- Deploy and manage AKS (Azure Kubernetes Service) via the portal  
- Deploy microservices and expose them using different service types

---

## 1. Create a Kubernetes Cluster using Minikube

### 📌 Prerequisites
- Install [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/)

### ✅ Steps
```bash
minikube start                # Starts a local cluster
kubectl get nodes             # Check if the node is ready
minikube dashboard            # Optional: Access GUI dashboard
```

### 📺 Resource
[YouTube Video](https://www.youtube.com/watch?v=c4nTKMU6fBU)

---

## 2. Create Kubernetes Cluster using kubeadm

### 📌 Prerequisites
- 2 Linux VMs (master + worker)
- Docker and kubeadm installed
- Disable swap memory

### ✅ Steps (Master Node)
```bash
sudo kubeadm init
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```

### ✅ Steps (Worker Node)
```bash
# From master, get the join command:
kubeadm token create --print-join-command
# Run on worker:
sudo kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### 📺 Resource
[YouTube Video](https://www.youtube.com/watch?v=gyjFNkk3QxY)

---

## 3. Deploy an AKS Cluster using Azure Portal

### ✅ Steps
1. Go to Azure Portal → "Create a resource" → Kubernetes Service
2. Fill in:
   - Resource Group
   - Cluster Name
   - Region, Node Size, Count
3. Enable Kubernetes dashboard in Monitoring
4. Click **Review + Create**

### ✅ Create Roles for Users
- Navigate to AKS → "Access control (IAM)"
- Assign roles like **Azure Kubernetes Service RBAC Viewer** or **Contributor**

### 📺 Resource
[YouTube Video](https://www.youtube.com/watch?v=XEdwGvS2AwA)

---

## 4. Deploy a Microservice Application on AKS Cluster

### ✅ Steps
```bash
# Connect local CLI to AKS
az login
az aks get-credentials --resource-group <rg-name> --name <cluster-name>

# Apply deployment YAML
kubectl apply -f microservice-deployment.yaml

# Confirm deployment
kubectl get pods
```

### 📺 Resource
[YouTube Video](https://www.youtube.com/watch?v=JDoRXJNr4es)

---

## 5. Expose Services in the Cluster

### ✅ NodePort
```yaml
type: NodePort
```
```bash
kubectl expose deployment <name> --type=NodePort --port=80
minikube service <name>
```

### ✅ ClusterIP (default)
```bash
kubectl expose deployment <name> --port=80
kubectl get service
```

### ✅ LoadBalancer
```bash
kubectl expose deployment <name> --type=LoadBalancer --port=80
kubectl get svc
```

### 📺 Resource
[YouTube Video](https://www.youtube.com/watch?v=uCh3iym4HZ8)

---

## ✅ Summary

| Task | Tools |
|------|-------|
| Minikube Cluster | `minikube` |
| Kubeadm Cluster | `kubeadm`, `docker` |
| AKS Portal Deployment | Azure Portal |
| Microservice Deployment | `kubectl`, `az` |
| Expose Services | NodePort, ClusterIP, LoadBalancer |

---

> **Tip**: Always verify each step using `kubectl get pods/services/nodes` for visibility.
