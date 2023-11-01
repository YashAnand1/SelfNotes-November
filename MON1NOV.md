<div allign="center">

# MON 1 NOV

## Kubernetes Session 2 10:00-02:30
## 1Nov - Wed - Session 2
## Check this image from blackboard for reference: 
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
- One Container Should Have One Application (Good Practice) - But you can try for understanding - Otherwise, it's wrong.

**Persistent Volume (PV)**:
- `podman run -itd --name httpd -P 9-9-"9-`
- Let's say I have `/var/log` as my log location, and I want to use it as the log in my container as well.
- Changes in persistent volume in the SE Linux: If "." is at the end of `ls -ld` under the first column of permission, then volume.
- `podman run -itd --name httpd -- -v/home/yash/logs -P 8080:httpd:latest`
- `podman logs <container>`
- `podman inspect` allows you to see everything about how a container was made, including the first `podman run` command.

**Node**:
- The node is just the virtual machine on which the container is running.

**Assigned Task**:
- Create an image of Ubuntu - might be done without a Dockerfile.
- Guided exercise.
