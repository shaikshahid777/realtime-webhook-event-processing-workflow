# Real-Time Webhook Event Processing Workflow — Lesson 5 Assessment

Production-style n8n webhook workflow for receiving real-time new-user events, validating an X-Webhook-Token header, normalizing payload data, routing authorized and unauthorized requests, and returning custom HTTP responses.

## Workflow Architecture

```text
POST /new-user
      ↓
New User Webhook (POST)
      ↓
Validate X-Webhook-Token
   ↙                 ↘
FALSE                 TRUE
  ↓                     ↓
Respond 403       Normalize User Profile
Forbidden                ↓
                   Respond 200 Success
```

## Features

- POST webhook endpoint using `new-user`
- Response controlled by Respond to Webhook nodes
- X-Webhook-Token validation
- Authorized and unauthorized routing
- HTTP 200 success response
- HTTP 403 forbidden response
- Email normalization with trim + lowercase
- Name whitespace normalization
- `receivedAt` timestamp generation
- Test versus production webhook guidance
- Webhook security and troubleshooting notes

## Example Request

```bash
curl -X POST "<N8N_WEBHOOK_URL>/new-user" \
  -H "Content-Type: application/json" \
  -H "X-Webhook-Token: <YOUR_TOKEN>" \
  -d '{"name":"Jane Doe","email":" JANE.DOE@EXAMPLE.COM "}'
```

Expected authorized response: HTTP 200 with normalized user information.

Unauthorized test:

```bash
curl -X POST "<N8N_WEBHOOK_URL>/new-user" \
  -H "Content-Type: application/json" \
  -H "X-Webhook-Token: WRONG_TOKEN" \
  -d '{"name":"Jane Doe","email":"jane@example.com"}'
```

Expected result: HTTP 403 Forbidden.

## Test Evidence

Capture screenshots for:

- Workflow canvas
- Webhook configuration
- Authorized execution / 200 response
- Unauthorized execution / 403 response
- Normalized email and timestamp
- Test versus production webhook URL behavior

## Security

Do not commit the real webhook token, API keys, passwords, or other secrets. Use safe secret/credential management in n8n and mask sensitive values in screenshots.

## Implementation Note

The exported workflow should be tested after import. The current design includes a name-normalization expression that should be verified in n8n before production use. Replace any unsupported string-formatting expression with a supported n8n expression if necessary.

## Repository Structure

```text
realtime-webhook-event-processing-workflow/
├── README.md
├── workflow/
│   └── New_User_Webhook_Event_Processor.json
├── documentation/
│   └── Real-Time_Webhook_Event_Processing_Documentation.pdf
├── screenshots/
│   ├── workflow-canvas.png
│   ├── authorized-200.png
│   └── unauthorized-403.png
└── tests/
    └── test-cases.md
```
