# Cloud Architecture Overview

This monorepo is a simple two-tier application with a browser-based frontend and a Node.js backend API. In the current implementation, data is stored in an in-memory SQLite database inside the backend process, so persistence lasts only for the life of the running server.

## System Context

```mermaid
flowchart LR
    User[User]
    Browser[Web Browser]
    Frontend[Frontend App\nReact + MUI\npackages/frontend]
    Backend[Backend API\nNode.js + Express\npackages/backend]
    Database[(In-Memory SQLite\nbetter-sqlite3)]

    User --> Browser
    Browser --> Frontend
    Frontend -->|HTTP /api/tasks| Backend
    Backend --> Database
```

## Sequence Diagram: Create a TODO

```mermaid
sequenceDiagram
    actor User
    participant Frontend as React Frontend
    participant Backend as Express API
    participant Database as In-Memory SQLite

    User->>Frontend: Enter task details and submit form
    Frontend->>Backend: POST /api/tasks with task payload
    Backend->>Backend: Validate title and request body
    Backend->>Database: INSERT new task record
    Database-->>Backend: Return inserted task id
    Backend->>Database: SELECT created task by id
    Database-->>Backend: Return created task
    Backend-->>Frontend: 201 Created with task JSON
    Frontend-->>User: Refresh task list and display new TODO
```

## Notes

- The frontend runs as a React application from the monorepo frontend package.
- The frontend calls the backend through `/api/tasks` endpoints.
- The backend runs as an Express service from the monorepo backend package.
- The database is not an external cloud service; it is an in-memory SQLite instance embedded in the backend process.
- No separate authentication, queueing, object storage, or third-party cloud services are present in the current repo.
