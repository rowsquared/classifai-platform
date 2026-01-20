
# classifai-platform

End-to-end platform for **hierarchical classification workflows**:
a user-friendly labeling UI + an optional AI classification service.

- **classifAI** → UI + database + workflow (projects, assignments, review, analytics)
- **taxomind** → modular hierarchical classification engine (Kedro + FastAPI job API)

This repository is the **umbrella**: documentation and a local stack to run both together.

## Repositories

- **classifAI (UI + backend)**: https://github.com/rowsquared/classifAI  
  A self-hosted labeling platform for deep taxonomies (ISCO, ISIC, COICOP, and beyond).
- **taxomind (AI service)**: https://github.com/rowsquared/taxomind  
  A multilingual hierarchical classification service with retrieval + routing + explicit stopping and optional incremental learning.

## Architecture

**classifAI** is the system of record (users, projects, annotations, audits).  
If enabled, **classifAI calls taxomind** to get AI label suggestions and to send corrections back for learning.

Typical flow:
1. User labels items in classifAI.
2. classifAI requests suggestions from taxomind (optional).
3. User confirms/corrects labels.
4. classifAI can send corrections to taxomind’s learning endpoint (optional).

## Quickstart (local stack)

This repo provides a reference Docker Compose stack in `dev/docker-compose.yml`.

1. Clone:
   ```bash
   git clone https://github.com/rowsquared/classifai-platform.git
   cd classifai-platform
  ```
	2.	Create env file:
  ```bash
  cp examples/.env.example .env
  ```bash

	3.	Start:
  ```bash
  docker compose -f dev/docker-compose.yml up -d
  ```

	4.	Open classifAI:
	•	http://localhost:3000

Notes:
	•	You can run classifAI without taxomind. The UI and workflows work in “human-only” mode.
	•	To enable AI suggestions, configure AI_LABELING_API_URL and AI_LABELING_API_KEY.

Configuration overview

classifAI (required)

See classifAI docs for full environment variables.

AI suggestions (optional)

To connect taxomind:
	•	AI_LABELING_API_URL (e.g. http://taxomind:8000)
	•	AI_LABELING_API_KEY

Documentation
	•	docs/architecture.md — components, ports, and integration points
	•	docs/local-dev.md — development workflow and troubleshooting
	•	docs/deployment.md — production patterns (reverse proxy, DB, secrets)

License

MIT. See LICENSE.

Support

Open a GitHub issue in the relevant repository:
	•	UI/workflows: classifAI repo
	•	AI service: taxomind repo
	•	Stack/docs: this repository
