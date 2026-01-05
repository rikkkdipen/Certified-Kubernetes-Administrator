# 🏆 My CKA Exam Prep Journey (65 Days)

**Start Date:** January 5th  
**Exam Date:** March 10th  
**Goal:** Pass Certified Kubernetes Administrator (CKA)  
**Status:** 🏃 In Progress

---

## 🧭 How to use this tracker
1.  **Daily:** Complete the tasks for the day.
2.  **Mark:** Put an `x` in the checkbox `[ ]` -> `[x]`.
3.  **Commit:** Save the file to track your streak.
4.  **Reflect:** Add notes in the "Struggle Log" at the bottom.

---

## 📊 Progress Dashboard
*Keep your "Why" in mind: Mastery of Kubernetes.*

- [ ] **Phase 1: Foundation** (Jan 5 - Jan 18)
- [ ] **Phase 2: Scheduling & Logging** (Jan 19 - Feb 1)
- [ ] **Phase 3: Maintenance, Net, Storage** (Feb 2 - Feb 15)
- [ ] **Phase 4: Security** (Feb 16 - Mar 1)
- [ ] **Phase 5: Exam Sim & Troubleshooting** (Mar 2 - Mar 10)

---

## 🗓️ Phase 1: The Foundation
*Focus: Core Concepts & Architecture*

<details open>
<summary><b>Week 1: Architecture & Basic Objects (Jan 5 - Jan 11)</b></summary>

- [ ] **Day 01 (Jan 05):** Architecture (ETCD, API, Scheduler, Kubelet)
- [ ] **Day 02 (Jan 06):** Pods (YAML structure, `kubectl run`)
- [ ] **Day 03 (Jan 07):** ReplicaSets (Selectors, Scaling)
- [ ] **Day 04 (Jan 08):** Deployments (Rolling Updates, Rollbacks)
- [ ] **Day 05 (Jan 09):** Services Part 1 (ClusterIP, NodePort)
- [ ] **Day 06 (Jan 10):** Namespaces & Contexts (ResourceQuotas)
- [ ] **Day 07 (Jan 11):** 🛑 **Review:** Redo hardest lab & Update notes
</details>

<details>
<summary><b>Week 2: Imperative vs. Declarative (Jan 12 - Jan 18)</b></summary>

- [ ] **Day 08 (Jan 12):** Imperative Drills (`kubectl run`, `create deploy`)
- [ ] **Day 09 (Jan 13):** Declarative (`diff`, `replace`, `apply`)
- [ ] **Day 10 (Jan 14):** Editing Live Objects (`edit`, `get -o yaml`)
- [ ] **Day 11 (Jan 15):** Container CMDS (CMD vs ENTRYPOINT)
- [ ] **Day 12 (Jan 16):** Env Vars & ConfigMaps
- [ ] **Day 13 (Jan 17):** Secrets (Encoding, Mounting)
- [ ] **Day 14 (Jan 18):** 🧪 **Bi-Weekly Mini Mock:** Deployments/Expose/Update
</details>

---

## 🗓️ Phase 2: Scheduling & Observation
*Focus: Placement, Logging, Monitoring*

<details>
<summary><b>Week 3: Scheduling (Jan 19 - Jan 25)</b></summary>

- [ ] **Day 15 (Jan 19):** Manual Scheduling & Labels
- [ ] **Day 16 (Jan 20):** Taints and Tolerations
- [ ] **Day 17 (Jan 21):** Node Affinity
- [ ] **Day 18 (Jan 22):** Resource Limits/Requests (OOMKilled)
- [ ] **Day 19 (Jan 23):** DaemonSets
- [ ] **Day 20 (Jan 24):** Static Pods (Manifests in `/etc`)
- [ ] **Day 21 (Jan 25):** 🛑 **Review:** Static Pods & Scheduling
</details>

<details>
<summary><b>Week 4: Logging & Monitoring (Jan 26 - Feb 1)</b></summary>

- [ ] **Day 22 (Jan 26):** Cluster Roles (Master vs Worker)
- [ ] **Day 23 (Jan 27):** Monitoring (`metrics-server`, `top`)
- [ ] **Day 24 (Jan 28):** Logging (`logs -f`, `logs -c`)
- [ ] **Day 25 (Jan 29):** Multiple Schedulers
- [ ] **Day 26 (Jan 30):** Troubleshooting Scheduling
- [ ] **Day 27 (Jan 31):** **Catch-up / Buffer Day**
- [ ] **Day 28 (Feb 01):** 🧪 **Bi-Weekly Mini Mock:** Scheduling & Limits
</details>

---

