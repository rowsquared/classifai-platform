# Usage overview

classifAI is the labeling platform. It provides the UI, workflows, user
management, and the database of record for projects and annotations.

taxomind is the optional AI service. It exposes an HTTP API that returns label
suggestions and related metadata.

Typical interaction: classifAI calls taxomind using `AI_LABELING_API_URL` and
`AI_LABELING_API_KEY`, then displays the suggestions for human review.

AI is optional. classifAI runs fully without taxomind, and taxomind can be used
independently in other integrations.
