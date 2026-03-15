# Deployment

## Environments

| Environment | Purpose | Access |
|---|---|---|
| **Development** | Local developer machines | Developers only |
| **Staging** | Integration testing, QA, demo | Team + selected testers |
| **Production** | Live service | Public |

---

## Prerequisites

- Docker 24+ and Docker Compose v2+ (for local / single-node)
- Kubernetes 1.28+ and Helm 3.14+ (for production)
- PostgreSQL 15+
- Redis 7+
- A domain name with DNS control
- A valid TLS certificate (auto-provisioned via cert-manager + Let's Encrypt in production)

---

## Local Development (Docker Compose)

1. **Clone the repository and copy environment template**

   ```bash
   git clone https://github.com/amilos/d3.git
   cd d3
   cp .env.example .env
   # Edit .env to fill in secrets
   ```

2. **Start all services**

   ```bash
   docker compose up --build
   ```

   This starts:
   - `api` — Core Service on port 3000
   - `identity` — Identity Service on port 3001
   - `db` — PostgreSQL on port 5432
   - `cache` — Redis on port 6379

3. **Run database migrations**

   ```bash
   docker compose exec api npx prisma migrate dev
   ```

4. **Seed demo data (optional)**

   ```bash
   docker compose exec api npx prisma db seed
   ```

5. **Access the API**

   ```
   http://localhost:3000/api/v1
   ```

---

## Production Deployment (Kubernetes + Helm)

### Infrastructure Overview

```
Internet
   │
   ▼
[Load Balancer]
   │
   ▼
[Ingress Controller (nginx)]
   │
   ├── /api          → Core Service (Deployment, HPA)
   ├── /auth         → Identity Service (Deployment)
   └── /audit        → Audit Log Service (StatefulSet)
                          │
                 ┌────────┴────────┐
                 ▼                 ▼
          [PostgreSQL        [Redis Cluster]
           (StatefulSet)]
```

### Step-by-Step

1. **Create a namespace**

   ```bash
   kubectl create namespace d3
   ```

2. **Install cert-manager** (if not already present)

   ```bash
   helm repo add jetstack https://charts.jetstack.io
   helm install cert-manager jetstack/cert-manager \
     --namespace cert-manager --create-namespace \
     --set crds.enabled=true
   ```

3. **Configure secrets**

   ```bash
   kubectl create secret generic d3-secrets \
     --namespace d3 \
     --from-literal=DATABASE_URL="postgresql://..." \
     --from-literal=JWT_PRIVATE_KEY="$(cat private.pem)" \
     --from-literal=JWT_PUBLIC_KEY="$(cat public.pem)" \
     --from-literal=REDIS_URL="redis://..."
   ```

4. **Deploy with Helm**

   ```bash
   helm repo add d3 https://charts.d3.example.com
   helm install d3 d3/d3 \
     --namespace d3 \
     --values production-values.yaml
   ```

5. **Run migrations**

   ```bash
   kubectl run --rm -it migrate \
     --image=ghcr.io/amilos/d3-api:latest \
     --namespace d3 \
     --restart=Never \
     -- npx prisma migrate deploy
   ```

6. **Verify rollout**

   ```bash
   kubectl rollout status deployment/d3-api -n d3
   kubectl rollout status deployment/d3-identity -n d3
   ```

---

## Configuration Reference

All services are configured via environment variables.

| Variable | Service | Description |
|---|---|---|
| `DATABASE_URL` | api, identity | PostgreSQL connection string |
| `REDIS_URL` | api | Redis connection string |
| `JWT_PRIVATE_KEY` | identity | RS256 private key (PEM, base64-encoded) |
| `JWT_PUBLIC_KEY` | api | RS256 public key (PEM, base64-encoded) |
| `JWT_ACCESS_EXPIRES_IN` | identity | Access token lifetime (default: `900s`) |
| `JWT_REFRESH_EXPIRES_IN` | identity | Refresh token lifetime (default: `30d`) |
| `PORT` | api, identity | HTTP listen port (default: `3000`) |
| `LOG_LEVEL` | all | `error`, `warn`, `info`, `debug` (default: `info`) |
| `CORS_ORIGINS` | api | Comma-separated list of allowed CORS origins |

---

## Health Checks

Each service exposes:

| Endpoint | Method | Description |
|---|---|---|
| `/health/live` | GET | Liveness probe — returns 200 if the process is running |
| `/health/ready` | GET | Readiness probe — returns 200 if DB and Redis are reachable |

---

## Scaling

The Core Service is stateless and can be scaled horizontally:

```bash
kubectl scale deployment d3-api --replicas=5 -n d3
```

A Horizontal Pod Autoscaler (HPA) is configured by default to scale between 2 and 10 replicas based on CPU utilisation (target: 60%).

---

## Backup and Recovery

- PostgreSQL is backed up daily using `pg_dump` to an encrypted S3-compatible object store.
- Backups are retained for 30 days.
- A recovery drill must be performed at least once per quarter.
- Recovery Time Objective (RTO): 4 hours. Recovery Point Objective (RPO): 24 hours.

---

## CI/CD Pipeline

| Stage | Tool | Trigger |
|---|---|---|
| Lint & type-check | ESLint, TypeScript | Every push |
| Unit tests | Jest | Every push |
| Integration tests | Jest + test DB | Every push to `main` or PR |
| SAST | CodeQL | Every push |
| Container build | Docker Buildx | Merge to `main` |
| Staging deploy | Helm | Merge to `main` |
| Production deploy | Helm (manual approval) | Git tag `v*.*.*` |
