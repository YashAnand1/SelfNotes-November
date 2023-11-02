<div align="center">

# THURS 2 NOV

|**Reached: 09:24**|**Left: 07:45**|
|-------------------------|-|

## KVM

## **Recap**
- I was able to resolve the following errors yesterday:
```
**kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b**
[WARNING FileAvailable--etc-kubernetes-kubelet.conf]: /etc/kubernetes/kubelet.conf already exists
[WARNING Port-10250]: Port 10250 is in use
[WARNING FileAvailable--etc-kubernetes-pki-ca.crt]: /etc/kubernetes/pki/ca.crt already exists
```

- The error being faced right now from the Worker VM is: 
```
**kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b**
[preflight] Running pre-flight checks
error execution phase preflight: couldn't validate the identity of the API Server: Get "https://192.168.122.12:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s": dial tcp 192.168.122.12:6443: connect: connection refused

```
- Believing that maybe there had been an issue during the set-up, I restored the snapshots of the 2 Master and Worker VMs back to their fresh-install. 
- **For setting up the Master VM, I ran the following commands**:
Copying the Kubeadm scripts from Hetzner to Master VM:

```
**scp -r kubeadm-scripts/ ims-master@192.168.122.111:/home/ims-master**
```

- Installing kubemaster in Master VM:
```
**In Master VM: bash kubemaster-installation.sh**
kubelet kubeadm kubectl installed
```

- Running the additional commands on Master VM, starting with pulling kubeadm config images:
```
**kubeadm config images pull**
[config/images] Pulled registry.k8s.io/kube-apiserver:v1.28.3
[config/images] Pulled registry.k8s.io/kube-controller-manager:v1.28.3
[config/images] Pulled registry.k8s.io/kube-scheduler:v1.28.3
[config/images] Pulled registry.k8s.io/kube-proxy:v1.28.3
[config/images] Pulled registry.k8s.io/pause:3.9
[config/images] Pulled registry.k8s.io/etcd:3.5.9-0
[config/images] Pulled registry.k8s.io/coredns/coredns:v1.10.1
```

- Then I initialised the kubeadm service as root:
```
**kubeadm init**
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.122.111:6443 --token 8ffubv.6zaclg89o16ljnm3 \
	--discovery-token-ca-cert-hash sha256:0221bfe25b828649354c5a09c13a23089427df2da74005bbe0317e7a29264dbd 
```

- As stated previously, the output of previous command gave me the connection token that was to be entered from the worker node as well as the the following commands for start using a cluster were to be run on Master VM as normal user:
```
  **mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config**
```

- However, I got the 'connection refused' error if I ran these commands as a non-root as it had been explained in the output of kubeadm init. Then I logged in again as a root user into the Master VM for start using the cluster as a root user from the previous commands and the following ones as well:
```
**export KUBECONFIG=/etc/kubernetes/admin.conf**
```

