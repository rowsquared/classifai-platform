# Local development

This repo provides a Docker Compose stack for running classifAI with optional
AI suggestions via taxomind.

## Docker Compose (recommended)

1. Copy the template env file:
   ```bash
   cp examples/.env.example .env
   ```
2. Start classifAI (default, no AI):
   ```bash
   docker compose -f dev/docker-compose.yml up -d
   ```
3. Open classifAI:
   - http://localhost:3000

To enable AI suggestions:

```bash
docker compose -f dev/docker-compose.yml --profile ai up -d
```

To stop the stack:

```bash
docker compose -f dev/docker-compose.yml down
```

## Manual run (advanced)

- Run classifAI from its repository (UI + API + DB).
- Run taxomind from its repository if you want AI suggestions.
- Set `AI_LABELING_API_URL` and `AI_LABELING_API_KEY` in classifAI.
- Ensure classifAI can reach the taxomind base URL.

## Configuration locations

- `.env` at the repo root is loaded by `dev/docker-compose.yml`.
- `examples/.env.example` is the template to copy.

## Changing ports

- Edit the port mappings in `dev/docker-compose.yml`.
- If you change the taxomind port, update `AI_LABELING_API_URL` in `.env`.

## Troubleshooting

- Port conflicts: stop the process using the port or edit the mapping.
- Compose profiles: taxomind only runs with `--profile ai`.
- Rebuilding images: `docker compose -f dev/docker-compose.yml build --no-cache`.

## Support routing

- UI/workflows issues: classifAI repo
- AI service issues: taxomind repo
- Stack/docs issues: classifai-platform repo
