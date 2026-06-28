# vikunja-compose

Git-ops Docker Compose project for deploying [Vikunja](https://vikunja.io), a task management application.

## Prerequisites

- Portainer with webhook support enabled
- Traefik running as the reverse proxy (on network `traefik_default`)

## Quick Start

1. Clone this repository to Portainer as a new stack.
2. Configure Portainer to deploy from the `deploy` branch.
3. Configure environment variables in Portainer.

## Environment Variables

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `SERVICE_IMAGE` | The Vikunja docker image | Yes | `ghcr.io/korjavin/vikunja-vendor:latest` |
| `POSTGRES_IMAGE` | The Postgres docker image | Yes | `postgres:16-alpine` |
| `SERVICE_CONTAINER_NAME` | Name for Vikunja container | No | `vikunja` |
| `DB_CONTAINER_NAME` | Name for Postgres container | No | `vikunja-db` |
| `TRAEFIK_NETWORK_NAME` | Traefik external network | Yes | `traefik_default` |
| `INTERNAL_NETWORK_NAME` | Internal network name | No | `vikunja_internal` |
| `DB_VOLUME_NAME` | Volume for Postgres data | No | `vikunja_db-data` |
| `DATA_PATH` | Path for Vikunja files | No | `./files` |
| `SERVICE_HOST` | Hostname for Traefik routing | Yes | `vikunja.yourdomain.com` |
| `TRAEFIK_CERTRESOLVER` | Traefik cert resolver | Yes | `myresolver` |
| `VIKUNJA_SERVICE_PUBLICURL` | Public URL of the service | Yes | `https://vikunja.yourdomain.com` |
| `VIKUNJA_SERVICE_SECRET` | Vikunja secret key | Yes | Generate with `openssl rand -hex 32` |
| `POSTGRES_DB` | Database name | Yes | `vikunja` |
| `POSTGRES_USER` | Database user | Yes | `vikunja` |
| `POSTGRES_PASSWORD` | Database password | Yes | Set to a secure password |

## Portainer Setup

1. In Portainer, create a new Stack using a repository.
2. Repository URL: `https://github.com/korjavin/vikunja-compose`
3. Branch: `deploy` (IMPORTANT: not `master`)
4. Compose path: `docker-compose.yml`
5. Enable "Git Repository updates" and copy the Webhook URL.
6. Set all environment variables above.
7. Deploy the stack.

## GitHub Secrets

To enable automated deployments on push, add the following GitHub secret:
- `PORTAINER_REDEPLOY_HOOK`: The webhook URL copied from Portainer.
