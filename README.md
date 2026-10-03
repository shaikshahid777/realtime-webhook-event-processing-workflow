<!-- SHOWCASE_START --><div align="center">[![Typing](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=22&duration=2800&pause=900&color=58A6FF&center=true&vCenter=true&width=900&lines=realtime%20webhook%20event%20processing%20workflow;AI%20%7C%20Automation%20%7C%20Engineering;Explore%20the%20project%20%F0%9F%9A%80)](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow)<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,50:161B22,100:58A6FF&height=110&section=header&text=realtime-webhook-event-processing-workflow&fontSize=26&fontColor=FFFFFF&animation=twinkling&fontAlignY=65" width="100%" alt="Animated project banner"/>

[![Repository](https://img.shields.io/badge/Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow) [![Issues](https://img.shields.io/badge/Report-Issue-red?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/issues/new) [![Stars](https://img.shields.io/github/stars/shaikshahid777/realtime-webhook-event-processing-workflow?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/stargazers) [![Fork](https://img.shields.io/github/forks/shaikshahid777/realtime-webhook-event-processing-workflow?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/fork) [![Profile](https://img.shields.io/badge/Profile-Visit-0A66C2?style=for-the-badge&logo=github)](https://github.com/shaikshahid777)</div>

> ✨ **Project Showcase Mode:** animated banner • interactive navigation • live repository actions

[🚀 Repository](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow) · [🐞 Report Issue](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/issues/new) · [⭐ Star](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/stargazers) · [🔱 Fork](https://github.com/shaikshahid777/realtime-webhook-event-processing-workflow/fork) · [👤 Profile](https://github.com/shaikshahid777)

<!-- SHOWCASE_END -->

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
