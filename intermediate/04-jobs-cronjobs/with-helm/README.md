# Jobs and CronJobs – with Helm

## Exercises

```bash
# Install (creates both a Job and a CronJob)
helm install my-jobs ./chart

# Disable the one-shot Job, keep CronJob
helm install my-jobs ./chart --set job.enabled=false

# Change cron schedule
helm upgrade my-jobs ./chart --set cronjob.schedule="0 * * * *"

# Cleanup
helm uninstall my-jobs
```
