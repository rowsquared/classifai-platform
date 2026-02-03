# Deployment

classiflow-platform is an orchestration and documentation repo. Production
deployments should build and run the classiflow and taxomind services directly
from their component repositories.

## Production pattern

- Put a reverse proxy (TLS) in front of classiflow and taxomind.
- Use a persistent database for classiflow (managed Postgres or equivalent).
- Store secrets in a secrets manager; do not use `.env.example` in production.
- Scale taxomind independently from classiflow; AI is optional.
- Keep taxomind on a private network segment if possible.

## Images and releases

- Build and publish images from the classiflow and taxomind repos.
- This repo wires images together for local dev and reference deployments.

## Support routing

- UI/workflows issues: classiflow repo
- AI service issues: taxomind repo
- Stack/docs issues: classiflow-platform repo

