# Architecture

classiflow-platform documents how classiflow and taxomind fit together. AI is
optional; classiflow runs independently without taxomind.

## Components

- classiflow: UI + API + database-backed workflows. System of record.
- taxomind: optional AI classification service (Kedro + FastAPI job API).
- Postgres (dev stack): local database for classiflow.
- classiflow-platform: docs and orchestration.

## Diagram

```text
+-----------+        +-------------------+        +------------------------+
| Web users | <----> | classiflow UI/API  | -----> | taxomind API (optional) |
+-----------+        +-------------------+        +------------------------+
                           |
                           v
                      +---------+
                      | Postgres|
                      +---------+
```

## Ports (dev defaults)

- classiflow web: http://localhost:3000
- taxomind API: http://localhost:8000 (only when profile "ai" is enabled)
- Postgres: localhost:5432

## Request flow (high level)

1. A user labels items in classiflow.
2. classiflow optionally requests AI suggestions from taxomind.
3. The user confirms or corrects labels.
4. classiflow can optionally send feedback for learning.

## Auth boundary (service-to-service)

- classiflow calls taxomind with a Bearer token from `AI_LABELING_API_KEY`.
- taxomind should reject missing or invalid tokens.

## Data boundary

- classiflow stores source data, projects, annotations, and audit trails.
- taxomind receives only the payload needed to generate suggestions and optional
  feedback.

## Support routing

- UI/workflows issues: classiflow repo
- AI service issues: taxomind repo
- Stack/docs issues: classiflow-platform repo

