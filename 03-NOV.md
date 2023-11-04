# Kubernetes and Openshift Notes

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

## Load Balancing

- Achieving load balancing using the least balancing algorithm.

## Connecting Pods

- Connect pods within Openshift/Kubernetes using services.
- Use container names instead of IPs for representation.
- Command for viewing pod logs: `oc logs -f <pod name>`.
- Events are like logs that provide a story of what happened.

## Deployment Best Practice

- Always perform deployments from YAML for traceability.

## Kubernetes Installation

- Create a Kubernetes cluster on your system from Rancher to join the next class.

