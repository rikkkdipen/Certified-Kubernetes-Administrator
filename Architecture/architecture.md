Kubernetes has a distributed architecture having master and worker nodes

1. Master Node - This decides what should run and where it should run
2. Worker Node - This actually runs the app

Master Node Components [Brain]
    
    a. KubeAPI Server - whichever commands we run using kubectl goes here.

    b. etcd - this is a database which stores data in key:value format.

    c. scheduler - this chooses which node should run the new pod.

    d. controller-manager - this keeps checking the state of the nodes and fixes if anything breaks.

Worker Node Components [Muscle]
    
    a. kubelet - this is the agent which talks to the control plane or the brain and runs the pods.

    b. container runtime - this actually starts the container eg: docker, containerd.

    c. kube-proxy - this handles the services, networking/load-balancing.

    d. pods - these are the smallest deployable units, The container runs inside this pods.

Networking + Access
   
    a. CNI plugin - this provides pod to pod network.

    b. Service - this gives virtual IP/DNS for the pods.

    c. CoreDNS - internal DNS.

    d. Ingress - This allows (HTTP/HTTPS) entry from outside


Flow
- user runs "Kubectl apply deployment.yml" --> API server stores that in etcd --> scheduler then picks the worker node --> kubelet starts the pod on that node --> controller-manager keeps it healthy and replaces it if necessary

reference: [Kubernetes Documentation](https://kubernetes.io/docs/concepts/architecture/)