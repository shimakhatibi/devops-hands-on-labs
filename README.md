# devops-labs
# Kubernetes Workload Resources

Hands-on Kubernetes labs covering Deployment update strategies and different workload resources.

## Topics

### Deployment and Rolling Update

Practiced rolling updates using `maxSurge` and `maxUnavailable` and observed how Kubernetes gradually replaces old Pods with new ones.

### StatefulSet

Created a StatefulSet with three replicas and observed stable Pod identities such as `nginx-0`, `nginx-1`, and `nginx-2`. Deleted a Pod and verified that Kubernetes recreated it with the same identity.

### DaemonSet

Created a DaemonSet and observed that Kubernetes maintains one Pod on each eligible Node.

### Job

Created a Job that runs a command once and reaches the `Completed` state after successful execution.

### CronJob

Created a CronJob with a scheduled execution and observed that it creates Jobs according to the defined schedule.

## Key Concepts

- Rolling Update
- maxSurge
- maxUnavailable
- StatefulSet
- DaemonSet
- Job
- CronJob
- Pod lifecycle
# Kubernetes Lab — Deployment & Probes

## Topics

- Deployment
- ReplicaSet
- Pod
- Readiness Probe
- Liveness Probe

## What I Practiced

Created an Nginx Deployment with 3 replicas.

Tested Pod self-healing by deleting a Pod and observing ReplicaSet creating a replacement Pod.

Tested Readiness Probe by using an invalid HTTP path and observed that the Pod remained Running but was not Ready.

Tested Liveness Probe and observed container restarts when the health check failed.

## Commands

```bash
kubectl apply -f deployment.yaml
kubectl get deployment
kubectl get rs
kubectl get pods
kubectl describe deployment nginx
kubectl rollout status deployment nginx
