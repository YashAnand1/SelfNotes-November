<div align="center">

# 03 November, 2023
**Day: Friday**

____________________________

## Tasks
</div>

- [Kubernetes Session 3](#kubernetes-session-3)

|**Duration: 10:30-05:30**|
|-------------------------|

<div align="center">

# Kubernetes Session 3
</div>

## Container Management

- Understand container push, pull, and Docker operations using DO-188.
- Pods are used to provide shared network environments and can run multiple containers.

## YAML Configuration

- Key elements of YAML configurations:
  - API version of Kubernetes/Openshift.
  - Kind (object type: deployment, pod, etc.).
  - Labels for differentiation.
  - Unique names.
  - Container image specification.
  - Node (physical or virtual machine).
  - Image pull policy (defines image behavior).

## Sequence of YAML

- Services: Cluster IP, Node Port, and LoadBalancer.
- One deployment typically corresponds to one task.

## Services and Pods

- Deployments create pods.
- Each application has its service.
- Service maintains pod IPs and handles traffic.
- Service does load balancing.
- Services also connect different pods within Openshift.
- Achieving load balancing using the least balancing algorithm.

## Connecting Pods

- Connect pods within Openshift/Kubernetes using services.
- Use container names instead of IPs for representation.
- Command for viewing pod logs: `oc logs -f <pod name>`.
- Events are like logs that provide a story of what happened.
- Always perform deployments from YAML for traceability.

## Assigned Tasks
- From rancher, setup kubernetes.

## Self-Learning
- Referred to this [YouTube tutorial](https://www.youtube.com/watch?v=uBgMbO0c9a4) and tried to set up Rancher on my Host machine.
- Was unable to connect with the Web UI even after creating the cotainerised images.
- Then I created the containers in a VM and through this method, I was able to set up rancher on my system.
- I then proceeded with logging into rancher. The codes utilised for this were as follows:
```
docker run --priveleged -d --restart=unless-stopped -p 80:80 -p 443:443  rancher/rancher
docker logs <containerid> 2>&1 | grep "Bootstrap Password:"
OPEN IN BROWSER: https://<serverIP>
``` 
