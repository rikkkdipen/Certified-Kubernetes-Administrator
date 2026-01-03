## Kubernetes Architecture Overview

### 🧠 Control Plane (Master Node Components)

- **ETCD Cluster**  
  Stores cluster-wide configuration, state data, and metadata. Acts as the single source of truth for the Kubernetes cluster.

- **Kube API Server**  
  Serves as the central communication hub for the cluster. All components interact with the cluster through the API server.

- **Kube Scheduler**  
  Decides which worker node is the best fit for newly created pods based on resource availability and scheduling policies.

- **Controller Manager**  
  Runs various controllers responsible for maintaining the desired state of the cluster, such as:
  - Node lifecycle management  
  - Pod replication  
  - Self-healing and system stability  

---

### ⚙️ Worker Node Components

- **Kubelet**  
  An agent running on each worker node. It:
  - Receives instructions from the Kube API Server  
  - Creates, updates, and deletes containers  
  - Continuously reports node and pod status back to the control plane  

- **Kube Proxy**  
  Handles networking on worker nodes by configuring network rules.  
  This enables seamless communication between pods across different nodes (e.g., a web server pod communicating with a database pod on another node).

---

### 📌 Key Notes

- **Controllers** (such as the Replication Controller) act like operations staff—ensuring the desired number of pods are always running and handling failures automatically.

- **Containerized Control Plane**  
  All Kubernetes components run as containers. Regardless of the container runtime used—**Docker**, **containerd**, or **CRI-O**—every node (including control plane nodes) must have a compatible container runtime installed.

---

💡 *Kubernetes continuously works to reconcile the actual cluster state with the desired state defined by users, ensuring reliability, scalability, and resilience.*

