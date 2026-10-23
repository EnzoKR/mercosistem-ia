---
platform: software-house
format: deploy-checklist
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Deployment Checklist and Runbook

## Core Principles

Deployments should be boring. A well-defined checklist eliminates cognitive load, reduces human error, and makes rollback a fast, practiced operation — not a panic.

- **Never deploy on Fridays.** Changes need observation time; deploy when the full team is available to respond.
- **Every deploy is a risk.** Mitigate it with incremental rollouts, feature flags, and observability.
- **Runbook first.** If a deployment procedure is not written down, it does not exist reliably.

## Pre-Deployment Checklist

### Code and Build
- [ ] All CI/CD pipeline checks passing (tests, linting, type checks, security scans)
- [ ] PR reviewed and approved by at least one other engineer
- [ ] Branch merged from up-to-date main/trunk
- [ ] CHANGELOG updated with changes and version bump
- [ ] No debug code, `console.log`, or temporary hacks remaining

### Database and Data
- [ ] Database migrations reviewed (are they reversible?)
- [ ] Migration tested against a production-like dataset
- [ ] No destructive schema changes without a data backup
- [ ] Migration execution plan documented (run before or after deploy?)

### Configuration and Secrets
- [ ] All required environment variables set in target environment
- [ ] No secrets committed to the repository
- [ ] Third-party service credentials (API keys) valid and tested
- [ ] Feature flags configured for the target environment

### Rollback Plan
- [ ] Rollback procedure documented: commands to revert deploy
- [ ] Database rollback: is the migration reversible? If not, is there a compensating migration?
- [ ] Rollback tested in staging (at minimum, the steps are verified as correct)
- [ ] Team knows who is responsible for executing a rollback

## Deployment Execution

### During Deploy
- [ ] Announce deploy start in the team communication channel
- [ ] Monitor error rate and latency in real-time during rollout
- [ ] Watch for new errors in the error tracking tool (Sentry, Datadog, etc.)
- [ ] Pause or abort if error rate increases more than 5% above baseline

### Post-Deployment Verification
- [ ] Smoke test: manually verify the core user flow in production
- [ ] Automated synthetic monitor alerts not triggered
- [ ] Key metrics returning to expected values (conversion, error rate, latency p95)
- [ ] Any affected external integrations verified (webhooks, third-party services)
- [ ] Announce deploy completion in the team channel

## Rollback Procedure

```bash
# Example rollback procedure for a containerized app
# Step 1: Identify the last stable image tag
docker image ls <image-name>

# Step 2: Redeploy the previous version
kubectl set image deployment/<app> app=<image>:<previous-tag>

# Step 3: Monitor rollout
kubectl rollout status deployment/<app>

# Step 4: If database migration was run, execute rollback migration
npm run migrate:down  # or equivalent

# Step 5: Verify system health post-rollback
# Run smoke tests and confirm error rate normalized
```

## Production Incident Response

If a critical issue is discovered post-deploy:

1. **Declare incident** — notify on-call and team channel immediately
2. **Assess severity** — data loss? Revenue impact? % of users affected?
3. **Rollback or hotfix** — default to rollback; hotfix only if rollback is slower or riskier
4. **Communicate** — status page update within 5 minutes of a confirmed incident
5. **Post-mortem** — within 48 hours: timeline, root cause, action items (blameless)

## Deployment Frequency and Strategy

| Risk Level | Strategy | Observation Period |
|-----------|----------|--------------------|
| Low (config change) | Direct deploy | 15 minutes |
| Medium (new feature) | Canary rollout (5% → 20% → 100%) | 30 minutes per step |
| High (data migration) | Blue/green with verification step | 2+ hours |
| Critical (auth, payments) | Maintenance window, staged rollout | Full business day |
