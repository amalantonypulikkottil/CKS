# Task 7/40 — Kubernetes Pods & YAML 🚀

In this task, I learned how to create Pods using imperative commands, generate YAML configurations, and troubleshoot pod creation errors in Kubernetes.

This task helped me understand:
- Imperative vs Declarative Kubernetes management
- Pod creation workflow
- YAML configuration files
- Kubernetes troubleshooting using `kubectl describe`

---

# ☸️ Task 1 — Create Pod Using Imperative Command

## ✅ Command Used

```bash
kubectl run nginx-pod --image=nginx
```

---

## 📌 Verify Pod Creation

```bash
kubectl get pods
```

Example Output:

```text
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          10s
```

---

## 📌 Describe Pod

```bash
kubectl describe pod nginx-pod
```

Purpose:
- View pod details
- Check events
- View container information
- Verify node scheduling

---

# ☸️ Task 2 — Generate YAML from Existing Pod

## ✅ Generate YAML

```bash
kubectl get pod nginx-pod -o yaml > nginx-pod.yaml
```

This command exported the running pod configuration into a YAML file.

---

## ✅ Update Pod Name

Changed:

```yaml
name: nginx-pod
```

to:

```yaml
name: nginx-new
```

---

## ✅ Apply Updated YAML

```bash
kubectl apply -f nginx-pod.yaml
```

---

## 📌 Verify New Pod

```bash
kubectl get pods
```

Example Output:

```text
NAME        READY   STATUS    AGE
nginx-pod   1/1     Running   5m
nginx-new   1/1     Running   20s
```

---

# ☸️ Task 3 — Troubleshooting Pod Errors

## ❌ Problematic YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: rediss
    name: redis
```

---

# 🚨 Apply YAML

```bash
kubectl apply -f redis.yaml
```

---

# 📌 Check Pod Status

```bash
kubectl get pods
```

Output:

```text
redis   0/1   ErrImagePull
```

---

# 🔍 Troubleshooting

## Describe Pod

```bash
kubectl describe pod redis
```

Error Message:

```text
Failed to pull image "rediss"
```

Reason:
- Incorrect image name
- `rediss` image does not exist

---

# ✅ Fix the Error

Updated:

```yaml
image: rediss
```

to:

```yaml
image: redis
```

---

# 🗑️ Delete Failed Pod

```bash
kubectl delete pod redis
```

---

# 🚀 Reapply Correct YAML

```bash
kubectl apply -f redis.yaml
```

---

# 📌 Verify Successful Pod

```bash
kubectl get pods
```

Example Output:

```text
redis   1/1   Running
```

---

# 🧠 Key Learnings

## ✅ Imperative Commands

Quick way to create Kubernetes resources.

Example:

```bash
kubectl run
```

---

## ✅ Declarative YAML Files

YAML files provide reusable Kubernetes configurations.

Example:

```bash
kubectl apply -f file.yaml
```

---

## ✅ Kubernetes Troubleshooting

Useful commands:

```bash
kubectl describe pod
kubectl logs
kubectl get pods
```

---

## ✅ Pods Are Temporary Units

Pods can:
- Restart
- Fail
- Be recreated

Kubernetes manages them automatically.

---

## ✅ Image Pull Errors

Incorrect container images cause:
- `ErrImagePull`
- `ImagePullBackOff`

---

# 📚 Important Commands Used

| Command | Purpose |
|---|---|
| `kubectl run` | Create pod |
| `kubectl get pods` | View pods |
| `kubectl describe pod` | Detailed pod information |
| `kubectl apply -f` | Apply YAML |
| `kubectl delete pod` | Delete pod |
| `kubectl exec -it` | Enter running container |
| `kubectl logs` | View container logs |

---

# 🎯 Conclusion

This task provided hands-on experience with:
- Kubernetes Pods
- YAML configurations
- Pod troubleshooting
- Imperative and declarative resource management

It also helped me understand how Kubernetes handles container lifecycle management and error debugging.

---

# 📖 References

- Kubernetes Official Documentation
- KIND Documentation
- Tech Tutorials With Piyush Kubernetes Series

---

# 🔖 Tags

`#40daysofkubernetes` `#Kubernetes` `#Docker` `#DevOps` `#CloudNative`
