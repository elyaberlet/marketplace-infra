# Marketplace Infrastructure

This repository contains the master Docker Compose configuration for the Marketplace microservices.

## Repository structure

The following repositories must be cloned into the same parent directory:

```text
marketplace/
├── marketplace-infra/
│   ├── docker-compose.yml
│   ├── .env.example
│   └── README.md
├── api-gateway-module/
├── auth-module/
│   └── secrets/
│       ├── private_key.pem
│       └── public_key.pem
├── user-module/
└── order-module/
    ├── Dockerfile
    ├── pom.xml
    └── src/
```

## Configuration

1. Copy `.env.example` to `.env`.
2. Set the required database passwords and admin credentials.
3. Configure Order Service database credentials:
    - `ORDER_DB_USERNAME`
    - `ORDER_DB_PASSWORD`
4. Generate the RSA key pair as described in the Auth Service README and place the files in `auth-module/secrets/`.

The `.env` file must not be committed to the repository.

## Start the application

Run the following commands from the `marketplace-infra` directory:

```bash
docker compose pull
docker compose up -d --build
```

The Order Service image is built locally using the Dockerfile from the `order-module` repository.

Other services are pulled from GitHub Container Registry.

## Check running containers

```bash
docker compose ps
```

## View service logs

```bash
docker compose logs -f order-service
```

To view logs of all services:

```bash
docker compose logs -f
```

## Stop the application

```bash
docker compose down
```

To remove containers and networks while preserving database volumes:

```bash
docker compose down
```

Database data is stored in named Docker volumes.

## Service access

- API Gateway: `http://localhost:8080`
- Order Service: available internally through the Docker network
- Order PostgreSQL: `localhost:5434` for local development

The API Gateway is the public entry point to the Marketplace application.