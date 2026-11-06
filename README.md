# Marketplace Infrastructure

This repository contains the master Docker Compose configuration for the Marketplace microservices.

## Repository structure

The following repositories must be cloned into the same parent directory:

```text
marketplace/
├── marketplace-infra/
├── api-gateway-module/
├── auth-module/
│   └── secrets/
│       ├── private_key.pem
│       └── public_key.pem
└── user-module/
```

## Configuration

1. Copy `.env.example` to `.env`.
2. Set the required database passwords and admin credentials.
3. Generate the RSA key pair as described in the Auth Service README and place the files in `auth-module/secrets/`.

## Start the application

Run the following commands from the `marketplace-infra` directory:

```bash
docker compose pull
docker compose up -d
```

To check the running containers:

```bash
docker compose ps
```

To stop the application:

```bash
docker compose down
```

The API Gateway is available at `http://localhost:8080`.
