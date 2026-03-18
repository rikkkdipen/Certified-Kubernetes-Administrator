# imperative-commands.md

# Kubernetes Imperative Commands for CKA (Current Exam-Aligned Guide)

_Last updated: 2026-03-17_

## Important note first

This guide is **CKA-aligned**, but it does **not** claim to reproduce or leak actual Linux Foundation exam questions. The CKA is a live, performance-based, command-line exam, and the exact task set is confidential. Use this file as a **current, exam-safe command reference** built around the latest official CKA scope, the current `kubectl` reference, and the speed patterns emphasized by current prep platforms.

## What this file is for

Use this when you want to:
- create common Kubernetes objects very fast
- generate YAML without writing everything from scratch
- remember the exact `kubectl` syntax under exam pressure
- troubleshoot quickly
- cover the **high-yield commands that repeatedly matter in current CKA prep and simulator-style tasks**

## What this file is not

This is **not** a full Kubernetes theory book.
It is a **practical command guide** for CKA.

---

# 1. Core exam mindset

## 1.1 The fastest pattern in CKA

When a task needs a manifest but you do not want to write YAML from zero:

```bash
kubectl <create-command> --dry-run=client -o yaml > file.yaml
vi file.yaml
kubectl apply -f file.yaml
```

Use this pattern constantly.

## 1.2 When to use pure imperative commands

Use pure imperative commands when the task is simple, such as:
- create a namespace
- create a pod
- create a deployment
- expose a deployment as a service
- create a configmap or secret
- create a job or cronjob
- label, annotate, or scale an existing object

## 1.3 When to switch to YAML quickly

Do **not** waste time fighting the CLI when the task needs:
- probes
- volumes and mounts
- affinity / anti-affinity
- tolerations
- securityContext
- network policies
- storage classes / PVC details
- Gateway API resources
- complex RBAC rules
- pod specs with several nested fields

In those cases, generate YAML first and edit it.

---

# 2. The small set of flags you must memorize

```bash
-n <namespace>
-A                         # all namespaces
-o yaml                    # output as YAML
-o wide                    # wider tabular output
--dry-run=client           # print object without creating it
--show-labels              # include labels in output
-l key=value               # label selector
--sort-by=.metadata.name   # sort results
```

Very common combo:

```bash
kubectl get pods -A -o wide
```

---

# 3. Namespace commands

## 3.1 Create a namespace

```bash
kubectl create namespace dev
```

**What it does:** creates a namespace named `dev`.

## 3.2 Generate namespace YAML

```bash
kubectl create namespace dev --dry-run=client -o yaml
```

**Use when:** the exam wants a file or wants you to modify metadata before creation.

## 3.3 Work inside a namespace

```bash
kubectl get pods -n dev
kubectl describe pod nginx -n dev
kubectl delete pod nginx -n dev
```

---

# 4. Pod commands (`kubectl run`)

`kubectl run` is your fastest way to create a **Pod**.

## 4.1 Create a simple pod

```bash
kubectl run nginx --image=nginx
```

**What it does:** creates a Pod named `nginx` running the `nginx` image.

## 4.2 Create a pod in a namespace

```bash
kubectl run nginx --image=nginx -n dev
```

## 4.3 Create pod YAML without creating the pod

```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

## 4.4 Add labels at creation time

```bash
kubectl run nginx --image=nginx --labels="app=nginx,tier=frontend"
```

## 4.5 Add an environment variable

```bash
kubectl run nginx --image=nginx --env="APP_ENV=prod"
```

## 4.6 Expose a container port in the pod spec

```bash
kubectl run nginx --image=nginx --port=80
```

## 4.7 Override the container command

```bash
kubectl run busybox --image=busybox --command -- sleep 3600
```

**Important:**
- use `--command --` when you want to override the image entrypoint/command
- without it, extra words may be treated as arguments instead of a new command

## 4.8 Fast exam recipe: pod + YAML + edit

```bash
kubectl run api --image=nginx --labels="app=api" --dry-run=client -o yaml > api.yaml
vi api.yaml
kubectl apply -f api.yaml
```

---

# 5. Deployment commands

## 5.1 Create a deployment

```bash
kubectl create deployment web --image=nginx
```

**What it does:** creates a Deployment named `web` with one replica by default.

## 5.2 Create a deployment with replicas

```bash
kubectl create deployment web --image=nginx --replicas=3
```

## 5.3 Add a container port during creation

```bash
kubectl create deployment web --image=nginx --port=80
```

## 5.4 Generate deployment YAML

```bash
kubectl create deployment web --image=nginx --replicas=3 --dry-run=client -o yaml
```

## 5.5 Scale a deployment

```bash
kubectl scale deployment web --replicas=5
```

**What it does:** updates the replica count.

## 5.6 Update the image of a deployment

```bash
kubectl set image deployment/web nginx=nginx:1.28
```

**What it does:** updates the image for the container named `nginx` in Deployment `web`.

## 5.7 Add or change environment variables in a workload

```bash
kubectl set env deployment/web APP_ENV=prod
kubectl set env deployment/web --from=configmap/app-config
```

## 5.8 Set CPU/memory requests and limits

```bash
kubectl set resources deployment/web \
  --requests=cpu=100m,memory=128Mi \
  --limits=cpu=200m,memory=256Mi
