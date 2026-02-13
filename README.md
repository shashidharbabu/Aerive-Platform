# Aerive Platform

Aerive is a microservices-based travel booking platform with a React frontend, an API gateway, and dedicated services for users, listings, bookings, billing, providers, and admin workflows. The platform uses MongoDB for core data, PostgreSQL for billing, Kafka for event-driven communication, and Redis for caching.

## Architecture

- Frontend: React + Vite + Tailwind CSS
- API Gateway: Routes and aggregates requests
- Services: User, Listing, Booking, Billing, Provider, Admin
- Eventing: Kafka topics for inter-service events
- Data: MongoDB (core), PostgreSQL (billing), Redis (cache)

## Repository Layout

- `frontend/`: React app
- `services/`: Node.js microservices
- `shared/`: Shared config, models, middleware, utils
- `infrastructure/`: Kubernetes and Postgres bootstrap
- `docker-compose.yml`: Local Kafka, Redis, Postgres

## Prerequisites

- Node.js 18+ and npm
- Docker Desktop (for Kafka/Redis/Postgres)
- MongoDB (local or Atlas)

## Quick Start (Local)

1) Install dependencies

```bash
npm run install:all
cd frontend && npm install
```

2) Start supporting services

```bash
docker-compose up -d
```

3) Configure environment variables

Set these in your shell or service-level `.env` files:

```bash
# Core data
MONGODB_URI=mongodb://localhost:27017/aerive

# Kafka
KAFKA_BROKERS=localhost:9092
KAFKA_CLIENT_ID=aerive-backend

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=

# PostgreSQL (billing)
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=aerive_billing
POSTGRES_USER=aerive
POSTGRES_PASSWORD=aerive123
POSTGRES_SSL=false
```

4) Run backend services

```bash
npm run dev
```

5) Run frontend

```bash
cd frontend
npm run dev
```

## Useful Scripts

From the repo root:

- `npm run dev`: Start all backend services concurrently
- `npm run dev:user|listing|booking|billing|provider|admin|gateway`: Start a single service
- `npm run build`: Build all backend services

From `frontend/`:

- `npm run dev`: Start the React app
- `npm run build`: Build frontend for production
- `npm run preview`: Preview production build

## Infrastructure

Kubernetes manifests are under `infrastructure/kubernetes/`. The Postgres init script lives at `infrastructure/postgres/init.sql` and is mounted by `docker-compose.yml` for local development.

## Notes

- Kafka and Redis are expected to be running before starting services.
- MongoDB is not included in `docker-compose.yml`; use a local instance or Atlas.

## License

MIT