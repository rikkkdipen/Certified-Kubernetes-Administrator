# Why Kubernetes Uses etcd

Kubernetes needs a storage system that provides:

- Strong consistency
- High availability
- Fast reads and writes
- Distributed safety

etcd provides all of this.

---

## Distributed and Consistent

etcd uses the **RAFT consensus algorithm**.

This means:
- Multiple etcd nodes agree before data is written
- One leader, multiple followers
- Data is always consistent across the cluster

---

## Why not a normal database?

Traditional databases:
- Are heavier
- Slower for metadata operations
- Not designed for distributed consensus

etcd is purpose-built for **cluster state management**.