```

## 5.9 Restart a rollout

```bash
kubectl rollout restart deployment/web
```

## 5.10 Check rollout status

```bash
kubectl rollout status deployment/web
```

## 5.11 See rollout history

```bash
kubectl rollout history deployment/web
```

## 5.12 Roll back to previous revision

```bash
kubectl rollout undo deployment/web
```

## 5.13 Patch the replica count quickly

```bash
kubectl patch deployment web -p '{"spec":{"replicas":3}}'
```

---

# 6. Service commands

You will use either:
- `kubectl expose`
- or `kubectl create service ...`

## 6.1 Expose an existing deployment as ClusterIP

```bash
kubectl expose deployment web --port=80 --target-port=8080
```

**What it does:** creates a Service that listens on port `80` and sends traffic to container port `8080`.

## 6.2 Expose as NodePort

```bash
kubectl expose deployment web --type=NodePort --port=80 --target-port=8080
```

## 6.3 Generate service YAML from `expose`

```bash
kubectl expose deployment web --type=NodePort --port=80 --target-port=8080 --dry-run=client -o yaml
```

## 6.4 Create ClusterIP directly

```bash
kubectl create service clusterip web-svc --tcp=80:8080
```

## 6.5 Create NodePort directly

```bash
kubectl create service nodeport web-svc --tcp=80:8080
```

## 6.6 Create LoadBalancer directly

```bash
kubectl create service loadbalancer web-svc --tcp=80:8080
```

**Note:** in many lab environments, a LoadBalancer service may stay `pending` unless there is a cloud provider or MetalLB-style implementation.

## 6.7 Verify the service quickly

```bash
kubectl get svc
kubectl describe svc web-svc
kubectl get endpoints web-svc
```

---

# 7. Ingress commands

Current `kubectl` has `kubectl create ingress`, which is useful for simple exam tasks.

## 7.1 Create a basic ingress rule

```bash
kubectl create ingress simple \
  --rule="foo.com/bar=svc1:8080"
```

## 7.2 Create ingress with class

```bash
kubectl create ingress web-ing \
  --class=nginx \
  --rule="example.com/=web-svc:80"
```

## 7.3 Create ingress with TLS secret

```bash
kubectl create ingress secure-ing \
  --class=nginx \
  --rule="example.com/=web-svc:80,tls=my-cert"
```

## 7.4 Generate ingress YAML

```bash
kubectl create ingress web-ing \
  --class=nginx \
  --rule="example.com/=web-svc:80" \
  --dry-run=client -o yaml
```

**Exam note:** if the task uses **Gateway API**, pure imperative creation is usually not enough. Use YAML.

---

# 8. ConfigMap commands

## 8.1 Create from a literal

```bash
kubectl create configmap app-config --from-literal=APP_ENV=prod
```

## 8.2 Create from multiple literals

```bash
kubectl create configmap app-config \
  --from-literal=APP_ENV=prod \
  --from-literal=LOG_LEVEL=info
```

## 8.3 Create from a file

```bash
kubectl create configmap app-config --from-file=config.properties
```

## 8.4 Create from a directory

```bash
kubectl create configmap app-config --from-file=./config-dir/
```

## 8.5 Generate ConfigMap YAML

```bash
kubectl create configmap app-config --from-literal=APP_ENV=prod --dry-run=client -o yaml
```

---

# 9. Secret commands

## 9.1 Create a generic secret from literals

```bash
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=pass123
```

## 9.2 Create a secret from files

```bash
kubectl create secret generic app-secret \
  --from-file=username.txt \
  --from-file=password.txt
