# devops-labs
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
