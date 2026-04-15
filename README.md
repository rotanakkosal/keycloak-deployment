# Keycloak Deployment

Production-ready Keycloak identity and access management deployment with PostgreSQL, using Docker Compose.

## Prerequisites

- Docker and Docker Compose
- TLS certificates for your domain

## Quick Start

### 1. Configure environment variables

Copy the example environment file and fill in your values:

```bash
cp .env.example .env
```

Edit `.env` with your actual credentials and hostname. **Use strong, unique passwords in production.**

### 2. Add TLS certificates

Place your TLS certificate and private key in the `certs/` directory:

```
certs/
├── fullchain.pem   # Full certificate chain
└── privkey.pem     # Private key
```

### 3. Start the services

```bash
docker compose up -d
```

Keycloak will be available at:
- **HTTP:** http://localhost
- **HTTPS:** https://localhost (or your configured `KC_HOSTNAME`)

### 4. Check service health

```bash
docker compose ps
docker compose logs -f keycloak
```

## Configuration

All configuration is managed through the `.env` file. See `.env.example` for all available options.

| Variable | Description |
|---|---|
| `KEYCLOAK_ADMIN` | Admin console username |
| `KEYCLOAK_ADMIN_PASSWORD` | Admin console password |
| `KC_HOSTNAME` | Public hostname for Keycloak |
| `KC_FEATURES` | Comma-separated Keycloak features to enable |
| `POSTGRES_DB` | PostgreSQL database name |
| `POSTGRES_USER` | PostgreSQL username |
| `POSTGRES_PASSWORD` | PostgreSQL password |
| `POSTGRES_HOST_PORT` | Host port mapped to PostgreSQL |

## Production Checklist

- [ ] Set strong passwords in `.env`
- [ ] Use valid TLS certificates (not self-signed)
- [ ] Restrict the Postgres port (`POSTGRES_HOST_PORT`) or remove it from compose if not needed externally
- [ ] Set up regular database backups
- [ ] Review Keycloak's [production configuration guide](https://www.keycloak.org/server/configuration-production)