```

## 9.3 Create a TLS secret

```bash
kubectl create secret tls tls-secret --cert=cert.crt --key=cert.key
```

## 9.4 Create a Docker registry secret

```bash
kubectl create secret docker-registry regcred \
  --docker-server=my-registry.example.com \
  --docker-username=myuser \
  --docker-password=mypassword \
  --docker-email=me@example.com
```

## 9.5 Generate Secret YAML

```bash
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=pass123 \
  --dry-run=client -o yaml
```

---

# 10. Job and CronJob commands

These are commonly useful in modern CKA practice tasks.

## 10.1 Create a Job

```bash
kubectl create job my-job --image=busybox
```

## 10.2 Create a Job with a command

```bash
kubectl create job my-job --image=busybox -- date
```

## 10.3 Create a Job from an existing CronJob

```bash
kubectl create job adhoc-run --from=cronjob/nightly-backup
```

## 10.4 Generate Job YAML

```bash
kubectl create job my-job --image=busybox --dry-run=client -o yaml
```

## 10.5 Create a CronJob

```bash
kubectl create cronjob my-job --image=busybox --schedule="*/1 * * * *"
```

## 10.6 Create a CronJob with a command

```bash
kubectl create cronjob my-job --image=busybox --schedule="*/5 * * * *" -- date
```

## 10.7 Generate CronJob YAML

```bash
kubectl create cronjob my-job --image=busybox --schedule="*/5 * * * *" --dry-run=client -o yaml
```

---

# 11. ServiceAccount and token commands

## 11.1 Create a service account

```bash
kubectl create serviceaccount app-sa
```

## 11.2 Generate a token for a service account

```bash
kubectl create token app-sa
```

## 11.3 Generate a time-limited token

```bash
kubectl create token app-sa --duration=10m
```

## 11.4 Use a service account in a Pod or Deployment

Usually easiest via YAML:

```yaml
spec:
  serviceAccountName: app-sa
```

**Exam tip:** create the service account imperatively, then generate the Pod/Deployment YAML and add `serviceAccountName` manually.

---

# 12. RBAC commands

Current CKA scope includes RBAC. You should know the fast commands below.

## 12.1 Create a Role

```bash
kubectl create role pod-reader \
  --verb=get --verb=list --verb=watch \
  --resource=pods -n dev
```

## 12.2 Create a ClusterRole

```bash
kubectl create clusterrole pod-reader \
  --verb=get,list,watch \
  --resource=pods
```

## 12.3 Create a RoleBinding

```bash
kubectl create rolebinding read-pods \
  --role=pod-reader \
  --serviceaccount=dev:app-sa \
  -n dev
```

## 12.4 Create a RoleBinding to a ClusterRole

```bash
kubectl create rolebinding read-view \
  --clusterrole=view \
  --serviceaccount=dev:app-sa \
  -n dev
```

## 12.5 Create a ClusterRoleBinding

```bash
kubectl create clusterrolebinding app-sa-view \
  --clusterrole=view \
  --serviceaccount=dev:app-sa
```

## 12.6 Check access fast

```bash
kubectl auth can-i create pods
kubectl auth can-i list deployments.apps
kubectl auth can-i get pods --as system:serviceaccount:dev:app-sa -n dev
```

**What it does:** lets you quickly test RBAC permissions.

---

# 13. Autoscaling commands

## 13.1 Create an HPA from a deployment

```bash
kubectl autoscale deployment web --cpu-percent=50 --min=1 --max=5
```

**What it does:** creates a HorizontalPodAutoscaler that targets average CPU utilization.

## 13.2 Generate HPA YAML

```bash
kubectl autoscale deployment web --cpu-percent=50 --min=1 --max=5 --dry-run=client -o yaml
```

**Note:** HPA behavior depends on metrics availability.

---

# 14. Label and annotation commands

## 14.1 Add a label

```bash
kubectl label pod nginx env=prod
```

## 14.2 Overwrite a label

```bash
kubectl label pod nginx env=prod --overwrite
```

## 14.3 Remove a label

```bash
kubectl label pod nginx env-
```

## 14.4 Add an annotation

```bash
kubectl annotate pod nginx owner=dipen
```

## 14.5 Remove an annotation

```bash
kubectl annotate pod nginx owner-
```

---

# 15. Quota, PDB, and PriorityClass commands

These are less frequent than Pods/Deployments/Services, but current `kubectl` supports them directly.

## 15.1 Create a ResourceQuota

```bash
kubectl create quota team-a-quota \
  --hard=pods=10,requests.cpu=2,requests.memory=4Gi,limits.cpu=4,limits.memory=8Gi \
  -n team-a
