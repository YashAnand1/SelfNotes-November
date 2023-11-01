<div align="center">

# MON 1 NOV

## Kubernetes Session 2

|**Duration: 10:00-02:30**|**Day: Wednesday**|
|-------------------------|-|
</div>



<div align="center">

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

- First I ran `netstat -aop | grep 10250` for fiding which port was already in use. Output: 
```

```
