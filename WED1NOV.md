<div align="center">

# WED 1 NOV

</div>
____________________________

## Tasks

# Table of Contents

1. [Kubernetes Session 2](#kubernetes-session-2)
   - [Root vs. Rootless Container](#root-vs-rootless-container)
   - [Dockerfile and Container File](#dockerfile-and-container-file)
   - [Explanation](#explanation)
   - [Container Best Practice](#container-best-practice)
   - [Persistent Volume (PV)](#persistent-volume-pv)
   - [Node](#node)
   - [Assigned Task](#assigned-task)

2. [Spreadsheet](#spreadsheet)
   - [Data Manipulation](#data-manipulation)

3. [KVM Troubleshooting Issues](#kvm-troubleshooting-issues)
   - [Analyzing Pre-flight Checks](#analyzing-pre-flight-checks)
   - [Attempted Solutions](#attempted-solutions)


___________________________

<div align="center">

## Kubernetes Session 2

|**Duration: 10:00-02:30**|**Day: Wednesday**|
|-------------------------|-|


![img](https://i.imgur.com/YDL5kxD.jpg)

</div>

**Root vs. Rootless Container**:
- Root vs. Rootless Container (Always use Rootless)
- Unsecure vs. Secure
- From Root vs. From Home

**Dockerfile and Container File**:
- Dockerfile = Container File (Container File is for Podman)
- Dockerfile has instructions like FROM, ADD, COPY, RUN, CMD, ENTRYPOINT (ALL CAPS)

**Explanation**:
- `FROM docker.io/library/ubuntu:latest` (Write the entire registry URL, good practice instead of `ubuntu:latest`)
- (For installation) `RUN yum install httpd -y` (httpd is Apache) (We can run multiple commands)
- `COPY code.tar /var/www/html`
- `ADD code.tar /var/www/html` (Will directly untar, same as `COPY`)
- `CMD apache -D foreground`
- Every `FROM`, `COPY`, etc., line is a different layer (line 1 = layer 2). The sequence of each layer is crucial.
- We can create the container in a Dockerfile from the normal container user, but we define a user inside the container.
- Dockerfile has some level of abstraction.
- `podman build -t himanshu-httpd:v1 .` (We add the image here).
- First, we get the OS, and then we install the Apache image.

**Container Best Practice**:
- One Container Should Have One Application (Good Practice) - But harsh sir said I can try for understanding - Otherwise, practically it's wrong.

**Persistent Volume (PV)**:
- `podman run -itd --name httpd -P <port>`
- Let's say I have `/var/log` as my log location, and I want to use it as the log in my container as well.
- Changes in persistent volume in the SE Linux: If "." is at the end of `ls -ld` under the first column of permission, then volume.
- `podman run -itd --name httpd -- -v/home/yash/logs -P 8080:httpd:latest` - Most important
- `podman logs <container>`
- `podman inspect` allows you to see everything about how a container was made, including the first `podman run` command.

**Node**:
- The node is just the virtual machine on which the container is running.

**Assigned Task**:
- Create an image of Ubuntu - might be done without a Dockerfile.
- Guided exercise.

-----------------------------------------

<div align="center">

## Spreadsheet 
</div>

**Data Manipulation**:
- changed column AU backup_url content - https://gitlab.com/checkpostApp2/backupconfig -> https://gitlab.com/checkpostApp2/backup.
- changed format of all dates in sheet from dd/mm/yy to dd-mm-yyyy.
- changed WWN address in row 2.
- added N/A to value of ax column backup_tested_date.
- to add document_tested_date b/w column o-p?
- changed col BA and made first row physical type to suit the data.
- changed col X "Haprox_Running" -> Haproxy_Running

<div align="center">

## KVM      
</div>

**Troubleshooting Issues**
> root@node:/home/imsnode/kubeadm-scripts# kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b 
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
[ERROR FileAvailable--etc-kubernetes-kubelet.conf]: /etc/kubernetes/kubelet.conf already exists
[ERROR Port-10250]: Port 10250 is in use
[ERROR FileAvailable--etc-kubernetes-pki-ca.crt]: /etc/kubernetes/pki/ca.crt already exists
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
root@node:/home/imsnode/kubeadm-scripts# 

- First I ran `netstat -aop | grep 10250` for fiding which port was already in use. Output showed that it was being used by kubelet: 
```
netstat -aop | grep 10250
tcp6    0    0 [::]:10250  [::]:*  LISTEN  676/kubelet off (0.00/0/0)
```
- All the other errors showed that the port 10250 for kubelt and ca.crt & kubelet.conf files were already existing. I decided to run this command with `--ignore-preflight-errors=` flag for exluding these errors:
```
**kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b --ignore-preflight-errors=FileAvailable--etc-kubernetes-kubelet.conf,Port-10250,FileAvailable--etc-kubernetes-pki-ca.crt**
kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b --ignore-preflight-errors=FileAvailable--etc-kubernetes-kubelet.conf,Port-10250,FileAvailable--etc-kubernetes-pki-ca.crt
[preflight] Running pre-flight checks
	[WARNING FileAvailable--etc-kubernetes-kubelet.conf]: /etc/kubernetes/kubelet.conf already exists
	[WARNING Port-10250]: Port 10250 is in use
	[WARNING FileAvailable--etc-kubernetes-pki-ca.crt]: /etc/kubernetes/pki/ca.crt already exists

```
- The second alternative thing that I did was run the same command with the verbose level --5 using the following command below. The output displayed the same errors with 
```
**kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b --v=5**
I1101 18:14:53.012719    6799 join.go:412] [preflight] found NodeName empty; using OS hostname as NodeName
I1101 18:14:53.013220    6799 initconfiguration.go:117] detected and using CRI socket: unix:///var/run/containerd/containerd.sock
[preflight] Running pre-flight checks
I1101 18:14:53.013418    6799 preflight.go:93] [preflight] Running general checks
I1101 18:14:53.013455    6799 checks.go:280] validating the existence of file /etc/kubernetes/kubelet.conf
I1101 18:14:53.013578    6799 checks.go:280] validating the existence of file /etc/kubernetes/bootstrap-kubelet.conf
I1101 18:14:53.013606    6799 checks.go:104] validating the container runtime
I1101 18:14:53.044923    6799 checks.go:639] validating whether swap is enabled or not
I1101 18:14:53.045089    6799 checks.go:370] validating the presence of executable crictl
I1101 18:14:53.045157    6799 checks.go:370] validating the presence of executable conntrack
I1101 18:14:53.045193    6799 checks.go:370] validating the presence of executable ip
I1101 18:14:53.045327    6799 checks.go:370] validating the presence of executable iptables
I1101 18:14:53.045398    6799 checks.go:370] validating the presence of executable mount
I1101 18:14:53.045467    6799 checks.go:370] validating the presence of executable nsenter
I1101 18:14:53.045551    6799 checks.go:370] validating the presence of executable ebtables
I1101 18:14:53.045614    6799 checks.go:370] validating the presence of executable ethtool
I1101 18:14:53.045673    6799 checks.go:370] validating the presence of executable socat
I1101 18:14:53.045735    6799 checks.go:370] validating the presence of executable tc
I1101 18:14:53.045766    6799 checks.go:370] validating the presence of executable touch
I1101 18:14:53.045870    6799 checks.go:516] running all checks
I1101 18:14:53.058342    6799 checks.go:401] checking whether the given node name is valid and reachable using net.LookupHost
I1101 18:14:53.059229    6799 checks.go:605] validating kubelet version
I1101 18:14:53.111424    6799 checks.go:130] validating if the "kubelet" service is enabled and active
I1101 18:14:53.121554    6799 checks.go:203] validating availability of port 10250
I1101 18:14:53.121751    6799 checks.go:280] validating the existence of file /etc/kubernetes/pki/ca.crt
I1101 18:14:53.121783    6799 checks.go:430] validating if the connectivity type is via proxy or direct
I1101 18:14:53.121820    6799 checks.go:329] validating the contents of file /proc/sys/net/bridge/bridge-nf-call-iptables
I1101 18:14:53.121857    6799 checks.go:329] validating the contents of file /proc/sys/net/ipv4/ip_forward
[preflight] Some fatal errors occurred:
	[ERROR FileAvailable--etc-kubernetes-kubelet.conf]: /etc/kubernetes/kubelet.conf already exists
	[ERROR Port-10250]: Port 10250 is in use
	[ERROR FileAvailable--etc-kubernetes-pki-ca.crt]: /etc/kubernetes/pki/ca.crt already exists
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
error execution phase preflight
k8s.io/kubernetes/cmd/kubeadm/app/cmd/phases/workflow.(*Runner).Run.func1
	cmd/kubeadm/app/cmd/phases/workflow/runner.go:260
k8s.io/kubernetes/cmd/kubeadm/app/cmd/phases/workflow.(*Runner).visitAll
	cmd/kubeadm/app/cmd/phases/workflow/runner.go:446
k8s.io/kubernetes/cmd/kubeadm/app/cmd/phases/workflow.(*Runner).Run
	cmd/kubeadm/app/cmd/phases/workflow/runner.go:232
k8s.io/kubernetes/cmd/kubeadm/app/cmd.newCmdJoin.func1
	cmd/kubeadm/app/cmd/join.go:179
github.com/spf13/cobra.(*Command).execute
	vendor/github.com/spf13/cobra/command.go:940
github.com/spf13/cobra.(*Command).ExecuteC
	vendor/github.com/spf13/cobra/command.go:1068
github.com/spf13/cobra.(*Command).Execute
	vendor/github.com/spf13/cobra/command.go:992
k8s.io/kubernetes/cmd/kubeadm/app.Run
	cmd/kubeadm/app/kubeadm.go:50
main.main
	cmd/kubeadm/kubeadm.go:25
runtime.main
	/usr/local/go/src/runtime/proc.go:250
runtime.goexit
	/usr/local/go/src/runtime/asm_amd64.s:1598
```

- To solve this issue, I tried removing the existing files and port. This was done using the following commands:
```
sudo systemctl stop kubelet
sudo rm /etc/kubernetes/kubelet.conf
sudo rm /etc/kubernetes/pki/ca.crt
```

- Once I had done that, I ran the kubeadm join command again but I was still unable to solve this issue:
```
**kubeadm join 192.168.122.12:6443 --token 3e24gr.522ahym3cdm75zcg --discovery-token-ca-cert-hash sha256:4a4782da4051cfd0521b8cf9a260b02345c3388c57a5feb740452efd3a2cd85b**
[preflight] Running pre-flight checks
error execution phase preflight: couldn't validate the identity of the API Server: Get "https://192.168.122.12:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s": dial tcp 192.168.122.12:6443: connect: connection refused
To see the stack trace of this error execute with --v=5 or higher
root@node:/home/imsnode/Desktop# 
```
