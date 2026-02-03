# Contributing

Thanks for helping improve classiflow-platform.

## Scope

This repo is the front door for the ecosystem: docs, local dev orchestration,
and integration guidance. For product changes, use the component repos:

- classiflow: https://github.com/rowsquared/classifAI
- taxomind: https://github.com/rowsquared/taxomind

## How to contribute

1. Open or pick an issue in the correct repository.
2. Fork and create a feature branch.
3. Keep docs concise and user-focused.
4. Do not commit secrets; update `examples/.env.example` for new config values.
5. Open a pull request with a clear description.

## Development

- Local dev instructions: `docs/local-dev.md`.
- The Docker Compose stack reads `.env` from the repo root.

## Support routing

- UI/workflows issues: classiflow repo
- AI service issues: taxomind repo
- Stack/docs issues: classiflow-platform repo
