# gRPC Microservices

A microservices architecture demo featuring gRPC communication, JWT authentication, and Prometheus monitoring.

## Services

| Service | Description | Stack |
|---------|-------------|-------|
| **[SSO](https://github.com/grpc-svc/sso)** | Authentication service with gRPC API | Go, gRPC, SQLite, JWT, Argon2 |
| **[URL Shortener](https://github.com/grpc-svc/url-shortener)** | URL shortening with auth integration | Go, Chi, gRPC client, SQLite, Prometheus |
| **[Infrastructure](https://github.com/grpc-svc/infra)** | Monitoring stack | Prometheus, Grafana, Docker Compose |
| **[Protos](https://github.com/grpc-svc/protos)** | Shared protocol buffer definitions | Protocol Buffers, gRPC, API contracts |

## Architecture

```
┌─────────────────┐       gRPC        ┌─────────────────┐
│  URL Shortener  │◄─────────────────►│       SSO       │
│   (HTTP API)    │                   │   (gRPC API)    │
└────────┬────────┘                   └────────┬────────┘
 │       │                                     │
 │       ▼                                     ▼
 │  ┌─────────┐                           ┌─────────┐
 │  │ SQLite  │                           │ SQLite  │
 │  └─────────┘                           └─────────┘
 │       
 ▼       
┌─────────────────┐       scrape      ┌─────────────────┐
│   Prometheus    │◄──────────────────│     Grafana     │
└─────────────────┘                   └─────────────────┘
```

## Features

- **SSO Service**: User registration, login, JWT token generation, admin role check
- **URL Shortener**: Create/delete short URLs, redirect, protected endpoints via JWT
- **Monitoring**: Request rate, error rate, latency percentiles (P50/P95/P99)

## Quick Start

```bash
# Start SSO service
cd sso && task run

# Start URL Shortener
cd url-shortener && task run

# Start monitoring
cd infra && docker-compose -f docker-compose.monitoring.yml up -d
```

## Tech Stack

- **Go 1.25** — core language
- **gRPC + Protobuf** — service communication ([protos](https://github.com/grpc-svc/protos))
- **Chi** — HTTP router
- **SQLite** — storage
- **Prometheus + Grafana** — observability
- **Taskfile** — task runner

## License

MIT
