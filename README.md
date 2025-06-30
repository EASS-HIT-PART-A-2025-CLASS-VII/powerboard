# ⚡ PowerBoard

> A modern, real-time project and task management platform — built for teams who value clarity, collaboration, and a beautiful user experience.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)  [![React](https://img.shields.io/badge/React-18-blue.svg)](https://reactjs.org/)  [![FastAPI](https://img.shields.io/badge/FastAPI-0.104-green.svg)](https://fastapi.tiangolo.com/)  [![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)  [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)  [![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)

**Live Demo:** https://powerboard.up.railway.app

## Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Setup](#environment-setup)
  - [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Usage Guide](#usage-guide)
- [Development](#development)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About the Project

**PowerBoard** is a full-stack project and task management platform built for developers and teams that need structured workflows, real-time collaboration, and visual clarity.

Inspired by tools like Jira and Linear, it includes a modern Kanban board, analytics dashboards, notification system, user roles, and optional AI-powered task breakdowns — all packed into a sleek glassmorphism UI and powered by a microservice backend.

### Architecture Overview


```
┌─────────────────┐     ┌───────────┐     ┌─────────────────┐     ┌───────────────────┐     ┌─────────────────┐
│   React Frontend│◄──► │   Auth0   │◄──► │      Nginx      │◄──► │  FastAPI Backend  │◄──► │   PostgreSQL    │
│   (TypeScript)  │     │ (Identity │     │ (Reverse Proxy) │     │ (Main Gateway)    │     │   (Database)    │
│                 │     │ Provider) │     │                 │     │                   │     │                 │
└─────────────────┘     └───────────┘     └─────────────────┘     └───────────────────┘     └─────────────────┘
                                                 │                       │
                                                 │                       │
                                                 │                ┌──────┴───────┐
                                                 │                │ Microservices│
                                                 │                └──────┬───────┘
                                                 │                       │
                                                 │         ┌─────────────┴───────────────────────────────────────────────────────────────┐
                                                 │         │                                                                             │
                                                 │   ┌───────────┐  ┌───────────┐  ┌─────────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐
                                                 ├──►│ AI Service│  │ Analytics │  │ Notification│  │  Project  │  │ Realtime  │  │ Scheduler │
                                                 │   │ (OpenAI/  │  │  Service  │  │   Service   │  │  Service  │  │  Gateway  │  │  Service  │
                                                 │   │ Gemini)   │  │           │  │             │  │           │  │           │  │           │
                                                 │   └───────────┘  └───────────┘  └─────────────┘  └───────────┘  └───────────┘  └───────────┘
                                                 │                                  
                                                 │                                
                                                 │                        ┌───────────┐
                                                 └───────────────────────►│ User      │
                                                                          │ Service   │
                                                                          └───────────┘

```

**Key Design Principles:**

- **Microservices Architecture** – Modular backend with isolated services for projects, tasks, users, analytics, notifications, real-time gateway, scheduler, and AI suggestions
- **Real-Time Collaboration** – Live updates via WebSocket gateway for drag & drop, comments, and notifications across connected clients
- **AI-Assisted Workflow (Optional)** – Generate subtasks and effort estimates using OpenAI integration
- **Glassmorphism UI Design** – Modern dark-themed frontend with floating panels, smooth animations, and responsive layout
- **Secure Auth with Auth0** – JWT-based authentication using Auth0, including support for email/password and OAuth (Google, GitHub)

## Features

### 🎯 Core Features

- **Kanban Task Management** – Drag and drop tasks across customizable status columns in a board inspired by Jira
- **Project & Epic Hierarchy** – Structure work with Projects → Big Tasks (Epics) → Tasks → Subtasks
- **Advanced Filtering** – Filter tasks by assignee, priority, due date, or status — per column or globally
- **User Role Management** – Add/remove project members, assign tasks by username, and manage roles
- **Task Detail Modals** – View and edit descriptions, deadlines, comments, and status in a smooth modal interface
- **Real-time Updates** – WebSocket-powered live collaboration and instant UI sync for changes across team members


### 🔐 Authentication & Security

- **Auth0 Integration** – Centralized authentication and authorization powered by Auth0
- **JWT-Based Sessions** – Secure login using signed tokens stored in httpOnly cookies
- **Role-Based Access Control** – Limit access to admin-only features or project ownership actions
- **Email Verification & Password Reset** – Managed securely through Auth0’s hosted flows

### 🎨 User Experience

- **Responsive & Accessible** – Fully optimized for desktop use
- **Modern Glassmorphism UI** – Dark theme with blur effects and elegant styling
- **Smooth Animations** – Seamless transitions for modals, panels, and page interactions

### 🛠️ Developer Experience

- **Docker-First Setup** – Simple local development and production deployment using Docker Compose
- **Modular Architecture** – Clean FastAPI microservices for separation of concerns
- **Auto-Generated API Docs** – Swagger/Open available at `/docs`
- **Centralized Error Handling** – Unified handling for validation, authentication, and server errors
- **Modular Codebase** – Well-structured project with clear separation of services and shared logic

## Tech Stack

### Frontend

- **React 18** – Modern component-based UI framework using hooks and JSX
- **Vite** – Lightning-fast build tool and development server
- **Material UI (MUI)** – Component library with theming and accessibility built-in
- **Lucide Icons** – Open-source icon set with beautiful, consistent SVGs
- **Auth0 React SDK** – Seamless authentication and session management via `@auth0/auth0-react`
- **Framer Motion** – Smooth animations for modals, toasts, and page transitions
- **React Hook Form** – Lightweight form handling with validations
- **Notistack** – Elegant and easy-to-use toast/snackbar notifications


### Backend

- **FastAPI** – Lightweight Python framework for APIs and microservices
- **PostgreSQL + SQLAlchemy** – Relational DB with ORM
- **Pydantic 2** – Type-safe validation and serialization
- **Uvicorn** – ASGI server for running the app
- **Auth0 + python-jose** – Secure JWT-based authentication
- **OpenAI SDK (optional)** – AI-powered subtask suggestions
- **Pandas & XlsxWriter** – Data export for analytics

### Database & External Services

- **PostgreSQL** – Relational database used across all microservices
- **Auth0** – Authentication and authorization platform with JWT support
- **OpenAI API** – Used for generating subtask suggestions (optional feature)

### DevOps & Tools

- **Docker & Docker Compose** – Containerization and orchestration for all services
- **Uvicorn** – ASGI server for running FastAPI apps
- **Git** – Version control and project history
- **Prettier & ESLint** – Frontend formatting and linting
- **Black & Flake8** – Backend code formatting and style enforcement

## Project Structure

```
PowerBoard/
├── backend
│   ├── alembic
│   │   ├── README
│   │   ├── env.py
│   │   ├── script.py.mako
│   │   └── versions
│   ├── alembic.ini
│   ├── common
│   │   ├── __init__.py
│   │   ├── auth0_docs.py
│   │   ├── config.py
│   │   ├── database.py
│   │   ├── enums.py
│   │   ├── models
│   │   │   ├── __init__.py
│   │   │   ├── big_task.py
│   │   │   ├── big_task_member.py
│   │   │   ├── notification.py
│   │   │   ├── project.py
│   │   │   ├── project_member.py
│   │   │   ├── task.py
│   │   │   ├── task_comment.py
│   │   │   └── user.py
│   │   ├── realtime.py
│   │   ├── schemas
│   │   │   ├── __init__.py
│   │   │   ├── big_task_member_schema.py
│   │   │   ├── big_task_schema.py
│   │   │   ├── project_member_schema.py
│   │   │   ├── project_schema.py
│   │   │   ├── task_comment_schema.py
│   │   │   ├── task_schema.py
│   │   │   └── user_schema.py
│   │   └── security
│   │       ├── auth0_bearer.py
│   │       └── dependencies.py
│   ├── docker-compose.yml
│   ├── nginx
│   │   ├── Dockerfile
│   │   └── nginx.conf
│   ├── requirements
│   │   ├── ai_service.txt
│   │   ├── analytics_service.txt
│   │   ├── common.txt
│   │   ├── notification_service.txt
│   │   ├── project_service.txt
│   │   ├── realtime_gateway.txt
│   │   ├── scheduler_service.txt
│   │   └── user_service.txt
│   ├── requirements.txt
│   ├── run_services.py
│   ├── services
│   │   ├── __init__.py
│   │   ├── ai_service
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   ├── main.py
│   │   │   └── routers
│   │   │       └── suggestions.py
│   │   ├── analytics_service
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   ├── main.py
│   │   │   └── routers
│   │   │       ├── __init__.py
│   │   │       ├── dashboard.py
│   │   │       ├── export.py
│   │   │       └── project_summary.py
│   │   ├── notification_service
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   ├── events.py
│   │   │   ├── main.py
│   │   │   └── routers
│   │   │       ├── __init__.py
│   │   │       └── notifications.py
│   │   ├── project_service
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   ├── main.py
│   │   │   └── routers
│   │   │       ├── admin.py
│   │   │       ├── big_task_members.py
│   │   │       ├── big_tasks.py
│   │   │       ├── project_members.py
│   │   │       ├── projects.py
│   │   │       ├── task_comments.py
│   │   │       └── tasks.py
│   │   ├── realtime_gateway
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   └── main.py
│   │   ├── scheduler_service
│   │   │   ├── Dockerfile
│   │   │   ├── __init__.py
│   │   │   ├── jobs.py
│   │   │   └── main.py
│   │   └── user_service
│   │       ├── Dockerfile
│   │       ├── __init__.py
│   │       ├── main.py
│   │       └── routers
│   │           ├── profile.py
│   │           └── users.py
│   └── tests
│       ├── conftest.py
│       ├── factories.py
│       ├── integration
│       │   ├── conftest.py
│       │   ├── test_ai_suggestions.py
│       │   ├── test_analytics_dashboard.py
│       │   ├── test_analytics_export.py
│       │   ├── test_analytics_project_summary.py
│       │   ├── test_big_task_members.py
│       │   ├── test_big_tasks.py
│       │   ├── test_project_members.py
│       │   ├── test_projects.py
│       │   ├── test_task_comments.py
│       │   ├── test_tasks.py
│       │   └── test_user_profile.py
│       └── unit
│           ├── test_big_tasks_helpers.py
│           ├── test_effective_assignee_id_extra.py
│           ├── test_projects_helpers.py
│           ├── test_suggest_subtasks.py
│           ├── test_suggest_subtasks_extra.py
│           └── test_tasks_helpers.py
├── docker-compose.yml
└── frontend
    ├── .env.local
    ├── .env.production
    ├── Dockerfile
    ├── eslint.config.js
    ├── index.html
    ├── nginx.conf
    ├── package-lock.json
    ├── package.json
    ├── public
    │   └── vite.svg
    ├── src
    │   ├── App.css
    │   ├── App.jsx
    │   ├── api
    │   │   ├── axios.js
    │   │   └── useMyId.js
    │   ├── assets
    │   │   └── react.svg
    │   ├── components
    │   │   ├── AdminRoute.jsx
    │   │   ├── AssignedProjectsCard.jsx
    │   │   ├── BigTaskCard.jsx
    │   │   ├── BigTaskDetailsModal.jsx
    │   │   ├── BigTaskMembersModal.jsx
    │   │   ├── BigTaskProgress.jsx
    │   │   ├── CalendarCommandPanel.jsx
    │   │   ├── CardShell.jsx
    │   │   ├── CommentsSection.jsx
    │   │   ├── CreateBigTaskModal.jsx
    │   │   ├── CreateProjectModal.jsx
    │   │   ├── CreateTaskModal.jsx
    │   │   ├── DashboardExportModal.jsx
    │   │   ├── DeleteConfirmModal.jsx
    │   │   ├── DueSoonListCard.jsx
    │   │   ├── Footer.jsx
    │   │   ├── Header.jsx
    │   │   ├── HelpModal.jsx
    │   │   ├── Hero.jsx
    │   │   ├── MetricsCard.jsx
    │   │   ├── MouseGlow.jsx
    │   │   ├── NotificationProvider.jsx
    │   │   ├── NotificationsMenu.jsx
    │   │   ├── ProfileMenu.jsx
    │   │   ├── ProjectCard.jsx
    │   │   ├── ProjectLayout.jsx
    │   │   ├── ProjectMembersModal.jsx
    │   │   ├── ProjectNavigation.jsx
    │   │   ├── ProjectSettingsModal.jsx
    │   │   ├── ProjectSummaryExportModal.jsx
    │   │   ├── RecentListCard.jsx
    │   │   ├── Sidebar.jsx
    │   │   ├── TaskDetailsModal.jsx
    │   │   ├── WaterProgress.css
    │   │   ├── WaterProgress.jsx
    │   │   ├── board
    │   │   │   ├── JiraTaskBoard.jsx
    │   │   │   └── TaskCard.jsx
    │   │   ├── calendar
    │   │   │   ├── CalendarCell.jsx
    │   │   │   ├── CalendarGrid.jsx
    │   │   │   ├── CalendarHeader.jsx
    │   │   │   ├── CalendarShell.jsx
    │   │   │   ├── DayDetailsModal.jsx
    │   │   │   └── calendarUtils.js
    │   │   └── charts
    │   │       ├── ChartArea.jsx
    │   │       ├── ChartBar.jsx
    │   │       ├── ChartLine.jsx
    │   │       └── StatsChart.jsx
    │   ├── hooks
    │   │   ├── useRealtimeGateway.js
    │   │   └── useRoles.js
    │   ├── index.css
    │   ├── main.jsx
    │   ├── pages
    │   │   ├── AdminProjectsPage.jsx
    │   │   ├── BigTasksPage.jsx
    │   │   ├── Dashboard.jsx
    │   │   ├── LoginPage.jsx
    │   │   ├── MainCalendar
    │   │   │   ├── index.jsx
    │   │   │   └── useCalendarData.js
    │   │   ├── ProfilePage.jsx
    │   │   ├── ProjectCalendar
    │   │   │   ├── index.jsx
    │   │   │   └── useCalendarData.js
    │   │   ├── ProjectSummary.jsx
    │   │   ├── ProjectsPage.jsx
    │   │   └── TaskBoard.jsx
    │   ├── theme.js
    │   └── themes
    │       ├── ColorModeContext.js
    │       └── filterStyles.js
    └── vite.config.js
```


## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Docker** (20.10+) and **Docker Compose** (2.0+)
- **Git** – For cloning the repository
- **Auth0 Application** – For authentication (create one at [Auth0 Dashboard](https://manage.auth0.com/))
- **OpenAI API Key** – (Optional) For AI-based subtask suggestions

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/markdavidb/powerboard.git
   cd powerboard
   ```

2. **Create environment files**

   ```bash
   # Create backend environment file
   cp backend/.env.example backend/.env

   # Create frontend environment file
   cp frontend/.env.example frontend/.env
   ```

### Environment Setup

#### Backend Environment (`backend/.env`)

```env
# PostgreSQL Database
DATABASE_URL=postgresql://postgres.USER:password@host:port/postgres
POSTGRES_DB=postgres
POSTGRES_USER=postgres.USER
POSTGRES_PASSWORD=your_password

# Security & JWT
SECRET_KEY=your-secret-key
ACCESS_TOKEN_EXPIRE_MINUTES=1440

# OpenAI (Optional)
OPENAI_API_KEY=sk-...

# Internal Gateway
GATEWAY_INTERNAL_SECRET=dev-secret
GATEWAY_URL=http://localhost:9000

# Auth0 – Application Settings
AUTH0_DOMAIN=dev-xxx.auth0.com
AUTH0_CLIENT_ID=your_auth0_spa_client_id
AUTH0_CLIENT_SECRET=your_auth0_client_secret
AUTH0_API_AUDIENCE=https://powerboard-api.local
AUTH0_ISSUER=https://dev-xxx.auth0.com/
AUTH0_ALGORITHMS=RS256

# Auth0 – Management API (Machine-to-Machine app)
AUTH0_M2M_CLIENT_ID=...
AUTH0_M2M_CLIENT_SECRET=...
AUTH0_M2M_AUDIENCE=https://dev-xxx.auth0.com/api/v2/

# Frontend redirection (after password reset, etc.)
FRONTEND_ORIGIN=http://localhost


#### Frontend Environment (`frontend/.env`)
# Auth0 Configuration
VITE_AUTH0_DOMAIN=dev-xxx.auth0.com
VITE_AUTH0_CLIENT_ID=your_auth0_spa_client_id
VITE_AUTH0_AUDIENCE=https://powerboard-api.local
VITE_AUTH0_SCOPE=openid profile email
VITE_AUTH0_REDIRECT_URI=http://localhost/dashboard

# API Endpoints
VITE_USER_API=http://localhost/api
VITE_PROJECT_API=http://localhost/api
VITE_ANALYTICS_API=http://localhost/api
VITE_NOTIFICATION_API=http://localhost/api
VITE_AI_API=http://localhost/api

# Optional: Project-level audience
VITE_PROJECT_API_AUD=https://powerboard-api.local


```

#### Environment Variables Guide

| Variable                        | Required    | Description                                     | How to Obtain                                                                 |
| ------------------------------ | ----------- | ----------------------------------------------- | ----------------------------------------------------------------------------- |
| `DATABASE_URL`                 | ✅ Yes      | PostgreSQL connection string                    | Provided by your PostgreSQL host (e.g., Supabase or Railway)                 |
| `SECRET_KEY`                   | ✅ Yes      | JWT signing key for backend                     | Generate with `openssl rand -hex 32`                                          |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | ✅ Yes      | Token expiry time in minutes                    | Recommended: 1440 (1 day)                                                     |
| `OPENAI_API_KEY`              | 🔧 Optional | For AI-based subtask suggestions                | [OpenAI API Key](https://platform.openai.com/account/api-keys)               |
| `AUTH0_DOMAIN`                | ✅ Yes      | Your Auth0 domain                               | From [Auth0 Dashboard](https://manage.auth0.com/)                            |
| `AUTH0_CLIENT_ID`            | ✅ Yes      | SPA client ID used in Auth0                     | From your Auth0 application settings                                          |
| `AUTH0_CLIENT_SECRET`        | ✅ Yes      | Backend client secret (never expose on frontend)| From your Auth0 application settings                                          |
| `AUTH0_API_AUDIENCE`         | ✅ Yes      | Identifier for your Auth0 API                   | Set in the Auth0 API settings                                                 |
| `AUTH0_ISSUER`               | ✅ Yes      | Full issuer URL from Auth0                      | Typically: `https://<AUTH0_DOMAIN>/`                                          |
| `AUTH0_ALGORITHMS`           | ✅ Yes      | Algorithm for verifying JWTs                    | Usually `RS256`                                                               |
| `AUTH0_M2M_CLIENT_ID`        | ✅ Yes      | M2M App client ID for backend management        | From your Auth0 Machine-to-Machine App                                        |
| `AUTH0_M2M_CLIENT_SECRET`    | ✅ Yes      | M2M App secret                                   | From Auth0 Dashboard                                                          |
| `AUTH0_M2M_AUDIENCE`         | ✅ Yes      | Audience for Auth0 Management API               | Usually `https://<AUTH0_DOMAIN>/api/v2/`                                      |
| `FRONTEND_ORIGIN`            | ✅ Yes      | Used for redirecting after password reset       | e.g., `http://localhost`                                                      |
| `VITE_AUTH0_DOMAIN`          | ✅ Yes      | Your Auth0 domain for frontend                  | Same as `AUTH0_DOMAIN`                                                        |
| `VITE_AUTH0_CLIENT_ID`       | ✅ Yes      | Frontend SPA client ID                          | Same as `AUTH0_CLIENT_ID`                                                     |
| `VITE_AUTH0_AUDIENCE`        | ✅ Yes      | Audience used in frontend API calls             | Matches `AUTH0_API_AUDIENCE`                                                  |
| `VITE_AUTH0_SCOPE`           | ✅ Yes      | Scopes for Auth0 login                          | Usually `openid profile email`                                                |
| `VITE_AUTH0_REDIRECT_URI`    | ✅ Yes      | Where Auth0 redirects after login               | e.g., `http://localhost/dashboard`                                            |
| `VITE_PROJECT_API`           | ✅ Yes      | Base URL for your project API                   | e.g., `http://localhost/api`                                                  |


## Running the Application

### 1. PostgreSQL Setup (Required)

This project uses a **PostgreSQL database**. If you're using a cloud provider like **Supabase**, make sure to:

- Create a PostgreSQL database
- Whitelist your IP if needed
- Copy the connection string and add it to your `.env` file as `DATABASE_URL`

If you want to run a local PostgreSQL instance:

```bash
docker run -d \
  --name powerboard-postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=yourpassword \
  -e POSTGRES_DB=postgres \
  -p 5432:5432 \
  postgres:15
```

### 2. Start All Services

To run the entire PowerBoard system locally with all backend services, frontend, and reverse proxy:

```bash
docker-compose up --build
```
This command will:

  * **Build** all services using their respective `Dockerfiles`.
  * **Start** each container with proper environment variables and automatically resolve service dependencies.

**Included services from `docker-compose.yml`:**

| Service          | Description                               | Port   |
| :--------------- | :---------------------------------------- | :----- |
| `user`           | User authentication (Auth0-based)         | `8001` |
| `project`        | Project/task management microservice      | `8002` |
| `analytics`      | Analytics dashboards and statistics       | `8003` |
| `notification`   | Notification delivery and scheduling      | `8004` |
| `scheduler`      | Background job runner                     | `8005` |
| `ai`             | AI service for subtask generation         | `8006` |
| `realtime-gateway` | Internal pub/sub messaging layer        | `9000` |
| `frontend`       | React client served via Nginx             | `3000` |
| `nginx`          | Reverse proxy for routing external access | `80`   |

Once started, the application is available at:

  * **Frontend**: `http://localhost:3000`
  * **Nginx Proxy (main access point)**: `http://localhost`
  * **Individual APIs** (e.g., `http://localhost:8001/docs` for User Service Swagger UI)

-----

## API Documentation

### AI Service

| Method | Endpoint                        | Description                                  | Auth Required |
| :----- | :------------------------------ | :------------------------------------------- | :------------ |
| `POST` | `/api/ai/suggest_subtasks`      | Suggest subtasks for a given description.    | ✅            |

### Analytics Service

| Method | Endpoint                            | Description                                      | Auth Required |
| :----- | :---------------------------------- | :----------------------------------------------- | :------------ |
| `GET`  | `/api/analytics/dashboard/summary`  | Get a summary of projects and tasks.             | ✅            |
| `GET`  | `/api/analytics/dashboard/projects/cumulative` | Get cumulative project data over a period. | ✅            |
| `GET`  | `/api/analytics/export`             | Export analytics data (dashboard or project summary) in various formats. | ✅            |
| `GET`  | `/api/analytics/projects/{project_id}/tasks/monthly` | Get monthly task creation and completion data for a specific project. | ✅            |

### Project Management

#### Projects

| Method | Endpoint                      | Description                                          | Auth Required |
| :----- | :---------------------------- | :--------------------------------------------------- | :------------ |
| `POST` | `/api/projects/`              | Create a new project.                                | ✅            |
| `GET`  | `/api/projects/`              | Get all projects for the current user, optionally filtered. | ✅            |
| `GET`  | `/api/projects/{project_id}`  | Get a specific project by ID.                        | ✅            |
| `PUT`  | `/api/projects/{project_id}`  | Update an existing project.                          | ✅            |
| `DELETE` | `/api/projects/{project_id}` | Delete a project.                                    | ✅            |

#### Project Members

| Method | Endpoint                                 | Description                                | Auth Required |
| :----- | :--------------------------------------- | :----------------------------------------- | :------------ |
| `POST` | `/api/projects/project_members/`         | Add a member to a project.                 | ✅            |
| `DELETE` | `/api/projects/project_members/{project_id}/members/{username}` | Remove a member from a project. | ✅            |
| `PUT`  | `/api/projects/project_members/{project_id}/members/{username}` | Update a project member's role. | ✅            |

#### Big Tasks

| Method | Endpoint                               | Description                                | Auth Required |
| :----- | :------------------------------------- | :----------------------------------------- | :------------ |
| `POST` | `/api/projects/big_tasks/`             | Create a new big task.                     | ✅            |
| `GET`  | `/api/projects/big_tasks/`             | Get all big tasks, optionally filtered by project. | ✅            |
| `GET`  | `/api/projects/big_tasks/{big_task_id}` | Get a specific big task by ID.             | ✅            |
| `PUT`  | `/api/projects/big_tasks/{big_task_id}` | Update an existing big task.               | ✅            |
| `DELETE` | `/api/projects/big_tasks/{big_task_id}` | Delete a big task.                         | ✅            |

#### Big Task Members

| Method | Endpoint                                   | Description                                  | Auth Required |
| :----- | :----------------------------------------- | :------------------------------------------- | :------------ |
| `POST` | `/api/projects/big_task_members/`          | Add a member to a big task.                  | ✅            |
| `GET`  | `/api/projects/big_task_members/{big_task_id}/members` | Get all members of a specific big task. | ✅            |
| `DELETE` | `/api/projects/big_task_members/{big_task_id}/members/{username}` | Remove a member from a big task. | ✅            |

#### Tasks

| Method | Endpoint                          | Description                                      | Auth Required |
| :----- | :-------------------------------- | :----------------------------------------------- | :------------ |
| `POST` | `/api/projects/tasks/`            | Create a new task.                               | ✅            |
| `GET`  | `/api/projects/tasks/`            | Get all tasks, optionally filtered by project or big task. | ✅            |
| `GET`  | `/api/projects/tasks/{task_id}`   | Get a specific task by ID.                       | ✅            |
| `PUT`  | `/api/projects/tasks/{task_id}`   | Update an existing task.                         | ✅            |
| `DELETE` | `/api/projects/tasks/{task_id}` | Delete a task.                                   | ✅            |

#### Task Comments

| Method | Endpoint                            | Description                                | Auth Required |
| :----- | :---------------------------------- | :----------------------------------------- | :------------ |
| `POST` | `/api/tasks/comments/`              | Create a new comment for a task.           | ✅            |
| `GET`  | `/api/tasks/{task_id}/comments`     | Get all comments for a specific task.      | ✅            |
| `PUT`  | `/api/tasks/comments/{comment_id}`  | Update an existing comment.                | ✅            |
| `DELETE` | `/api/tasks/comments/{comment_id}` | Delete a comment.                          | ✅            |


#### User Profile & Management

| Method | Endpoint                            | Description                                        | Auth Required |
| :----- | :---------------------------------- | :------------------------------------------------- | :------------ |
| `GET`  | `/api/users/me`                     | Returns the current user's profile.      | ✅            |
| `PUT`  | `/api/users/me`                     | Updates the current user's profile.      | ✅            |
| `POST` | `/api/users/password-change-ticket` | Initiates a password change flow by returning a ticket URL. | ✅            |

#### Notification Service

| Method | Endpoint                            | Description                                          | Auth Required |
| :----- | :---------------------------------- | :--------------------------------------------------- | :------------ |
| `GET`  | `/api/notifications/`               | List all notifications for the current user. If `unread_only=True`, return only the unread ones, and immediately mark them as read in the database. | ✅            |
| `POST` | `/api/notifications/{note_id}/read` | Mark a single notification as read.        | ✅            |

## Usage Guide

### 1. Register and Log In

- Open [http://localhost:3000](http://localhost:3000) in your browser.
- Click **Sign Up** to create a new account with your email and password (Auth0 authentication).
- Verify your email if prompted.
- Log in to access your workspace.

### 2. Create a New Project

- Go to **Projects** in the sidebar.
- Click **Create New Project**.
- Enter project name, description, due date, and status.
- (Optional) Add team members by their username (they must be registered on the site).

### 3. Project Board and Big Tasks

- Enter the project page to access its Kanban board.
- Create **Big Tasks** (Epics) for major work streams.
- For each Big Task, you can add specific group members who will work on it.
  - Only assigned members can access and manage that Big Task and its tasks.
- Within each Big Task, create smaller tasks to organize the workflow.

### 4. Task Management

- Click any task to open its details modal.
- Edit description, due date, assignee, and add comments.
- Manage subtasks and update status directly in the modal.

### 5. Filtering and Analytics

- Use filters to view tasks by assignee, due date, priority, or status.
- Open the dashboard for charts, metrics, and data export.

### 6. Notifications and Real-Time Updates

- Receive in-app notifications for assignments, comments, and project changes.
- All updates are synced in real-time for everyone involved.

### 7. AI Suggestions (Optional)

- In Big Task details, use **AI Suggest Subtasks** to generate task suggestions (requires OpenAI API key in backend).

### 8. Export Data

- Export project summaries or analytics dashboards as CSV or JSON from the UI.



## Development

### Local Development Setup

1. **Frontend Development**

   ```bash
   cd frontend
   npm install
   npm run dev
   ```

2. **Backend Development**

   ```bash
   cd backend
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   python run_services.py
   ```

3. **Database Setup (Local PostgreSQL)**
   ```bash
   docker run -d \
    --name powerboard-postgres \
    -e POSTGRES_USER=postgres \
    -e POSTGRES_PASSWORD=yourpassword \
    -e POSTGRES_DB=postgres \
    -p 5432:5432 \
    postgres:15

   ```

## Testing

The project includes comprehensive backend and integration testing using pytest.
Tests are located under backend/tests/ and can be run manually or via Docker build.

```bash
cd backend
pytest
```

Running Specific Test Suites
```bash
# Unit tests
pytest tests/unit/ -v

# Integration tests
pytest tests/integration/ -v

```

**Note**: There are currently **no frontend tests** implemented. Only backend testing is available.


## Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines

- Follow existing code style and conventions
- Write meaningful commit messages
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

**Project Maintainer**: Mark David Boyko

- Email: maarkboyko@gmail.com
- GitHub: [markdavidb](https://github.com/markdavidb)
- Project Link: [https://github.com/markdavidb/powerboard](https://github.com/markdavidb/powerboard)

---


_PowerBoard - simple, flexible, and powerful._


