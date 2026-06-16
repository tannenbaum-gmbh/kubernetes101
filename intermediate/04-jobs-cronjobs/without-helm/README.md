# Jobs and CronJobs

## Concepts

| Resource | Description |
|----------|-------------|
| **Job** | Runs a Pod to completion; ensures a specified number of successful completions |
| **CronJob** | Creates Jobs on a scheduled (cron) basis |

## Job Patterns

| Pattern | `completions` | `parallelism` |
|---------|--------------|---------------|
| Single run | 1 | 1 |
| Fixed task queue | N | 1 |
| Parallel fixed | N | M |
| Work queue | - | M |

## Concurrency Policies (CronJob)

| Policy | Description |
|--------|-------------|
| `Allow` | Multiple concurrent Job runs allowed |
| `Forbid` | Skip new run if previous is still running |
| `Replace` | Cancel running Job, start new one |

## Exercises

```bash
# Run a Job
kubectl apply -f job.yaml
kubectl get jobs
kubectl get pods
kubectl logs -l job-name=pi-calculator

# Parallel Job
kubectl apply -f parallel-job.yaml
kubectl get jobs -w   # Watch completions

# CronJob
kubectl apply -f cronjob.yaml
kubectl get cronjobs

# Manually trigger a CronJob
kubectl create job --from=cronjob/backup-job manual-backup

# Watch created Jobs
kubectl get jobs -w

# Cleanup
kubectl delete -f .
```
