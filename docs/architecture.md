# 🧠 Scoutd — System Architecture

## ⚽ Overview

Scoutd is a full-stack football scouting and analytics platform designed to help users discover, analyze, and compare football players.

The system follows a **client-server architecture** with clear separation between frontend, backend, external APIs, and database layers.

It supports:

- Player search and discovery
- Player profile analysis
- Player comparison
- Watchlist management
- User authentication
- Data visualization (future expansion)

---

## 🏗️ High-Level Architecture

### System Flow

Frontend (React) → Backend API (FastAPI - Python) → External Football API (API-Football) → Database (MySQL)

---

### Architecture Breakdown

| Layer | Technology | Purpose |
|------|------------|---------|
| Frontend | React | User interface, dashboards, and visualization |
| Backend | FastAPI (Python) | API logic, authentication, data processing |
| External API | API-Football | Provides football data (players, stats, matches) |
| Database | MySQL | Stores users, watchlists, and application data |

---

## 🧩 System Components

---

## 🎨 1. Frontend (Client)

**Technology:** React

### Responsibilities

- Render user interface
- Player search UI
- Player profile pages
- Player comparison dashboard
- Watchlist interface
- Data visualization (charts, graphs)

### Communication

- Communicates with backend via REST API
- Receives JSON responses

---

## ⚙️ 2. Backend (Server)

**Technology:** Python (FastAPI)

### Responsibilities

- Handle all API requests from frontend
- Process and structure football data
- Communicate with external API (API-Football)
- Manage authentication (JWT)
- Handle watchlist logic
- Normalize and filter data before sending to frontend

### Core API Routes (MVP)

| Route | Description |
|------|------------|
| `/players/search` | Search players |
| `/players/{id}` | Get player details |
| `/compare` | Compare two players |
| `/auth/register` | User registration |
| `/auth/login` | User login |
| `/watchlist` | Add/remove saved players |

### Backend Design Principles

- FastAPI for routing
- Pydantic for validation
- Service layer for business logic
- Modular structure (routes, services, models)

---

## 🛰️ 3. External API Layer

**API Used:** API-Football

### Responsibilities

- Provide raw football data:
  - Player statistics
  - Teams
  - Leagues
  - Match data

### System Role

- Backend acts as a middleware layer
- Frontend NEVER directly accesses API-Football
- Backend processes and filters all external data

---

## 🗄️ 4. Database Layer

**Database:** MySQL

### Responsibilities

- Store user accounts
- Store authentication data
- Store user watchlists
- Cache frequently accessed player data (optional optimization)

---

## 🧾 Database Schema (Initial Design)

---

## 👤 users Table

| Field | Type | Description |
|------|------|------------|
| id | INT (PK) | Unique user ID |
| name | VARCHAR | Full name |
| email | VARCHAR | Unique email |
| password | VARCHAR | Hashed password |
| created_at | TIMESTAMP | Account creation time |

---

## ⭐ watchlist Table

| Field | Type | Description |
|------|------|------------|
| id | INT (PK) | Unique record ID |
| user_id | INT (FK) | Links to users table |
| player_id | INT | API-Football player ID |
| player_name | VARCHAR | Cached player name |
| created_at | TIMESTAMP | When player was saved |

---

## 🔄 Data Flow

---

### 1. Player Search Flow

Frontend → Backend (FastAPI) → API-Football → Backend Processing → Frontend

---

### 2. Watchlist Flow

Frontend → Backend (FastAPI) → MySQL Database → Backend → Frontend

---

### 3. Authentication Flow

Frontend → Backend (FastAPI) → MySQL → JWT Token → Frontend

---

## 🧠 Design Principles

- Separation of Concerns (Frontend / Backend / Database)
- Scalable service-based backend architecture
- Secure handling of API keys (backend only)
- Modular and maintainable codebase
- MVP-first development approach

---

## 🚀 MVP (Minimum Viable Product)

### Core Features

- Player search
- Player profile view
- Player comparison
- Watchlist system
- User authentication
