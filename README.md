# classifai-platform

classifai-platform is the front door for the classifAI ecosystem: documentation,
local development orchestration, and integration guidance for running classifAI
with the optional taxomind AI service.

AI is optional. classifAI runs as a full labeling platform without taxomind.

## Repositories

- classifAI (UI + backend): https://github.com/rowsquared/classifAI
- taxomind (AI service): https://github.com/rowsquared/taxomind

## Architecture summary

+-----------+        +-------------------+        +------------------------+
| Web users | <----> | classifAI UI/API  | -----> | taxomind API (optional) |
+-----------+        +-------------------+        +------------------------+
                           |
                           v
                      +---------+
                      | Postgres|
                      +---------+

- classifAI is the system of record (users, projects, annotations, audits).
- taxomind provides optional AI label suggestions over an HTTP API.
- classifAI authenticates to taxomind with a Bearer token.

## Quickstart (Docker Compose)

1. Clone and enter the repo:
   ```bash
   git clone https://github.com/rowsquared/classifai-platform.git
   cd classifai-platform
   ```
2. Create your local env file:
   ```bash
   cp examples/.env.example .env
   ```
3. Start classifAI (default, no AI):
   ```bash
   docker compose -f dev/docker-compose.yml up -d
   ```
4. Open classifAI:
   - http://localhost:3000

## Run without AI

- Use the default compose command (no profile).
- Leave taxomind stopped; classifAI still works in human-only mode.
- If you see AI connection errors, remove or blank `AI_LABELING_API_URL` and
  `AI_LABELING_API_KEY` in `.env`.

## Enable AI suggestions

1. Ensure the integration values are set in `.env`:
   - `AI_LABELING_API_URL=http://taxomind:8000`
   - `AI_LABELING_API_KEY=change-me`
2. Start with the AI profile:
   ```bash
   docker compose -f dev/docker-compose.yml --profile ai up -d
   ```

## Manual setup (advanced)

- Run classifAI from its repository (UI + API + DB).
- Run taxomind from its repository if you want AI suggestions.
- Point classifAI to taxomind with `AI_LABELING_API_URL` and
  `AI_LABELING_API_KEY`.

## Configuration overview

- `.env` at the repo root drives `dev/docker-compose.yml`.
- Common classifAI settings: `NEXTAUTH_SECRET`, `DEFAULT_ADMIN_EMAIL`,
  `DEFAULT_ADMIN_PASSWORD`.
- AI integration settings: `AI_LABELING_API_URL`, `AI_LABELING_API_KEY`.
- For full configuration options, see the classifAI and taxomind docs.

## Documentation

- `docs/architecture.md` - components, ports, and integration boundaries
- `docs/local-dev.md` - local dev workflow and troubleshooting
- `docs/deployment.md` - production patterns and scaling
- `docs/integration.md` - classifAI to taxomind configuration

## Support

Open an issue in the relevant repository:

- UI/workflows: classifAI repo
- AI service: taxomind repo
- Stack/docs: this repository (classifai-platform)

## License

MIT. See `LICENSE`.
