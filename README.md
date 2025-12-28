# DartAppClean – Full Stack Application
The backend project was generated using the [Clean.Architecture.Solution.Template](https://github.com/jasontaylordev/CleanArchitecture) version 9.0.12.


[![.NET](https://img.shields.io/badge/.NET-9-512BD4?logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13-336791?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-007ACC?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![SignalR](https://img.shields.io/badge/SignalR-ASP.NET-512BD4?logo=asp.net&logoColor=white)](https://dotnet.microsoft.com/apps/aspnet/signalr)
[![Docker](https://img.shields.io/badge/Docker-Blue-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)


* **Backend:** ASP.NET 8 API using Clean Architecture and Domain-Driven Design
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

Clone the orchestration repository:

```bash
git clone https://github.com/majkusi/DartAppClean.Local.git
cd DartAppClean.Local
```

```bash
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
| backend  | ASP.NET 8 API (Clean Architecture + DDD + SignalR Hubs) | 8080 |
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

* Reset database:

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

* **CORS & SignalR:** Configured for Docker networking in development
* **HTTPS:** Disabled for local development
* **Data Persistence:** PostgreSQL uses a Docker volume `pgdata`
* **Clean Architecture:** Backend follows DDD principles with separate layers
* **Hot Reload:** Frontend runs in development mode with live reload


---

## License

MIT License
