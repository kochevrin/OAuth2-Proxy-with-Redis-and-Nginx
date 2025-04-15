# OAuth2 Proxy with Redis and Nginx

This repository contains a Dockerized setup for an OAuth2 Proxy using Redis as the session store and Nginx for redirects. The setup allows you to securely authenticate users via an OpenID Connect (OIDC) provider.

## Features

- OAuth2 Proxy for handling authentication.
- Redis for session storage.
- Nginx for redirecting requests.
- Fully configurable with environment variables.

## Getting Started

### Prerequisites

- Docker and Docker Compose installed on your machine.

### Setup Instructions

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo-name.git
   cd your-repo-name
   ```

2. Copy the example configuration files and customize them:
   ```bash
   cp .env.example .env
   cp nginx.conf.example nginx.conf
   ```
   - Update `.env` with your own values. For example:
     - Replace `your-client-id`, `your-client-secret`, and `your-tenant-id` with your OIDC provider credentials.
     - Replace `your-cookie-secret` with a secure generated secret (see below for the command).
     - Replace `your.domain.com` with your application's domain.
   - Update `nginx.conf` if needed.

3. Generate a secure cookie secret:
   ```bash
   openssl rand -base64 32 | head -c 32
   ```
   Copy the output and set it as the value for `OAUTH2_PROXY_COOKIE_SECRET` in your `.env` file.

4. Start the services:
   ```bash
   docker-compose up -d
   ```

5. Stop the services:
   ```bash
   docker-compose down
   ```

### File Descriptions

- `.env.example`: Contains the environment variables needed for the setup.
- `nginx.conf.example`: Nginx configuration for handling redirects.
- `docker-compose.yaml`: Docker Compose file for defining and running the services.

### Environment Variables

Below are the key environment variables you need to configure in your `.env` file:

| Variable                      | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| `REDIS_IMAGE`                 | Redis Docker image version.                                                |
| `OAUTH2_PROXY_IMAGE`          | OAuth2 Proxy Docker image version.                                         |
| `NGINX_IMAGE`                 | Nginx Docker image version.                                                |
| `OAUTH2_PROXY_PROVIDER`       | OAuth2 provider (e.g., `oidc`).                                            |
| `OAUTH2_PROXY_CLIENT_ID`      | Client ID from your OIDC provider.                                         |
| `OAUTH2_PROXY_CLIENT_SECRET`  | Client Secret from your OIDC provider.                                     |
| `OAUTH2_PROXY_COOKIE_SECRET`  | Secure cookie secret.                                                      |
| `OAUTH2_PROXY_REDIRECT_URL`   | Redirect URL for the OAuth2 callback.                                      |
| `OAUTH2_PROXY_OIDC_ISSUER_URL`| OIDC issuer URL from your provider.                                        |
| `OAUTH2_PROXY_UPSTREAMS`      | Upstream services for authenticated users.                                 |

### Project Structure

```
.
├── .env.example          # Example environment configuration file
├── nginx.conf.example    # Example Nginx configuration file
├── docker-compose.yaml   # Docker Compose configuration
```

## Commands Reference

- **Generate Cookie Secret**:
  ```bash
  openssl rand -base64 32 | head -c 32
  ```
- **Start Services**:
  ```bash
  docker-compose up -d
  ```
- **Stop Services**:
  ```bash
  docker-compose down
  ```

## Author

This project is created and maintained by [kochevrin](https://github.com/kochevrin).