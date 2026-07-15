# Module 11 - Calculation Model with SQLAlchemy, Pydantic, and Factory Pattern

A FastAPI application with a Calculation model built using SQLAlchemy, validated
with Pydantic schemas, and using the factory pattern to handle different
calculation types (Add, Subtract, Multiply, Divide). Includes unit and
integration tests and a CI/CD pipeline that deploys a Docker image to Docker Hub.

## Features

- SQLAlchemy `Calculation` model with fields for `a`, `b`, `type`, and `result`
- Factory pattern (`Calculation.create()`) to instantiate the correct calculation subclass
- Foreign key to the `User` model via `user_id`
- Pydantic schemas: `CalculationCreate` validates input (including no division by zero), `CalculationRead` serializes output
- Unit and integration tests (integration tests run against a real Postgres database)
- GitHub Actions CI/CD: runs all tests, then builds and pushes a Docker image to Docker Hub

## Running Tests Locally

1. Create and activate a virtual environment:

```bash
   python3 -m venv venv
   source venv/bin/activate
```

2. Install dependencies:

```bash
   pip install -r requirements.txt
   playwright install
```

3. Start a local Postgres database:

```bash
   docker-compose up -d
```

4. Set the database URL and run the tests:

```bash
   export DATABASE_URL=postgresql://user:password@localhost:5432/mytestdb
   pytest tests/unit/
   pytest tests/integration/
   pytest tests/e2e/
```

## Docker Hub

The Docker image is automatically built and pushed to Docker Hub by the CI/CD pipeline:

https://hub.docker.com/r/nr598/module11_is601

Pull and run the image:

```bash
docker pull nr598/module11_is601:latest
docker run -p 8000:8000 nr598/module11_is601:latest
```
