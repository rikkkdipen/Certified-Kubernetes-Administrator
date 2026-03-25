<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=260&color=0:030712,20:0F172A,45:111827,70:1E293B,100:000000&text=Certified%20Kubernetes%20Administrator&fontSize=40&fontColor=38BDF8&fontAlignY=36&desc=%20DevOps%20CKA%20Notes%20%7C%20Questions%20%7C%20Practice&descAlignY=58&animation=fadeIn" />
<!-- <h1 align="center">☸️ Certified Kubernetes Administrator</h1> -->
<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=38BDF8&center=true&vCenter=true&width=980&lines=Premium+Cyber+DevOps+CKA+Preparation+Repository;Architecture+%7C+etcd+%7C+Scheduler+%7C+Kubelet+%7C+API+Server;Notes+%7C+Questions+%7C+Hands-on+Practice;Learn+Kubernetes+one+component+at+a+time" alt="Typing SVG" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/CKA-Preparation-38BDF8?style=for-the-badge&logo=kubernetes&logoColor=06121f" />
  <img src="https://img.shields.io/badge/Repository-Active-8B5CF6?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Mode-Notes%20%2B%20Questions%20%2B%20Practice-22C55E?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Focus-Kubernetes%20Fundamentals-F97316?style=for-the-badge" />
</p>

<p align="center">
  <b>A structured, revision-friendly, hands-on repository for learning Kubernetes deeply and preparing for the Certified Kubernetes Administrator exam.</b>
</p>

<p align="center">
  Built to organize Kubernetes concepts into <b>clear notes</b>, <b>self-check questions</b>, and <b>practical learning files</b> in one place.
</p>

---

## `> repo.mission`

