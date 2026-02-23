# FastAPI Beyond CRUD

This is the source code for the [FastAPI Beyond CRUD](https://youtube.com/playlist?list=PLEt8Tae2spYnHy378vMlPH--87cfeh33P&si=rl-08ktaRjcm2aIQ) course. The course focuses on FastAPI development concepts that go beyond the basic CRUD operations.

For more details, visit the project's [website](https://jod35.github.io/fastapi-beyond-crud-docs/site/).

## Table of Contents

1. [Getting Started](#getting-started)
2. [Prerequisites](#prerequisites)
3. [Project Setup](#project-setup)
4. [Running the Application](#running-the-application)
5. [GitHub Actions Workflows](#github-actions-workflows)
6. [Running Tests](#running-tests)
7. [How to Test a Failing Nightly Build](#how-to-test-a-failing-nightly-build)
8. [Contributing](#contributing)

## Getting Started

Follow the instructions below to set up and run the project.

## Prerequisites

Recommended (for this assignment):

- Docker Desktop
- Git

> This repo can also be run locally with Python/PostgreSQL/Redis, but the intended verification for this assignment is `docker compose up`.

## Project Setup

1. Clone the project repository:
   ```bash
   git clone https://github.com/jod35/fastapi-beyond-CRUD.git

2. Navigate to the project directory:
   ```bash
   cd fastapi-beyond-CRUD/
   ```

3. Copy the example environment variables file:
   ```bash
   cp .env.example .env
   ```

4. Fill the env file with your own values (example values are provided in the .env.example file)

## Running the Application

1. Start the application:
   ```bash
   docker compose up -build
   ```
### Verify the app is running

Open:
- `http://localhost:8000/api/v1/docs`

You can also test an endpoint:

```bash
curl http://localhost:8000/api/v1/books
```

## GitHub Actions Workflows

This repo includes two GitHub Actions workflows for the assignment.

### 1) PR Conventional Commit Enforcement

Workflow file:
- `.github/workflows/pr-conventional-commit.yml`

What it does:
- Validates PR titles using Conventional Commits (examples: `feat: ...`, `fix: ...`, `docs: ...`)
- Automatically closes PRs with invalid titles
- Adds a PR comment explaining why it was closed
- Sends an email notification on failure

### 2) Nightly Build and Container Push

Workflow file:
- `.github/workflows/nightly-build.yml`

What it does:
- Runs nightly from the default branch (and can also be run manually)
- Starts the project with `docker compose up -d --build`
- Verifies the API is healthy before continuing
- Builds and pushes a container image to GitHub Container Registry (GHCR)
- Sends an email notification if the nightly build fails

### Required GitHub Secrets

Set these in:

**Repo Settings → Secrets and variables → Actions**

- `MAIL_SERVER`
- `MAIL_PORT`
- `MAIL_USERNAME`
- `MAIL_PASSWORD`
- `MAIL_FROM`
- `MAIL_TO`

(Used for email notifications in both workflows.)

## Running Tests

If running locally without Docker, run tests with:

```bash
pytest
```
