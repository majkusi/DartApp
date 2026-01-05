# DartApp – Full Stack Application
The backend project was generated using the [Clean.Architecture.Solution.Template](https://github.com/jasontaylordev/CleanArchitecture) version 9.0.12.

## ⚠️ IMPORTANT NOTICE

**Currently this application won’t work due to MediatR being licensed.  
The whole match component is based on MediatR hubs.**

**This is a simple learning project that allows to play a game of classic 501 darts game. The scoring system is based on inputting a sum of thrown points (similar to how tournaments look like)**
  
[![.NET](https://img.shields.io/badge/.NET-9-white?logo=dotnet&logoColor=white&color=512BD4&style=flat)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13-white?logo=postgresql&logoColor=white&color=336791&style=flat)](https://www.postgresql.org/)
[![React](https://img.shields.io/badge/React-18-white?logo=react&logoColor=black&color=61DAFB&style=flat)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-white?logo=typescript&logoColor=white&color=007ACC&style=flat)](https://www.typescriptlang.org/)
[![SignalR](https://img.shields.io/badge/SignalR-ASP.NET-white?logo=asp.net&logoColor=white&color=512BD4&style=flat)](https://dotnet.microsoft.com/apps/aspnet/signalr)
[![Docker](https://img.shields.io/badge/Docker-Blue-white?logo=docker&logoColor=white&color=2496ED&style=flat)](https://www.docker.com/)


* **Backend:** ASP.NET 9 API using Clean Architecture and Domain-Driven Design
* **Database:** PostgreSQL
* **Frontend:** React + TypeScript
* **Real-time updates:** SignalR Hubs

---

## Table of Contents

1. Prerequisites
2. Getting Started
3. Project Structure
4. Docker Services
5. Development Workflow
6. Frontend / Backend URLs
7. Additional Notes
8. License

---

## Prerequisites

* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install/)
* Git

---

## Getting Started

Clone the orchestration repository and update submodules:

```bash
git clone https://github.com/majkusi/DartApp.git
cd DartApp
git submodule update --init --recursive
```

Start all services:

```bash
docker compose up --build
```

---

## Project Structure

```
DartAppClean.Local/
├── docker-compose.yml        # Orchestration for backend, frontend, and DB
├── README.md                 
├── backend/                  # ASP.NET Clean Architecture backend (module)
│   ├── Dockerfile
│   └── src/
├── frontend/                 # React + TypeScript frontend (module)
│   ├── Dockerfile
│   └── src/
```

---

## Docker Services

| Service  | Description                                             | Port |
| -------- | ------------------------------------------------------- | ---- |
| postgres | PostgreSQL database for backend                         | 5432 |
| backend  | ASP.NET 9 API (Clean Architecture + DDD + SignalR Hubs) | 8080 |
| frontend | React + TypeScript frontend with hot-reload             | 5173 |

---

## Environment Variables

### Backend (Docker Compose)

```yaml
environment:
  ASPNETCORE_ENVIRONMENT: Development
  ASPNETCORE_URLS: http://+:8080
  ConnectionStrings__DefaultConnection: Host=postgres;Port=5432;Database=dartapp;Username=dartapp;Password=dartapp
```

### Frontend (.env)

```env
VITE_API_URL=http://backend:8080
```

---

## Development Workflow

* Start services:

```bash
docker compose up --build
```

* Stop services:

```bash
docker compose down
```

* Reset docker:

```bash
docker compose down -v
docker compose up --build
```

* Run EF Core migrations manually:

```bash
docker compose exec backend dotnet ef database update
```

---

## Frontend / Backend URLs

| Service  | URL                                                          |
| -------- | ------------------------------------------------------------ |
| Frontend | [http://localhost:5173](http://localhost:5173)               |
| Backend  | [http://localhost:8080](http://localhost:8080)               |
| Swagger  | [http://localhost:8080/api](http://localhost:8080/api)       |
| Health   | [http://localhost:8080/health](http://localhost:8080/health) |
| SignalR  | ws://localhost:8080/api/hubs/match                           |

---

## Additional Notes

* Database credentials are for local development only and are not used in production.
* Login and register feature is currently added but only for backend, no "login" state is kept on frontend. Login and Register forms works but are not fully functional.

* **CORS & SignalR:** Configured for Docker networking in development
* **HTTPS:** Disabled for local development
* **Data Persistence:** PostgreSQL uses a Docker volume `pgdata`
* **Clean Architecture:** Backend follows DDD principles with separate layers

---

## License

MIT License
