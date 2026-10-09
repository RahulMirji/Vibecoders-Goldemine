# Stateless Scaling Checklist

Use this before running your app on multiple servers.

## Pre-deployment checklist

### Sessions and authentication
- [ ] Server-side sessions are stored in shared storage (e.g. Redis) OR properly validated signed tokens are used where appropriate.
- [ ] Session revocation strategy is considered and handled.

### File uploads
- [ ] Uploads are stored in object storage (e.g. S3, Google Cloud Storage), not on the local disk of any server instance.

### In-memory state
- [ ] Important user state, shared counters, and background-job status have been moved out of process memory.
- [ ] Ephemeral UI state is acceptable to remain in-memory.

### Caching
- [ ] Local/disposable caches are identified.
- [ ] Shared caches are used when consistency across servers matters.

### Rate limiting
- [ ] Rate limits apply across all instances using a shared counter store when needed.

### Background jobs
- [ ] Jobs are enqueued in a shared queue.
- [ ] Jobs are idempotent and safe to retry without duplicating side effects.

### Database
- [ ] Persistent data lives in a shared database.
- [ ] Connection pooling is configured with sensible limits.
- [ ] Migrations are safe and reproducible.

### Configuration and secrets
- [ ] Config and secrets are loaded consistently across all instances.
- [ ] Secrets are never committed to source control.
- [ ] Secrets are never logged.

### Health checks
- [ ] Readiness and liveness endpoints are exposed.
- [ ] Unhealthy instances can be removed from the load balancer.

### Production reliability
- [ ] Shared-store failures are accounted for (timeouts, retries, circuit breakers).
- [ ] Backups, monitoring, and alerting are in place.
- [ ] Graceful shutdown and recovery paths are tested.

## Copy-paste AI prompt

Use this in Claude Code, Cursor, Antigravity, or your preferred coding agent.

```text
Act as a senior backend engineer performing a production-readiness audit.

Review my codebase for issues that could break when running two or more application server instances behind a load balancer.

Tasks:
1. Identify server-side sessions stored in process memory and propose shared session storage or a suitable token-based alternative.
2. Find local file uploads, in-memory user state, shared counters, caches and job status that could cause inconsistent behavior across instances.
3. Check rate limiting, background jobs, scheduled tasks, WebSockets and any other instance-specific state.
4. Verify database connection handling, configuration consistency, secrets management and health checks.
5. Identify dependencies on shared services, including Redis, and explain their failure modes.
6. Recommend the smallest safe set of changes for multi-instance deployment.

Constraints:
- Inspect the existing architecture before suggesting changes.
- Do not rewrite unrelated code or assume Redis is always required.
- Preserve existing authentication and authorization behavior.
- Never expose secrets or log session tokens.
- Include appropriate tests for multiple instances, session persistence, failure handling and retries.

Output:
- Findings ranked Critical / High / Medium / Low
- File paths and relevant code references
- Recommended fixes and their trade-offs
- Implementation plan ordered by priority
- Tests required before deployment

Do not modify files until I approve the implementation plan.
```

## Key reminders

- Stateless doesn't mean no state. It means application instances don't depend on their own local memory to handle requests correctly.
- Redis isn't automatically highly available. If sessions depend on Redis, plan for its availability, security, monitoring, and recovery.
- JWTs can reduce the need for server-side session lookups in some architectures, but revocation, token expiry, and authorization still need careful design.

**Recommended workflow:** Run the audit prompt first, review the findings, then implement and test the changes before deploying a second instance.
