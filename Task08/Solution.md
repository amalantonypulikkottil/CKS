# Task 8/40 — ReplicaSet & Deployment in Kubernetes 🚀

In this task, I learned how ReplicaSets and Deployments work in Kubernetes. I also explored scaling applications, rollout updates, rollback functionality, and troubleshooting Deployment YAML issues.

This task helped me understand:
- ReplicaSet management
- Deployment lifecycle
- Rolling updates
- Rollback functionality
- Scaling applications
- Kubernetes troubleshooting

---

# ☸️ ReplicaSet

A ReplicaSet ensures that a specified number of pod replicas are always running.

---

# ✅ Create ReplicaSet with 3 Replicas

## ReplicaSet YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet

metadata:
  name: nginx-rs

spec:
  replicas: 3

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
        image: nginx
```

---

# 🚀 Apply ReplicaSet

```bash
kubectl apply -f replicaset.yaml
```

---

# 📌 Verify ReplicaSet

```bash
kubectl get rs
```

```bash
kubectl get pods
```

---

# ✅ Update Replicas to 4 from YAML

Updated:

```yaml
replicas: 3
```

to:

```yaml
replicas: 4
```

---

# 🚀 Apply Updated YAML

```bash
kubectl apply -f replicaset.yaml
```

---

# ✅ Scale ReplicaSet to 6 Using Command

```bash
kubectl scale rs nginx-rs --replicas=6
```

---

# 📌 Verify Scaling

```bash
kubectl get rs
```

---

# ☸️ Deployment

A Deployment manages ReplicaSets and provides advanced features like:
- Rolling updates
- Rollbacks
- Scaling
- Self-healing

---

# ✅ Create Deployment

## Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx
  labels:
    tier: backend

spec:
  replicas: 3

  selector:
    matchLabels:
      app: v1

  template:
    metadata:
      labels:
        app: v1

    spec:
      containers:
      - name: nginx
        image: nginx:1.23.0
```

---

# 🚀 Apply Deployment

```bash
kubectl apply -f deployment.yaml
```

---

# 📌 Verify Deployment

```bash
kubectl get deployment
```

```bash
kubectl get pods
```

---

# ✅ Update Image Version

```bash
kubectl set image deployment/nginx nginx=nginx:1.23.4
```

---

# 📌 Verify Rollout Status

```bash
kubectl rollout status deployment/nginx
```

---

# ✅ Add Change Cause

```bash
kubectl annotate deployment/nginx kubernetes.io/change-cause="Pick up patch version"
```

---

# ✅ Scale Deployment to 5 Replicas

```bash
kubectl scale deployment nginx --replicas=5
```

---

# 📌 Verify Scaling

```bash
kubectl get deployment
```

---

# ✅ View Rollout History

```bash
kubectl rollout history deployment/nginx
```

---

# ✅ Rollback to Revision 1

```bash
kubectl rollout undo deployment/nginx --to-revision=1
```

---

# 📌 Verify Rollback

```bash
kubectl describe deployment nginx
```

Image version reverted to:

```text
nginx:1.23.0
```

---

# ☸️ Troubleshooting Deployment YAML — Issue 1

## ❌ Incorrect YAML

```yaml
apiVersion: v1
kind: Deployment
```

---

# 🚨 Problem

Deployments belong to:

```yaml
apiVersion: apps/v1
```

---

# ✅ Fix

Updated:

```yaml
apiVersion: apps/v1
```

---

# 🚀 Apply Fixed YAML

```bash
kubectl apply -f deployment.yaml
```

---

# ☸️ Troubleshooting Deployment YAML — Issue 2

## ❌ Incorrect Selector Labels

Selector:

```yaml
selector:
  matchLabels:
    env: dev
```

Pod Labels:

```yaml
labels:
  env: demo
```

---

# 🚨 Problem

Deployment selector labels must match pod labels.

---

# ✅ Fix

Updated selector:

```yaml
selector:
  matchLabels:
    env: demo
```

---

# 🚀 Apply Fixed YAML

```bash
kubectl apply -f deployment.yaml
```

---

# 📚 Important Commands Used

| Command | Purpose |
|---|---|
| `kubectl apply -f` | Apply YAML file |
| `kubectl get rs` | View ReplicaSets |
| `kubectl get deployment` | View Deployments |
| `kubectl get pods` | View Pods |
| `kubectl scale` | Scale replicas |
| `kubectl set image` | Update image |
| `kubectl rollout status` | Check rollout |
| `kubectl rollout history` | View rollout history |
| `kubectl rollout undo` | Rollback deployment |
| `kubectl describe deployment` | Detailed deployment info |

---

# 🧠 Key Learnings

## ✅ ReplicaSet
- Maintains desired number of pod replicas
- Automatically recreates failed pods

---

## ✅ Deployment
- Higher-level Kubernetes controller
- Manages ReplicaSets
- Supports rolling updates and rollbacks

---

## ✅ Rolling Updates
- Updates application without downtime
- Gradually replaces old pods with new ones

---

## ✅ Rollback
- Easily revert failed deployments
- Kubernetes maintains revision history

---

## ✅ Scaling
- Applications can be scaled dynamically
- Increase or decrease replicas based on workload

---

# 📌 ReplicaSet vs Deployment

| ReplicaSet | Deployment |
|---|---|
| Maintains replicas | Manages replicas + updates |
| No rollout support | Supports rollout & rollback |
| Lower-level object | Higher-level controller |

---

# 🎯 Conclusion

This task provided hands-on experience with:
- ReplicaSets
- Deployments
- Rolling updates
- Rollbacks
- Scaling applications
- Troubleshooting Kubernetes YAML issues

I also learned how Kubernetes manages application lifecycle efficiently in production environments.

---

# 📖 References

- Kubernetes Official Documentation
- KIND Documentation
- Tech Tutorials With Piyush Kubernetes Series

---

# 🔖 Tags

`#40daysofkubernetes` `#Kubernetes` `#Docker` `#DevOps` `#CloudNative`