## 🗓️ Phase 3: The Heavy Lifting
*Focus: Upgrades, Networking, Storage*

<details>
<summary><b>Week 5: App Lifecycle & Maintenance (Feb 2 - Feb 8)</b></summary>

- [ ] **Day 29 (Feb 02):** OS Upgrades (Drain/Cordon)
- [ ] **Day 30 (Feb 03):** Cluster Upgrade (`kubeadm upgrade`)
- [ ] **Day 31 (Feb 04):** Backup 1 (ETCD Snapshot Save)
- [ ] **Day 32 (Feb 05):** Restore 2 (ETCD Snapshot Restore)
- [ ] **Day 33 (Feb 06):** InitContainers
- [ ] **Day 34 (Feb 07):** Self-Healing (Probes)
- [ ] **Day 35 (Feb 08):** 🛑 **Review:** Break cluster & Restore
</details>

<details>
<summary><b>Week 6: Storage & Networking I (Feb 9 - Feb 15)</b></summary>

- [ ] **Day 36 (Feb 09):** PV & PVCs
- [ ] **Day 37 (Feb 10):** Storage Classes
- [ ] **Day 38 (Feb 11):** Networking Basics (CNI/IPAM)
- [ ] **Day 39 (Feb 12):** DNS (CoreDNS, `nslookup`)
- [ ] **Day 40 (Feb 13):** Ingress Resources
- [ ] **Day 41 (Feb 14):** Ingress Controllers
- [ ] **Day 42 (Feb 15):** 🧪 **Week 6 Mock Exam:** ETCD + Storage
</details>

---

## 🗓️ Phase 4: Security
*Focus: Authentication, Authorization, Policies*

<details>
<summary><b>Week 7: Auth & RBAC (Feb 16 - Feb 22)</b></summary>

- [ ] **Day 43 (Feb 16):** Authentication (Certs/Kubeconfig)
- [ ] **Day 44 (Feb 17):** Service Accounts
- [ ] **Day 45 (Feb 18):** RBAC 1 (Roles/Bindings)
- [ ] **Day 46 (Feb 19):** RBAC 2 (ClusterRoles)
- [ ] **Day 47 (Feb 20):** `auth can-i`
- [ ] **Day 48 (Feb 21):** Security Contexts (User/Group IDs)
- [ ] **Day 49 (Feb 22):** 🛑 **Review:** RBAC Deep Dive
</details>

<details>
<summary><b>Week 8: Network Security (Feb 23 - Mar 1)</b></summary>

- [ ] **Day 50 (Feb 23):** Network Policies 1 (Default Deny)
- [ ] **Day 51 (Feb 24):** Network Policies 2 (Egress/Ingress)
- [ ] **Day 52 (Feb 25):** Docker/CRI (`crictl`)
- [ ] **Day 53 (Feb 26):** Adv. Troubleshooting (CNI)
- [ ] **Day 54 (Feb 27):** JSON Path (Custom Output)
- [ ] **Day 55 (Feb 28):** **Mock Exam Prep**
- [ ] **Day 56 (Mar 01):** 🧪 **Week 8 Major Mock Exam (2 Hours)**
</details>

---

## 🗓️ Phase 5: The Final Sprint
*Focus: Troubleshooting & Simulation*

<details>
<summary><b>Week 9: Troubleshooting Masterclass (Mar 2 - Mar 6)</b></summary>

- [ ] **Day 57 (Mar 02):** **Control Plane Failure** (Simulate Crash)
- [ ] **Day 58 (Mar 03):** **Worker Node Failure** (Kubelet/Certs)
- [ ] **Day 59 (Mar 04):** **Network Failure** (CNI/DNS)
- [ ] **Day 60 (Mar 05):** 🧪 **Full Mock Exam 1**
- [ ] **Day 61 (Mar 06):** **Mock Analysis** (Review failures)
</details>

<details>
<summary><b>Week 10: The Last Mile (Mar 7 - Mar 10)</b></summary>

- [ ] **Day 62 (Mar 07):** **Speed Run** (Lightning Labs)
- [ ] **Day 63 (Mar 08):** 🧪 **Full Mock Exam 2**
- [ ] **Day 64 (Mar 09):** **Rest & Light Review** (Memorize Cheatsheet)
- [ ] **Day 65 (Mar 10):** 🏁 **EXAM DAY**
</details>

---

## 🧠 Struggle Log
*Edit this section to add commands or concepts you keep forgetting.*

### 📝 Commands to Memorize
```bash
# The "Golden" Alias
alias k=kubectl
export do="--dry-run=client -o yaml"

# Check certificate expiry
kubeadm certs check-expiration

# Run a temporary busybox to test DNS
k run test --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-service