```

## 15.2 Create a PodDisruptionBudget

```bash
kubectl create poddisruptionbudget web-pdb \
  --selector=app=web \
  --min-available=1
```

## 15.3 Create a PriorityClass

```bash
kubectl create priorityclass high-priority \
  --value=1000000 \
  --global-default=false \
  --description="High priority workloads"
```

---

# 16. Fast inspection and troubleshooting commands

These commands are not all “imperative create” commands, but they are absolutely essential for CKA.

## 16.1 Get resources

```bash
kubectl get pods
kubectl get pods -A
kubectl get pods -o wide
kubectl get pods --show-labels
kubectl get svc,endpoints
kubectl get deploy,rs,po
kubectl get nodes -o wide
```

## 16.2 Get YAML for an existing object

```bash
kubectl get deploy web -o yaml
kubectl get pod nginx -o yaml
```

## 16.3 Use JSONPath for targeted output

```bash
kubectl get pod nginx -o jsonpath='{.spec.containers[*].image}'
kubectl get nodes -o jsonpath='{.items[*].metadata.name}'
```

## 16.4 Describe an object

```bash
kubectl describe pod nginx
kubectl describe node worker-1
kubectl describe svc web-svc
```

**Why it matters:** `describe` is one of the fastest ways to spot events, scheduling issues, image pull errors, port mismatches, taints, and selector problems.

## 16.5 Logs

```bash
kubectl logs nginx
kubectl logs -f nginx
kubectl logs nginx --previous
kubectl logs deploy/web
kubectl logs nginx -c sidecar
```

## 16.6 Execute a command inside a container

```bash
kubectl exec -it nginx -- sh
kubectl exec -it nginx -- /bin/bash
kubectl exec nginx -- env
```

## 16.7 Copy files to/from a container

```bash
kubectl cp file.txt nginx:/tmp/file.txt
kubectl cp nginx:/etc/nginx/nginx.conf ./nginx.conf
```

## 16.8 Port-forward

```bash
kubectl port-forward pod/nginx 8080:80
kubectl port-forward svc/web-svc 8080:80
```

## 16.9 Events

```bash
kubectl get events -A --sort-by=.metadata.creationTimestamp
kubectl events
```

## 16.10 Top

```bash
kubectl top nodes
kubectl top pods -A
```

**Note:** this needs metrics support in the cluster.

## 16.11 Explain object fields

```bash
kubectl explain pod
kubectl explain deployment.spec.template.spec
kubectl explain service.spec.ports
```

**Why it matters:** this is one of the best exam helpers when you forget field names.

## 16.12 API discovery

```bash
kubectl api-resources
kubectl api-versions
```

## 16.13 Wait for readiness

```bash
kubectl wait --for=condition=Ready pod/nginx --timeout=60s
kubectl wait --for=condition=available deployment/web --timeout=60s
```

## 16.14 Edit live resources

```bash
kubectl edit deployment web
kubectl edit svc web-svc
```

## 16.15 Replace a manifest

```bash
kubectl replace -f web.yaml
```

## 16.16 Delete objects quickly

```bash
kubectl delete pod nginx
kubectl delete deployment web
kubectl delete -f web.yaml
kubectl delete pod -l app=nginx
```

---

# 17. Node maintenance commands

These are frequently relevant in admin-style tasks.

## 17.1 Mark a node unschedulable

```bash
kubectl cordon worker-1
```

**What it does:** stops new Pods from being scheduled onto the node.

## 17.2 Mark it schedulable again

```bash
kubectl uncordon worker-1
```

## 17.3 Drain a node safely

```bash
kubectl drain worker-1 --ignore-daemonsets --delete-emptydir-data
```

**What it does:** evicts Pods and prepares the node for maintenance.

## 17.4 Taint a node

```bash
kubectl taint nodes worker-1 dedicated=infra:NoSchedule
```

## 17.5 Remove a taint

```bash
kubectl taint nodes worker-1 dedicated=infra:NoSchedule-
```

---

# 18. Debug commands

## 18.1 Debug a Pod with an ephemeral container

```bash
kubectl debug pod/nginx -it --image=busybox
```

## 18.2 Debug a specific target container

```bash
kubectl debug pod/nginx -it --image=busybox --target=nginx
```

## 18.3 Debug a node

```bash
kubectl debug node/worker-1 -it --image=busybox
```

**Use when:** normal `exec` is not enough or the workload container lacks debugging tools.

---

# 19. Context and cluster selection commands

These save you from working in the wrong cluster or namespace.

## 19.1 See current context

```bash
kubectl config current-context
```

## 19.2 List contexts

```bash
kubectl config get-contexts
```

## 19.3 Switch context

```bash
kubectl config use-context kubernetes-admin@cluster1
```

## 19.4 View kubeconfig

```bash
kubectl config view
```

**Exam note:** always confirm the context before solving a task.

---

# 20. High-yield YAML generation recipes

These are the ones worth memorizing exactly.

## 20.1 Pod YAML

```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml
```

## 20.2 Deployment YAML

```bash
kubectl create deployment web --image=nginx --replicas=3 --dry-run=client -o yaml > deploy.yaml
```

## 20.3 Service YAML

```bash
kubectl expose deployment web --port=80 --target-port=8080 --dry-run=client -o yaml > svc.yaml
```

## 20.4 Job YAML

```bash
kubectl create job my-job --image=busybox --dry-run=client -o yaml > job.yaml
```

## 20.5 CronJob YAML

```bash
kubectl create cronjob my-job --image=busybox --schedule="*/5 * * * *" --dry-run=client -o yaml > cronjob.yaml
```

## 20.6 ConfigMap YAML

```bash
kubectl create configmap app-config --from-literal=APP_ENV=prod --dry-run=client -o yaml > cm.yaml
```

## 20.7 Secret YAML

```bash
kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=pass123 --dry-run=client -o yaml > secret.yaml
```

## 20.8 Namespace YAML

```bash
kubectl create namespace dev --dry-run=client -o yaml > ns.yaml
```

---

# 21. Commands that are not pure imperative, but are still CKA-critical

The CKA is not only about creating Pods and Deployments. The current scope also includes cluster lifecycle, RBAC, troubleshooting, storage, and networking. These commands are high value even though they are not all “imperative object creation” commands.

## 21.1 kubeadm basics

### Initialize a cluster

```bash
kubeadm init
```

### Join a worker node

```bash
kubeadm join <control-plane-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### Print a join command from the control plane

