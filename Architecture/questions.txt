1. How a Pod gets created in the background?

Kubectl sends request to kubeapi-server
API server validates + admission controlls
Object gets stored in the etcd
controller manager notices desired replicas and creats pods
pods are created but have no nodes --> pending
scheduler assigns a node 
Node's kubelet sees pods assigned to me
kubectl asks container runtime to pull images and runs containers
kubelet reports pod status back via API server
kube-proxy ensures services can route the traffic to the pod