```bash
repository   : Certified-Kubernetes-Administrator
purpose      : structured CKA preparation
style        : concept-first, practical, revision-friendly
workflow     : learn -> write -> question -> practice -> revise
goal         : strong Kubernetes fundamentals + exam readiness
````

---

## `> table.of.contents`

* [Why This Repository Exists](#-why-this-repository-exists)
* [Quick Access](#-quick-access)
* [Repository Structure](#-repository-structure)
* [What Youll Find Here](#-what-youll-find-here)
* [Learning Workflow](#-learning-workflow)
* [Skills This Repo Helps Build](#-skills-this-repo-helps-build)
* [Current Learning Roadmap](#-current-learning-roadmap)
* [Current Focus](#-current-focus)
* [Recommended Study Path](#-recommended-study-path)
* [Contributions](#-contributions)
* [Support](#-support)
* [Author](#-author)

---

## `> why.this.repository.exists`

Most Kubernetes learners keep notes in random places.

This repository exists to turn scattered learning into a clean system where every topic can be studied through:

* notes
* questions
* practice files
* topic-wise folders

The idea is simple:

```text
less confusion
more structure
faster revision
better CKA preparation
```

---

## `> quick.access`

<p align="center">
  <a href="./Architecture"><img src="https://img.shields.io/badge/Architecture-0EA5E9?style=for-the-badge" /></a>
  <a href="./Docker-vs-Containerd"><img src="https://img.shields.io/badge/Docker%20vs%20Containerd-8B5CF6?style=for-the-badge" /></a>
  <a href="./controllerManager"><img src="https://img.shields.io/badge/Controller%20Manager-F97316?style=for-the-badge" /></a>
  <a href="./etcd"><img src="https://img.shields.io/badge/etcd-10B981?style=for-the-badge" /></a>
</p>

<p align="center">
  <a href="./etcd-in-kubernetes"><img src="https://img.shields.io/badge/etcd%20in%20Kubernetes-2563EB?style=for-the-badge" /></a>
  <a href="./kube-api-server"><img src="https://img.shields.io/badge/Kube%20API%20Server-E11D48?style=for-the-badge" /></a>
  <a href="./kubelet"><img src="https://img.shields.io/badge/Kubelet-06B6D4?style=for-the-badge" /></a>
  <a href="./kubeproxy"><img src="https://img.shields.io/badge/Kube%20Proxy-A855F7?style=for-the-badge" /></a>
  <a href="./scheduler"><img src="https://img.shields.io/badge/Scheduler-84CC16?style=for-the-badge" /></a>
</p>

---

## `> repository.structure`

```bash
Certified-Kubernetes-Administrator/
├── Architecture/
│   ├── architecture.md
│   ├── misc.txt
│   └── questions.txt
├── Docker-vs-Containerd/
├── controllerManager/
├── etcd/
├── etcd-in-kubernetes/
│   ├── etcd-in-k8s.txt
│   └── questions.txt
├── kube-api-server/
├── kubelet/
├── kubeproxy/
├── scheduler/
│   ├── manualScheduling.txt
│   ├── notes.txt
│   └── questions.txt
└── abc.txt
```

---

## `> what.youll.find.here`

<table>
  <tr>
    <th align="left">Type</th>
    <th align="left">Purpose</th>
  </tr>
  <tr>
    <td><b>Notes</b></td>
    <td>Simple, revision-friendly explanations of Kubernetes concepts</td>
  </tr>
  <tr>
    <td><b>Questions</b></td>
    <td>Self-check prompts to verify understanding after each topic</td>
  </tr>
  <tr>
    <td><b>Practice Files</b></td>
    <td>Hands-on examples, commands, and scenario-based learning</td>
  </tr>
  <tr>
    <td><b>Topic Folders</b></td>
    <td>Organized study path for major Kubernetes components</td>
  </tr>
</table>

---

## `> learning.workflow`

<p align="center">
  <img src="https://img.shields.io/badge/01-LEARN-0EA5E9?style=for-the-badge" />
  <img src="https://img.shields.io/badge/02-WRITE-8B5CF6?style=for-the-badge" />
  <img src="https://img.shields.io/badge/03-QUESTION-F97316?style=for-the-badge" />
  <img src="https://img.shields.io/badge/04-PRACTICE-22C55E?style=for-the-badge" />
  <img src="https://img.shields.io/badge/05-REVISE-E11D48?style=for-the-badge" />
</p>

```text
Learn → Write → Question → Practice → Revise → Repeat
```

<p align="center">
  <i>Study small. Understand deeply. Repeat consistently.</i>
</p>

---

## `> skills.this.repo.helps.build`

* Kubernetes architecture understanding
* control plane component clarity
* etcd and cluster state awareness
* scheduler and pod placement concepts
* kubelet responsibilities at node level
* kube-proxy and networking basics
* container runtime understanding
* disciplined CKA-style revision

---

## `> current.learning.roadmap`

<table align="center">
  <tr>
    <td><b>Architecture</b></td>
    <td><code>████████░░ 80%</code></td>
  </tr>
  <tr>
    <td><b>etcd</b></td>
    <td><code>███████░░░ 70%</code></td>
  </tr>
  <tr>
    <td><b>Scheduler</b></td>
    <td><code>███████░░░ 70%</code></td>
  </tr>
  <tr>
    <td><b>Kube API Server</b></td>
    <td><code>██████░░░░ 60%</code></td>
  </tr>
  <tr>
    <td><b>Kubelet</b></td>
    <td><code>██████░░░░ 60%</code></td>
  </tr>
  <tr>
    <td><b>Kube Proxy</b></td>
    <td><code>█████░░░░░ 50%</code></td>
  </tr>
  <tr>
    <td><b>Container Runtime Concepts</b></td>
    <td><code>█████░░░░░ 50%</code></td>
  </tr>
</table>

<p align="center">
  <i>This roadmap is manual and reflects my current learning journey.</i>
</p>

---

## `> current.focus`

```bash
[+] Kubernetes architecture
[+] Core control plane components
[+] etcd and cluster state
[+] Scheduler behavior and pod placement
[+] Kubelet and node operations
[+] Networking basics with kube-proxy
[+] Revision-first CKA preparation
```

---

## `> recommended.study.path`

1. Start with **Architecture**
2. Move to **etcd** and **etcd-in-kubernetes**
3. Study **scheduler**, **kube-api-server**, and **controller-manager**
4. Revise using the `questions.txt` files
5. Practice commands and scenarios
6. Repeat until the concepts feel natural

---

## `> contributions`

This repository is mainly my personal learning space, but useful suggestions are welcome.

You can contribute by:

* opening an issue
* suggesting improvements
* fixing mistakes
* creating a pull request

---

## `> support.and.fuel`

<p align="center">
  <img src="https://img.shields.io/badge/STAR%20THIS%20REPO-IF%20IT%20HELPS-FACC15?style=for-the-badge&logo=github&logoColor=111827" />
  <a href="https://buymeacoffee.com/rikkkdipen" target="_blank">
    <img src="https://img.shields.io/badge/FUEL%20THIS%20JOURNEY-FFDD00?style=for-the-badge&logo=buymeacoffee&logoColor=111827" alt="Buy Me a Coffee" />
  </a>
</p>

<p align="center">
  Found this repository helpful for your Kubernetes or CKA preparation?<br>
  Consider giving it a star and supporting the journey with a coffee ☕
</p>

---

## `> author`

<p align="center">
  <a href="https://github.com/rikkkdipen">
    <img src="https://img.shields.io/badge/GitHub-rikkkdipen-111827?style=for-the-badge&logo=github&logoColor=white" />
  </a>
  <a href="https://www.linkedin.com/in/dipenrikkaame/">
    <img src="https://img.shields.io/badge/LinkedIn-Dipen-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
</p>

---

## `> final.message`

```text
Kubernetes becomes easier when you study it one component at a time.
```

<p align="center">
  <b>Build strong fundamentals. Practice deeply. Revise consistently.</b>
</p>
