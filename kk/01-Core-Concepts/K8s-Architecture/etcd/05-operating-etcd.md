# Operating etcd (Admin Basics)

etcd usually runs as:
- A **static pod** on control plane nodes
- Or a **systemd service** (older setups)

---

## Common Location

```bash
/etc/kubernetes/manifests/etcd.yaml

etcdctl Basics

Set API version:

export ETCDCTL_API=3


Check cluster health:

etcdctl endpoint health


List all keys:

etcdctl get / --prefix --keys-only