- For being able to deploy a pod network to my cluster, I finally ran the following command with the syntax of "kubectl apply -f [podnetwork].yaml" with one of the options listed at "https://kubernetes.io/docs/concepts/cluster-administration/addons/":
```
**kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml**
Error from server (Timeout): error when retrieving current configuration of:
Resource: "/v1, Resource=serviceaccounts", GroupVersionKind: "/v1, Kind=ServiceAccount"
Name: "weave-net", Namespace: "kube-system"
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": the server was unable to return a response in the time allotted, but may still be processing the request (get serviceaccounts weave-net)
error when retrieving current configuration of:
Resource: "rbac.authorization.k8s.io/v1, Resource=clusterroles", GroupVersionKind: "rbac.authorization.k8s.io/v1, Kind=ClusterRole"
Name: "weave-net", Namespace: ""
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": Get "https://192.168.122.12:6443/apis/rbac.authorization.k8s.io/v1/clusterroles/weave-net": net/http: TLS handshake timeout - error from a previous attempt: http2: server sent GOAWAY and closed the connection; LastStreamID=9, ErrCode=NO_ERROR, debug=""
error when retrieving current configuration of:
Resource: "rbac.authorization.k8s.io/v1, Resource=clusterrolebindings", GroupVersionKind: "rbac.authorization.k8s.io/v1, Kind=ClusterRoleBinding"
Name: "weave-net", Namespace: ""
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": Get "https://192.168.122.12:6443/apis/rbac.authorization.k8s.io/v1/clusterrolebindings/weave-net": dial tcp 192.168.122.12:6443: connect: connection refused - error from a previous attempt: read tcp 192.168.122.12:38276->192.168.122.12:6443: read: connection reset by peer
error when retrieving current configuration of:
Resource: "rbac.authorization.k8s.io/v1, Resource=roles", GroupVersionKind: "rbac.authorization.k8s.io/v1, Kind=Role"
Name: "weave-net", Namespace: "kube-system"
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": Get "https://192.168.122.12:6443/apis/rbac.authorization.k8s.io/v1/namespaces/kube-system/roles/weave-net": dial tcp 192.168.122.12:6443: connect: connection refused
error when retrieving current configuration of:
Resource: "rbac.authorization.k8s.io/v1, Resource=rolebindings", GroupVersionKind: "rbac.authorization.k8s.io/v1, Kind=RoleBinding"
Name: "weave-net", Namespace: "kube-system"
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": Get "https://192.168.122.12:6443/apis/rbac.authorization.k8s.io/v1/namespaces/kube-system/rolebindings/weave-net": dial tcp 192.168.122.12:6443: connect: connection refused
error when retrieving current configuration of:
Resource: "apps/v1, Resource=daemonsets", GroupVersionKind: "apps/v1, Kind=DaemonSet"
Name: "weave-net", Namespace: "kube-system"
from server for: "https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml": Get "https://192.168.122.12:6443/apis/apps/v1/namespaces/kube-system/daemonsets/weave-net": dial tcp 192.168.122.12:6443: connect: connection refused
```

- I rolledback to the previous state again and ran the kubemaster installation script while being on a different wifi network and when I ran the command provided above, I got the following output:
```
**kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml**
serviceaccount/weave-net created
clusterrole.rbac.authorization.k8s.io/weave-net created
clusterrolebinding.rbac.authorization.k8s.io/weave-net created
role.rbac.authorization.k8s.io/weave-net created
rolebinding.rbac.authorization.k8s.io/weave-net created
daemonset.apps/weave-net created
```

