# Integration (classifAI -> taxomind)

classifAI can call taxomind for AI label suggestions. This integration is
optional.

## Required configuration

Set these variables in classifAI:

- `AI_LABELING_API_URL`: Base URL for taxomind.
- `AI_LABELING_API_KEY`: Bearer token used by classifAI.

Example values:

```bash
AI_LABELING_API_URL=http://taxomind:8000
AI_LABELING_API_KEY=change-me
```

## Auth behavior

- classifAI sends `Authorization: Bearer <AI_LABELING_API_KEY>`.
- taxomind should reject missing or invalid tokens.

## Endpoints

- classifAI uses the taxomind HTTP API. See the taxomind repo for endpoint
  paths and request bodies.

## Support routing

- UI/workflows issues: classifAI repo
- AI service issues: taxomind repo
- Stack/docs issues: classifai-platform repo
