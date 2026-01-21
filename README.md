# classifai-platform

<video controls playsinline muted loop>
  <source src="docs/assets/classifai-overview.mp4" type="video/mp4">
  Your browser does not support the video tag. Open it here:
  docs/assets/classifai-overview.mp4
</video>

Complex classifications made easy. Open-source, AI-assisted, and user-friendly.
Built for ISCO, ISIC, COICOP, and beyond.

classifai-platform is the front door for the classifAI ecosystem: documentation,
local development orchestration, and integration guidance for running classifAI
with the optional taxomind AI service.

AI is optional. classifAI runs as a full labeling platform without taxomind.

## Components

- classifAI: labeling UI + database + workflows
- taxomind: optional AI classification service (HTTP API)

## Links

- Website: https://rowsquared.com/classifai/
- classifAI repo: https://github.com/rowsquared/classifAI
- taxomind repo: https://github.com/rowsquared/taxomind

## Why classifAI

### Faster & Cheaper
Get instant preliminary results from AI, then let your team verify and correct
the suggestions. Time and cost drop as the model learns from corrections.

![Faster & Cheaper](docs/assets/faster-cheaper.webp)

### Improved Quality
Review and correct AI suggestions to continuously improve quality. Use review and
double-annotation workflows to create gold standards.

![Improved Quality](docs/assets/improved-quality.webp)

### Simple Process Management
Track progress, assign work, and manage workflows in one place. Custom filters,
flexible assignments, and built-in commenting keep teams aligned.

![Simple Process Management](docs/assets/simple-process-management.webp)

### Solid AI Integration
AI predictions can be wrong. classifAI (via taxomind) keeps humans in control,
so teams review every prediction and teach the model over time.

![Solid AI Integration](docs/assets/solid-ai-integration.webp)

## Architecture summary

```text
+-----------+        +-------------------+        +------------------------+
| Web users | <----> | classifAI UI/API  | -----> | taxomind API (optional) |
+-----------+        +-------------------+        +------------------------+
                           |
                           v
                      +---------+
                      | Postgres|
                      +---------+
```

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
