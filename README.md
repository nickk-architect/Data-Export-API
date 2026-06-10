# Data-Export-API

Curl-based reference scripts for interacting with the [Decagon Conversations API](https://docs.decagon.ai). Intended for enterprise integrations (e.g. Genesys, CCaaS platforms) that need to create, manage, and export AI conversation data programmatically.

## Base URL

```
https://api.decagon.ai
```

## Authentication

All requests require a Bearer token:

```bash
-H 'Authorization: Bearer YOUR_API_KEY'
```

**Rate limit:** 1 request/second across all endpoints.

---

## Scripts

### `decagon_conversations_api_reference.sh`

Full reference covering every available endpoint, organized into four sections:

- **Create & Manage** — create new conversations (`/new`, `/new_by_api_key`, `/get_or_create`), close, delete, and mark conversations as escalated
- **Read Messages** — fetch message history, all conversations for a user, unread counts, and add feedback
- **Transcripts & Exports** — export conversations in bulk (paginated, filterable by metadata like ANI/Caller), retrieve or download transcripts, generate AI summaries, email transcripts, and get voice recording URLs
- **Metadata** — link conversations to users, update metadata (e.g. Genesys conversation ID, Caller ANI), backfill historical messages, and delete all data for a user (GDPR)

### `decagon_export_and_create_conversations.sh`

Focused script covering the three most common integration touchpoints:

1. **Export** — filter exported conversations by metadata (e.g. Caller ANI) using `user_filters`
2. **Create** — start a new conversation via `/new_by_api_key` with a `user_id` (ANI), `flow_id`, and optional metadata; Decagon uses the ANI to associate the call with existing caller history
3. **Summarize** — retrieve an AI-generated summary of a completed conversation by `conversation_id`

---

## Common Use Cases

- **Post-call workflows** — after a Genesys/CCaaS call ends, create a Decagon conversation, pass metadata like `CCaaS_Flow_Id` and caller ANI, then retrieve a summary
- **Bulk data export** — paginate through conversation exports filtered by caller phone number or other metadata fields
- **GDPR / data purge** — delete all data associated with a specific user ID
- **Transcript delivery** — download or email transcripts for QA, compliance, or CRM ingestion

---

## Docs

- Full API reference: https://docs.decagon.ai/llms.txt
- Export API: https://docs.decagon.ai/external/api-reference/exporting-conversations-via-api
- Chat API endpoints: https://docs.decagon.ai/internal/api-data/chat-api-endpoints