- In order to ensure everything was working, I ran the command provided below, which helped me understand that the kubelet service was running. However, some error messages in the log incdicte issues with connecting to the Kubernetes API server on the address 192.168.122.111:6443 while giving "connection refused errors":
```
**systemctl status kubelet**
 kubelet.service - kubelet: The Kubernetes Node Agent
     Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor preset: enabled)
    Drop-In: /etc/systemd/system/kubelet.service.d
             \u2514\u250010-kubeadm.conf
     Active: active (running) since Thu 2023-11-02 12:54:36 IST; 5min ago
       Docs: https://kubernetes.io/docs/home/
   Main PID: 2357 (kubelet)
      Tasks: 11 (limit: 3468)
     Memory: 45.2M
        CPU: 8.407s
     CGroup: /system.slice/kubelet.service
             \u2514\u25002357 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/bootstrap-kubelet.conf --kubeconfig=/etc/kubernetes/kubelet.conf --config=/var/lib/kubelet/config.yaml --container-runtime-endpoint=unix:///var/run/containerd/containerd.sock --pod-infra-container-image=registry.k8s.io/pause:3.9

Nov 02 12:59:07 master kubelet[2357]: E1102 12:59:07.333378    2357 kubelet_node_status.go:540] "Error updating node status, will retry" err="error getting node \"master\": Get \"https://192.168.122.111:6443/api/v1/nodes/master?timeout=10s\": dial tcp 192.168.122.111:6443: connect: connection refused"
Nov 02 12:59:07 master kubelet[2357]: E1102 12:59:07.333651    2357 kubelet_node_status.go:540] "Error updating node status, will retry" err="error getting node \"master\": Get \"https://192.168.122.111:6443/api/v1/nodes/master?timeout=10s\": dial tcp 192.168.122.111:6443: connect: connection refused"
Nov 02 12:59:07 master kubelet[2357]: E1102 12:59:07.333866    2357 kubelet_node_status.go:540] "Error updating node status, will retry" err="error getting node \"master\": Get \"https://192.168.122.111:6443/api/v1/nodes/master?timeout=10s\": dial tcp 192.168.122.111:6443: connect: connection refused"
Nov 02 12:59:07 master kubelet[2357]: E1102 12:59:07.334193    2357 kubelet_node_status.go:540] "Error updating node status, will retry" err="error getting node \"master\": Get \"https://192.168.122.111:6443/api/v1/nodes/master?timeout=10s\": dial tcp 192.168.122.111:6443: connect: connection refused"
Nov 02 12:59:07 master kubelet[2357]: E1102 12:59:07.334231    2357 kubelet_node_status.go:527] "Unable to update node status" err="update node status exceeds retry count"
Nov 02 12:59:09 master kubelet[2357]: E1102 12:59:09.582243    2357 controller.go:146] "Failed to ensure lease exists, will retry" err="Get \"https://192.168.122.111:6443/apis/coordination.k8s.io/v1/namespaces/kube-node-lease/leases/master?timeout=10s\": dial tcp 192.168.122.111:6443: connect: connection refused" interval="7s"
Nov 02 12:59:13 master kubelet[2357]: I1102 12:59:13.148252    2357 scope.go:117] "RemoveContainer" containerID="114f9b0f1729f6b493f516188b8b4c6da707a999c4d069e82448cc41d4febe48"
Nov 02 12:59:14 master kubelet[2357]: I1102 12:59:14.148611    2357 scope.go:117] "RemoveContainer" containerID="ecc8c9eb01a7f7916fbe279e4d001106670dd5898a4e319c4728cc43ca604d92"
Nov 02 12:59:14 master kubelet[2357]: E1102 12:59:14.149196    2357 pod_workers.go:1300] "Error syncing pod, skipping" err="failed to \"StartContainer\" for \"kube-controller-manager\" with CrashLoopBackOff: \"back-off 40s restarting failed container=kube-controller-manager pod=kube-controller-manager-master_kube-system(f1a02ffb8f3c38c888cedb75ccbdb598)\"" pod="kube-system/kube-controller-manager-master" podUID="f1a02ffb8f3c38c888cedb75ccbdb598"
Nov 02 12:59:27 master kubelet[2357]: I1102 12:59:27.153923    2357 scope.go:117] "RemoveContainer" containerID="ecc8c9eb01a7f7916fbe279e4d001106670dd5898a4e319c4728cc43ca604d92"
```
- **For setting up the Master VM, I ran the following commands**:
- From the Hetzner Server, I first ran the following command for copying the kubeadm scripts to the Node machine:
```
**scp -r kubeadm-scripts ims-node@192.168.122.246:/home/ims-node**
```

- I decided to also resetup the IMS-NODE machine by running the following script on the Node machine from the kubeadm-scripts directory:
```
**bash node.sh**
```

- Once the setup had been done, I tried to connect the Node VM with the Master VM into the cluster using the following command:
```
**kubeadm join 192.168.122.111:6443 --token 8ffubv.6zaclg89o16ljnm3 \
	--discovery-token-ca-cert-hash sha256:0221bfe25b828649354c5a09c13a23089427df2da74005bbe0317e7a29264dbd** 

[preflight] Running pre-flight checks
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -o yaml'
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...
[kubelet-check] Initial timeout of 40s passed.

Unfortunately, an error has occurred:
	timed out waiting for the condition

This error is likely caused by:
	- The kubelet is not running
	- The kubelet is unhealthy due to a misconfiguration of the node in some way (required cgroups disabled)

If you are on a systemd-powered system, you can try to troubleshoot the error with the following commands:
	- 'systemctl status kubelet'
	- 'journalctl -xeu kubelet'
error execution phase kubelet-start: timed out waiting for the condition
To see the stack trace of this error execute with --v=5 or higher
```
