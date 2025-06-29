
# Week 6 Task

## Overview
This guide provides step-by-step instructions to deploy and manage various Kubernetes components and configurations on Azure Kubernetes Service (AKS). It includes deployments, ReplicaSets, ReplicationControllers, service types, volumes, probes, scaling, and more.

---

## 1. Deploy ReplicaSet, ReplicationController, and Deployment

### Create a ReplicaSet
```bash
kubectl apply -f replicaset.yaml
```
Example: replicaset.yaml
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: mycontainer
        image: nginx
```

### Create a ReplicationController
```bash
kubectl apply -f replicationcontroller.yaml
```
Example: replicationcontroller.yaml
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: my-rc
spec:
  replicas: 2
  selector:
    app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: mycontainer
        image: nginx
```

### Create a Deployment
```bash
kubectl apply -f deployment.yaml
```
Example: deployment.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: mycontainer
        image: nginx
```

## 2. Kubernetes Service Types

```bash
kubectl expose deployment my-deployment --type=ClusterIP --port=80
kubectl expose deployment my-deployment --type=NodePort --port=80
kubectl expose deployment my-deployment --type=LoadBalancer --port=80
```

## 3. PersistentVolume and PersistentVolumeClaim

```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

## 4. AKS Cluster Management

### Create AKS Cluster
```bash
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
```

### Scale AKS Cluster
```bash
az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3
```

### Upgrade AKS Cluster
```bash
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version 1.27.3
```

## 5. Configure Liveness and Readiness Probes

Add this to your pod spec:
```yaml
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 3
  periodSeconds: 3
readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 5
```

## 6. Taints and Tolerations

```bash
kubectl taint nodes <node-name> key=value:NoSchedule
```

In pod spec:
```yaml
tolerations:
- key: "key"
  operator: "Equal"
  value: "value"
  effect: "NoSchedule"
```

## 7. Create and Attach PVC to Pods

Attach PVC in pod spec:
```yaml
volumes:
- name: mypvc
  persistentVolumeClaim:
    claimName: myclaim
```

## 8. Configure Health Probes

Same as step 5 for liveness/readiness.

## 9. Configure Autoscaling

Enable autoscaler:
```bash
kubectl autoscale deployment my-deployment --cpu-percent=50 --min=1 --max=5
```

---

## References
YouTube & Microsoft Learn links provided in the assignment.
