# Architecture Overview

This diagram describes the current monorepo implementation, not a proposed cloud deployment.
The React frontend communicates with the Express API, which stores tasks in an in-memory SQLite
database. Data is lost when the backend process restarts.

## System Context

```mermaid
flowchart LR
  User[User] -->|Uses in browser| Frontend[React frontend]
  subgraph Monorepo[TODO application monorepo]
    Frontend -->|HTTP task requests| API[Express API]
    API -->|Read and write tasks| Store[(In-memory SQLite database)]
  end
```

## Create a TODO

```mermaid
sequenceDiagram
  actor User
  participant UI as React frontend
  participant API as Express API
  participant DB as In-memory SQLite

  User->>UI: Enter task details and submit
  UI->>UI: Validate required title
  alt Title is missing
    UI-->>User: Show required-title error
  else Title is valid
    UI->>API: POST /api/tasks with task details
    API->>API: Validate title
    API->>DB: Insert task and read created record
    DB-->>API: Created task
    API-->>UI: 201 Created with task JSON
    UI->>API: GET /api/tasks to refresh list
    API->>DB: Query tasks
    DB-->>API: Task records
    API-->>UI: Task list JSON
    UI-->>User: Display refreshed task list
  end
```