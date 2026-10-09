# IT373 Practical Test — Secure Docker Deployment

## Live Websites

**Production:** https://it373-sathvik.duckdns.org

**QA:** https://qa-it373-sathvik.duckdns.org

**GitHub Repository:** https://github.com/Sathvik-Alla/it373-practical-test

## Project Overview

This project demonstrates deploying a Dockerized HTML website to a DigitalOcean Ubuntu server using GitHub Actions CI/CD.

The website is served by Nginx inside Docker containers, with Caddy acting as a reverse proxy to provide HTTPS access.

## Technologies Used

- DigitalOcean Ubuntu 24.04
- Docker and Nginx
- GitHub Actions
- GitHub Container Registry (GHCR)
- Caddy reverse proxy
- DuckDNS
- Git and GitHub

## Deployment Environments

| Environment | Git Branch | Internal Port |
|---|---|---|
| Production | `main` | `127.0.0.1:8081` |
| QA | `qa` | `127.0.0.1:8082` |

The environments run in separate Docker containers so that changes to QA do not automatically change production.

## CI/CD Pipeline

When code is pushed to the `main` or `qa` branch, GitHub Actions:

1. Checks out the repository.
2. Validates the website files.
3. Builds and tests the Docker image.
4. Pushes the image to GitHub Container Registry.
5. Connects to the DigitalOcean server using SSH.
6. Deploys the image to the corresponding environment.

GitHub Actions runs: https://github.com/Sathvik-Alla/it373-practical-test/actions

## Server Security

The Ubuntu server uses a non-root deployment account with SSH public-key authentication. Root SSH login and password-based SSH authentication are disabled.

UFW allows SSH, HTTP, and HTTPS traffic. Docker containers expose their application ports only on the server's loopback interface. Caddy handles public HTTPS traffic and forwards requests to the appropriate container.

## Deployment Verification

Both QA and production have been verified running their respective GHCR images in separate Docker containers. The production and QA websites are accessible using their HTTPS domains.

## Evidence

Screenshots documenting SSH hardening, Docker container status, successful GitHub Actions workflows, and both live websites can be added to an `evidence/` directory.

## Author

NJIT — IT373 Practical Test
