# Deployment

classifai-platform is an orchestration and documentation repo. Production
deployments should build and run the classifAI and taxomind services directly
from their component repositories.

## Production pattern

- Put a reverse proxy (TLS) in front of classifAI and taxomind.
- Use a persistent database for classifAI (managed Postgres or equivalent).
- Store secrets in a secrets manager; do not use `.env.example` in production.
- Scale taxomind independently from classifAI; AI is optional.
- Keep taxomind on a private network segment if possible.

## Images and releases

- Build and publish images from the classifAI and taxomind repos.
- This repo wires images together for local dev and reference deployments.

## Support routing

- UI/workflows issues: classifAI repo
- AI service issues: taxomind repo
- Stack/docs issues: classifai-platform repo
