# Architecture

classifai-platform documents how classifAI and taxomind fit together. AI is
optional; classifAI runs independently without taxomind.

## Components

- classifAI: UI + API + database-backed workflows. System of record.
- taxomind: optional AI classification service (Kedro + FastAPI job API).
- Postgres (dev stack): local database for classifAI.
- classifai-platform: docs and orchestration.

## Diagram

+-----------+        +-------------------+        +------------------------+
| Web users | <----> | classifAI UI/API  | -----> | taxomind API (optional) |
+-----------+        +-------------------+        +------------------------+
                           |
                           v
                      +---------+
                      | Postgres|
                      +---------+

## Ports (dev defaults)

- classifAI web: http://localhost:3000
- taxomind API: http://localhost:8000 (only when profile "ai" is enabled)
- Postgres: localhost:5432

## Request flow (high level)

1. A user labels items in classifAI.
2. classifAI optionally requests AI suggestions from taxomind.
3. The user confirms or corrects labels.
4. classifAI can optionally send feedback for learning.

## Auth boundary (service-to-service)

- classifAI calls taxomind with a Bearer token from `AI_LABELING_API_KEY`.
- taxomind should reject missing or invalid tokens.

## Data boundary

- classifAI stores source data, projects, annotations, and audit trails.
- taxomind receives only the payload needed to generate suggestions and optional
  feedback.

## Support routing

- UI/workflows issues: classifAI repo
- AI service issues: taxomind repo
- Stack/docs issues: classifai-platform repo
