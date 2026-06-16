# Health Probes

## Probe Types

| Probe | Trigger | Action on Failure |
|-------|---------|------------------|
| **Startup** | During startup only | Container restarted |
| **Liveness** | Throughout container lifetime | Container restarted |
| **Readiness** | Throughout container lifetime | Pod removed from Service endpoints |

## Probe Mechanisms

| Mechanism | Description |
|-----------|-------------|
| `httpGet` | HTTP GET request; success = 2xx/3xx |
| `tcpSocket` | TCP connection; success = connection established |
| `exec` | Command execution; success = exit code 0 |
| `grpc` | gRPC health check |

## Key Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `initialDelaySeconds` | Wait before first probe | 0 |
| `periodSeconds` | Time between probes | 10 |
| `timeoutSeconds` | Probe timeout | 1 |
| `failureThreshold` | Failures before action | 3 |
| `successThreshold` | Successes to be considered healthy | 1 |

## Files

| File | Description |
|------|-------------|
| `deployment-with-probes.yaml` | Startup + Liveness + Readiness probes (HTTP) |
| `tcp-probe-pod.yaml` | TCP socket probes on Redis |
| `exec-probe-pod.yaml` | Exec probe; fails after 30s (observe restart) |

## Exercises

```bash
# Deploy with all HTTP probes
kubectl apply -f deployment-with-probes.yaml
kubectl get pods
kubectl describe pod <pod-name>  # Check probe events

# Watch exec probe fail and trigger restart
kubectl apply -f exec-probe-pod.yaml
kubectl get pod exec-probe-pod -w    # Watch restarts after ~30s
kubectl describe pod exec-probe-pod  # Shows liveness probe failures

# TCP probe
kubectl apply -f tcp-probe-pod.yaml
kubectl describe pod tcp-probe-pod

# Cleanup
kubectl delete -f .
```