```bash
kubeadm token create --print-join-command
```

### Reset a node

```bash
kubeadm reset
```

## 21.2 kubeadm certificate checks and renewal

```bash
kubeadm certs check-expiration
kubeadm certs renew all
```

## 21.3 etcd backup and restore

Set environment variables first:

```bash
export ETCDCTL_API=3
```

### Take a snapshot

```bash
etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /opt/etcd-backup.db
```

### Check snapshot status

```bash
etcdctl snapshot status /opt/etcd-backup.db
```

### Restore snapshot

```bash
etcdctl snapshot restore /opt/etcd-backup.db --data-dir=/var/lib/etcd-from-backup
```

**Important:** actual paths can vary by cluster setup. Always inspect the static pod manifest and existing cert paths first.

## 21.4 kubelet and node troubleshooting

```bash
systemctl status kubelet
systemctl restart kubelet
journalctl -u kubelet -xe
crictl ps -a
crictl logs <container-id>
```

---

# 22. What is especially worth practicing for the current CKA

Without pretending to know confidential live questions, these are the areas most worth drilling because they line up well with the current official CKA scope and current simulator-style prep:

## 22.1 Very high priority
- `kubectl run`
- `kubectl create deployment`
- `kubectl expose`
- `kubectl create configmap`
- `kubectl create secret`
- `kubectl create job`
- `kubectl create cronjob`
- `kubectl scale`
- `kubectl set image`
- `kubectl set env`
- `kubectl set resources`
- `kubectl rollout status/history/undo/restart`
- `kubectl get -o yaml`
- `kubectl describe`
- `kubectl logs`
- `kubectl exec`
- `kubectl explain`
- `kubectl auth can-i`
- `kubectl cordon / uncordon / drain`
- `kubectl taint`
- `kubectl config use-context`

## 22.2 Commonly useful
- `kubectl create ingress`
- `kubectl autoscale`
- `kubectl create serviceaccount`
- `kubectl create token`
- `kubectl create role`
- `kubectl create rolebinding`
- `kubectl create clusterrole`
- `kubectl create clusterrolebinding`
- `kubectl patch`
- `kubectl edit`
- `kubectl wait`
- `kubectl debug`

