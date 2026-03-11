# Certified Kubernetes Administrator (CKA) — Prep Repo

This repository is my structured preparation workspace for the **Certified Kubernetes Administrator (CKA)** exam.

It contains:
- Topic-wise notes (short + exam-focused)
- Self-check questions (Q&A)
- Hands-on labs and debugging workflows
- Service + pod networking practice (port-forward, services, endpoints)
- Troubleshooting patterns (Events-first)

---

## CKA Domains (Exam Focus)

The CKA exam is performance-based (hands-on). I’m organizing practice around these core domains:

| Domain | Weight |
|---|---:|
| Troubleshooting | 30% |
| Cluster Architecture, Installation & Configuration | 25% |
| Services & Networking | 20% |
| Workloads & Scheduling | 15% |
| Storage | 10% |

---

## Repo Structure (Current Topics)

- [`Architecture/`](./Architecture) — architecture notes + questions
- [`Docker-vs-Containerd/`](./Docker-vs-Containerd) — runtime concepts + CKA debugging angle
- [`kube-api-server/`](./kube-api-server) — API server notes + questions
- [`controllerManager/`](./controllerManager) — controller manager notes + questions
- [`scheduler/`](./scheduler) — scheduler notes + questions
- [`kubelet/`](./kubelet) — kubelet notes + questions
- [`kubeproxy/`](./kubeproxy) — kube-proxy + service routing notes + questions
- [`etcd/`](./etcd) — etcd beginner notes
- [`etcd-in-kubernetes/`](./etcd-in-kubernetes) — etcd in k8s + questions

---

## How I Study (Loop)

**Daily loop (60–120 mins):**
1. Read `notes.txt` for the topic (fast, exam-focused)
2. Do 1–2 hands-on labs (kubectl + YAML)
3. Answer `questions.txt` without looking
4. Add mistakes to a “mistake log” (what broke + why + fix)

**Weekly loop:**
- Run at least 1 timed drill (30–60 min)
- Re-do the top 5 weakest labs until muscle memory kicks in

---

## Local Lab Setup

I practice primarily on:
- Docker Desktop Kubernetes OR kind (Kubernetes in Docker)
- kubectl configured via kubeconfig

Useful commands:
```bash
kubectl get pods -o wide
kubectl describe pod <name>
kubectl logs <pod> --previous
kubectl get svc,ep
kubectl port-forward svc/<svc> 8080:80
