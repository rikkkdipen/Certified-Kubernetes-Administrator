# What is etcd?

etcd is the **brain and memory of Kubernetes**.

In simple terms:

> **etcd is a distributed key-value database that stores the entire state of a Kubernetes cluster.**

Kubernetes does not store its data in files or local memory.  
Instead, **everything Kubernetes knows is stored in etcd**.

---

## What does etcd store?

etcd stores **metadata and state**, not application data.

Examples:
- Pods and their status
- Deployments and ReplicaSets
- ConfigMaps and Secrets
- Nodes and their health
- Services and networking info

If etcd goes down permanently → **the cluster forgets everything**.

---

## Real-world analogy

Think of Kubernetes as a company:

- API Server → Front desk
- Scheduler → HR assigning desks
- Controllers → Managers fixing issues
- **etcd → Company register + live status board**

Without etcd, Kubernetes cannot function.

