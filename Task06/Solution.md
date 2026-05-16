# Task 6/40 — KIND Cluster Setup 🚀

In this task, I learned how to create Kubernetes clusters locally using KIND (Kubernetes IN Docker).

I explored:
- Single-node Kubernetes cluster
- Multi-node Kubernetes cluster
- Kubectl client installation
- Kubernetes contexts
- How KIND uses Docker containers as Kubernetes nodes

---

# ☸️ What is KIND?

KIND stands for:

> Kubernetes IN Docker

KIND creates Docker containers and uses them as Kubernetes nodes.

This helps us practice Kubernetes locally without using cloud infrastructure.

---

# 🛠️ Installed Single Node KIND Cluster

First, I created a single-node Kubernetes cluster using KIND with Kubernetes version `1.29`.

Example command:

```bash
kind create cluster --name cka-cluster1 --image kindest/node:v1.29.0
```

---

# 🗑️ Deleted the Single Node Cluster

After verification, I deleted the cluster.

```bash
kind delete cluster --name cka-cluster1
```

---

# 🚀 Created Multi-Node KIND Cluster

Next, I created a multi-node cluster with:

- 1 Control Plane
- 3 Worker Nodes
- Kubernetes Version 1.30

Cluster Name:

```text
cka-cluster2
```

---

# 📄 KIND Configuration File

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4

nodes:
  - role: control-plane
    image: kindest/node:v1.30.0

  - role: worker
    image: kindest/node:v1.30.0

  - role: worker
    image: kindest/node:v1.30.0

  - role: worker
    image: kindest/node:v1.30.0
```

---

# ▶️ Create Multi-Node Cluster

```bash
kind create cluster --name cka-cluster2 --config kind-config.yaml
```

---

# ⚙️ Installed Kubectl Client

Installed kubectl client for interacting with Kubernetes clusters.

Verification:

```bash
kubectl version --client
```

---

# 🔄 Set Current Kubernetes Context

```bash
kubectl config use-context kind-cka-cluster2
```

This sets the current cluster context.

---

# 📌 Verified Cluster Nodes

```bash
kubectl get nodes
```

Example output:

```text
NAME                                 STATUS   ROLES
cka-cluster2-control-plane           Ready    control-plane
cka-cluster2-worker                  Ready    worker
cka-cluster2-worker2                 Ready    worker
cka-cluster2-worker3                 Ready    worker
```

---

# 🐳 Verified Nodes as Docker Containers

Since KIND uses Docker internally, all Kubernetes nodes run as Docker containers.

Verification:

```bash
docker ps
```

This command displayed all control-plane and worker nodes as running containers.

---

# 🧠 Key Learnings

## ✅ KIND simplifies Kubernetes learning

KIND allows running Kubernetes locally without cloud infrastructure.

---

## ✅ Kubernetes Nodes Can Run as Containers

KIND uses Docker containers as Kubernetes nodes.

---

## ✅ Multi-Node Clusters Simulate Real Production Environments

Having worker nodes helps understand:
- Pod scheduling
- Cluster management
- High availability
- Workload distribution

---

## ✅ Kubectl is the Main Kubernetes Client Tool

Kubectl helps manage Kubernetes resources from the command line.

---

# 🚀 Important Commands Used

## Create Cluster

```bash
kind create cluster
```

Purpose:
Creates Kubernetes cluster using KIND.

---

## Delete Cluster

```bash
kind delete cluster
```

Purpose:
Deletes existing KIND cluster.

---

## Get Kubernetes Nodes

```bash
kubectl get nodes
```

Purpose:
Displays cluster nodes.

---

## View Docker Containers

```bash
docker ps
```

Purpose:
Shows KIND nodes running as Docker containers.

---

## Check Current Context

```bash
kubectl config current-context
```

Purpose:
Displays active Kubernetes cluster context.

---

# 🎯 Conclusion

This task helped me understand:
- Kubernetes cluster setup using KIND
- Difference between single-node and multi-node clusters
- Kubernetes contexts
- How Kubernetes nodes work internally using Docker containers

It also provided hands-on experience with local Kubernetes environments useful for CKA and CKS preparation.

---

# 📚 References

- KIND Official Documentation
- Kubernetes Official Documentation
- Tech Tutorials With Piyush Kubernetes Series

---

# 🔖 Tags

`#40daysofkubernetes` `#Kubernetes` `#KIND` `#Docker` `#DevOps` `#CloudNative`