## 22.3 Worth knowing, but often faster with YAML
- NetworkPolicy
- affinity / anti-affinity
- tolerations
- probes
- PV / PVC
- securityContext
- Gateway API resources

---

# 23. Fast exam workflow examples

## Example 1: Create a Pod with a command and label

Task style:
Create a Pod named `bb` using `busybox`, run `sleep 3600`, and label it `app=debug`.

Fast way:

```bash
kubectl run bb --image=busybox --labels="app=debug" --command -- sleep 3600
```

If you need YAML:

```bash
kubectl run bb --image=busybox --labels="app=debug" --command -- sleep 3600 --dry-run=client -o yaml > bb.yaml
```

## Example 2: Create a Deployment, expose it, then scale it

```bash
kubectl create deployment web --image=nginx --replicas=2
kubectl expose deployment web --port=80 --target-port=80
kubectl scale deployment web --replicas=3
```

## Example 3: Create a Secret and mount/use it later

```bash
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=pass123 \
  --dry-run=client -o yaml > secret.yaml
```

Then edit workload YAML to reference the Secret.

## Example 4: Create a ServiceAccount and bind read-only access

```bash
kubectl create serviceaccount app-sa -n dev
kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods -n dev
kubectl create rolebinding read-pods --role=pod-reader --serviceaccount=dev:app-sa -n dev
kubectl auth can-i get pods --as system:serviceaccount:dev:app-sa -n dev
```

## Example 5: Create a CronJob fast

```bash
kubectl create cronjob backup --image=busybox --schedule="0 */6 * * *" -- sh -c 'date; echo backup'
```

## Example 6: Drain a node for maintenance

```bash
kubectl cordon worker-1
kubectl drain worker-1 --ignore-daemonsets --delete-emptydir-data
kubectl uncordon worker-1
```

---

# 24. Personal memorization shortlist

If you memorize only one compact set first, make it this:

```bash
# Namespaces
kubectl create namespace dev

# Pods
kubectl run nginx --image=nginx
kubectl run bb --image=busybox --command -- sleep 3600
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml

# Deployments
kubectl create deployment web --image=nginx
kubectl create deployment web --image=nginx --replicas=3 --dry-run=client -o yaml > deploy.yaml
kubectl scale deployment web --replicas=5
kubectl set image deployment/web nginx=nginx:1.28
kubectl rollout status deployment/web
kubectl rollout undo deployment/web

# Services
kubectl expose deployment web --port=80 --target-port=8080
kubectl expose deployment web --type=NodePort --port=80 --target-port=8080
kubectl create service clusterip web-svc --tcp=80:8080
kubectl create service nodeport web-svc --tcp=80:8080

# Config and secrets
kubectl create configmap app-config --from-literal=APP_ENV=prod
kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=pass123

# Jobs
kubectl create job my-job --image=busybox -- date
kubectl create cronjob my-job --image=busybox --schedule="*/5 * * * *" -- date

# RBAC
kubectl create serviceaccount app-sa
kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods -n dev
kubectl create rolebinding read-pods --role=pod-reader --serviceaccount=dev:app-sa -n dev
kubectl auth can-i get pods --as system:serviceaccount:dev:app-sa -n dev

# Troubleshooting
kubectl get pods -A -o wide
kubectl describe pod nginx
kubectl logs nginx --previous
kubectl exec -it nginx -- sh
kubectl explain deployment.spec.template.spec
kubectl get events -A --sort-by=.metadata.creationTimestamp

# Nodes
kubectl cordon worker-1
kubectl drain worker-1 --ignore-daemonsets --delete-emptydir-data
kubectl uncordon worker-1
kubectl taint nodes worker-1 dedicated=infra:NoSchedule

# Contexts
kubectl config current-context
kubectl config get-contexts
kubectl config use-context kubernetes-admin@cluster1
```

---

# 25. Final advice for CKA

1. Do not try to solve everything with one perfect imperative command.
2. Use imperative commands to get **80% of the object** quickly.
3. Use `--dry-run=client -o yaml` to generate the base manifest.
4. Use `kubectl explain` when field names slip from memory.
5. Verify after every task with `get`, `describe`, `logs`, or `rollout status`.
6. Always confirm the context before starting the task.
7. For current CKA prep, be strong not only in creation commands, but also in **RBAC, node maintenance, kubeadm, etcd backup/restore, and troubleshooting**.

