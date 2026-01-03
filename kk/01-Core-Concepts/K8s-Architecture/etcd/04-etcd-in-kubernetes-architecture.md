# etcd in Kubernetes Architecture

In Kubernetes, **only one component talks to etcd**:

> ✅ The Kube API Server

---

## Request Flow Example

1. User runs:
   ```bash
   kubectl apply -f pod.yaml
2. Request goes to the API Server

3. API Server writes desired state to etcd

4. Controllers watch etcd for changes

5. Controllers act to match real state

