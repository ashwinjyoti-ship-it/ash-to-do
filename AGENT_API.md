# Ashwin List unified agent API

The deployed site exposes a small REST data API via here.now. It is designed for agents and automation as well as the UI.

Base URL: `https://<site-slug>.here.now/.herenow/data/items`

| Action | Method | Endpoint | Body |
| --- | --- | --- | --- |
| List items | `GET` | `/items?limit=50` | — |
| Read one | `GET` | `/items/{recordId}` | — |
| Create | `POST` | `/items` | task or document object |
| Update (owner) | `PATCH` | `/items/{recordId}` | any mutable fields |
| Delete (owner) | `DELETE` | `/items/{recordId}` | — |

Use `Content-Type: application/json` for writes and an `Idempotency-Key` when retrying a create. For a task use `{ "kind":"task", "text":"…", "tag":"work", "when":"today", "done":false }`. For rich writing use `{ "kind":"document", "title":"Quote", "content":"<blockquote>Formatted HTML</blockquote>" }`.

Public agents can read and add tasks. Updates and deletes require the owner API: `https://here.now/api/v1/publishes/<slug>/data/todos` with `Authorization: Bearer <API_KEY>`.
