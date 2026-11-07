# AP Self-Storage

**Self-hosted personal cloud storage platform.**

AP Self-Storage is a project focused on building a personal cloud storage platform from the ground up. The goal is to provide a self-hosted alternative to commercial cloud storage services, allowing individuals to store, manage, and access their files using infrastructure they control.

The project is designed around independent micro-services, containerized application deployments, and automated infrastructure management.

> **Project status: Early development.** The foundational authentication service and local database infrastructure are under development. The platform is not yet ready for production use.

---

## Project Goals

- **Self-hosted:** Run the platform on personally owned infrastructure.
- **Privacy and ownership:** Keep personal files and data under the owner's control.
- **Modular architecture:** Build independently deployable services with clearly defined responsibilities.
- **Cross-platform:** Support installations and access across Windows, macOS, and Linux.
- **Automated deployment:** Use CI/CD to build, publish, and deploy application updates.
- **Open source:** Allow anyone to fork the project and maintain their own independent installation.

## Architecture

The platform follows a modular, service-oriented architecture.

Each service is maintained in its own GitHub repository and is intended to be independently developed, deployed, and maintained.

The initial architecture is built around the following principles:

- Application services communicate through defined APIs.
- Each installation represents one personal instance, intended for a single owner.
- There is no planned public registration, invitation system, or multi-tenant architecture.
- The initial administrator account is provisioned locally during installation or setup.
- Services are containerized to simplify deployment and portability.
- Persistent data is managed independently of application containers.

### Planned Infrastructure

The production environment is intended to run on an Ubuntu Server (MacOS and Windows support in the future).

| Component | Planned implementation |
|---|---|
| Operating system | Ubuntu Server LTS |
| Application services | Docker containers |
| Database | Native PostgreSQL installation |
| External connectivity | Cloudflare Tunnel |
| CI | GitHub Actions |
| Container registry | GitHub Container Registry |
| Deployment | Pull-based automated deployment |
| Application backend | Python and FastAPI |

PostgreSQL will run natively on the host rather than inside a container. Application services will connect to it through a configurable database connection.

Cloudflare Tunnel is intended to provide external connectivity without requiring traditional port forwarding.

## Repository Structure

Each repository represents an individual component of the platform.

| Repository | Responsibility | Status |
|---|---|---|
| `ap-auth-service` | Authentication and identity management | <img src="" alt=""/> In development |
| Additional services | To be defined as development progresses | Planned |

See the individual repositories for implementation details, dependencies, and development documentation.

## Authentication Service

The first component under development is `ap-auth-service`.

It is being built with:

- Python 3.12+
- FastAPI
- PostgreSQL
- SQLAlchemy
- Psycopg 3
- Pydantic Settings
- Argon2id for password hashing
- JWT for authentication tokens

### Intended functionality

- Authenticate users against PostgreSQL.
- Securely hash and verify passwords using Argon2id.
- Issue JWT access tokens.
- Support refresh-token rotation and revocation.
- Provide authentication mechanisms for other platform services.
- Restrict account provisioning to the local administrator.

### Current implementation status

**Completed:**
- Initial FastAPI application.
- Health-check and root endpoints.
- Authentication router structure.
- Pydantic login request model.
- Environment-based database configuration.
- SQLAlchemy engine and PostgreSQL connectivity.
- SQLAlchemy declarative base.
- Initial User database model.
- Local PostgreSQL development environment using Docker Compose.
- Initial `users` table created and verified in PostgreSQL.

**In progress:**
- Manual administrator account provisioning.
- Database queries for user lookup.
- Password hashing and verification.
- Functional login endpoint.
- JWT issuance and validation.

**Not yet implemented:**
- Refresh-token lifecycle.
- Token revocation.
- Production deployment configuration.
- Automated CI/CD pipeline.

## Development and Deployment Strategy

Development and production environments have different database configurations.

**Development**
- PostgreSQL runs locally through Docker Compose.
- Application services run in a Python virtual environment during development.
- Database models and queries are developed and tested locally.

**Production**
- PostgreSQL is installed natively on the Ubuntu host.
- Application services run as Docker containers.
- Installation scripts provision the database, users, permissions, and application configuration.
- CI/CD builds and publishes application images.
- The home server periodically checks for new releases and pulls updated images.

Database schema versioning and automated migrations will be introduced in a later development stage.

## Development Roadmap

| Phase | Objective | Status |
|---|---|---|
| 1 | Project architecture and repository organization | In progress |
| 2 | Authentication service foundation | In progress |
| 3 | Functional authentication and database operations | Pending |
| 4 | Application containerization | Pending |
| 5 | Ubuntu server preparation and installation scripts | Pending |
| 6 | CI/CD and automated deployment | Pending |
| 7 | Core file storage service | Pending |
| 8 | File management and access APIs | Pending |
| 9 | Cross-platform client access | Pending |
| 10 | Security hardening and production readiness | Pending |


## Disclaimer

This project is under active development and is not currently intended for production use. Features, architecture, and implementation details may change as development progresses.
