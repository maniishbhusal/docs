# Pdflet Mintlify Documentation

## Context

This document contains the complete Mintlify documentation for **Pdflet** - a PDF API for developers. The documentation lives in a **separate repository** from the main Pdflet codebase and is deployed to `docs.pdflet.dev` via Mintlify.

### Repository Structure

```
pdflet-docs/           # Separate docs repository (connected to Mintlify)
├── mint.json          # Mintlify configuration
├── favicon.png        # Site favicon
├── introduction.mdx
├── quickstart.mdx
├── authentication.mdx
├── pricing.mdx
├── errors.mdx
├── api-reference/
│   ├── overview.mdx
│   ├── html-to-pdf.mdx
│   ├── get-conversion.mdx
│   └── api-keys.mdx
├── examples/
│   ├── invoices.mdx
│   └── reports.mdx
├── sdks/
│   ├── python.mdx
│   ├── javascript.mdx
│   └── curl.mdx
└── logo/
    ├── dark.png       # Logo for dark mode
    └── light.png      # Logo for light mode
```

### How to Use This Document

1. Create a new repository for your Mintlify docs (e.g., `pdflet-docs`)
2. Copy each file section below into the corresponding file in your docs repo
3. Add your logo files (`logo/dark.png`, `logo/light.png`) and `favicon.png`
4. Connect the repo to Mintlify via the dashboard
5. Commit and push - Mintlify auto-deploys on every push

---

# File Contents

## 1. `mint.json`

```json
{
  "$schema": "https://mintlify.com/schema.json",
  "name": "Pdflet",
  "logo": {
    "dark": "/logo/dark.png",
    "light": "/logo/light.png"
  },
  "favicon": "/favicon.png",
  "colors": {
    "primary": "#f05335",
    "light": "#ff6b4a",
    "dark": "#d9442c",
    "background": {
      "light": "#fff5eb",
      "dark": "#1a1a1a"
    }
  },
  "topbarLinks": [
    {
      "name": "Dashboard",
      "url": "https://pdflet.dev/dashboard"
    }
  ],
  "topbarCtaButton": {
    "name": "Get Started",
    "url": "https://pdflet.dev/signup"
  },
  "tabs": [
    {
      "name": "API Reference",
      "url": "api-reference"
    }
  ],
  "anchors": [
    {
      "name": "GitHub",
      "icon": "github",
      "url": "https://github.com/pdflet"
    },
    {
      "name": "Support",
      "icon": "envelope",
      "url": "mailto:support@pdflet.dev"
    }
  ],
  "navigation": [
    {
      "group": "Getting Started",
      "pages": ["introduction", "quickstart", "authentication"]
    },
    {
      "group": "API Reference",
      "pages": [
        "api-reference/overview",
        "api-reference/html-to-pdf",
        "api-reference/get-conversion",
        "api-reference/api-keys"
      ]
    },
    {
      "group": "Examples",
      "pages": [
        "examples/invoices",
        "examples/reports"
      ]
    },
    {
      "group": "SDKs & Libraries",
      "pages": [
        "sdks/python",
        "sdks/javascript",
        "sdks/curl"
      ]
    },
    {
      "group": "Resources",
      "pages": ["pricing", "errors"]
    }
  ],
  "footerSocials": {
    "twitter": "https://twitter.com/pdflet",
    "github": "https://github.com/pdflet"
  },
  "api": {
    "baseUrl": "https://api.pdflet.dev/api/v1"
  }
}
```

---

## 2. `introduction.mdx`

```mdx
---
title: 'Introduction'
description: 'Convert HTML to PDF with a simple API'
---

# Welcome to Pdflet

Pdflet is a PDF generation API built for developers. Convert HTML to high-quality PDFs with a single API call.

## Why Pdflet?

<CardGroup cols={2}>
  <Card title="Simple Integration" icon="code">
    One POST request to convert HTML to PDF. No complex setup or configuration required.
  </Card>
  <Card title="High Quality Output" icon="file-pdf">
    Powered by Chromium for pixel-perfect rendering. Your PDFs look exactly like your HTML.
  </Card>
  <Card title="Fast & Reliable" icon="bolt">
    Average conversion time under 3 seconds. 99.9% uptime SLA on paid plans.
  </Card>
  <Card title="Developer First" icon="terminal">
    RESTful API with comprehensive documentation. SDKs for Python, JavaScript, and more.
  </Card>
</CardGroup>

## Common Use Cases

- **Invoices & Receipts** - Generate professional invoices from your billing data
- **Reports** - Create PDF reports from dashboards and analytics
- **Contracts** - Convert dynamic contracts and agreements to PDF
- **Certificates** - Generate certificates, tickets, and badges at scale

## How It Works

<Steps>
  <Step title="Send HTML">
    POST your HTML content or URL to our API endpoint
  </Step>
  <Step title="We Render">
    Our servers render your HTML using a headless browser
  </Step>
  <Step title="Get PDF">
    Download your PDF from the returned URL
  </Step>
</Steps>

## Quick Example

```bash
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{"html": "<h1>Hello World</h1>"}'
```

Response:

```json
{
  "id": "conv_abc123",
  "status": "pending",
  "created_at": "2024-01-15T10:30:00Z"
}
```

<Card title="Ready to start?" icon="rocket" href="/quickstart">
  Follow our quickstart guide to generate your first PDF in 5 minutes
</Card>
```

---

## 3. `quickstart.mdx`

```mdx
---
title: 'Quickstart'
description: 'Generate your first PDF in 5 minutes'
---

# Quickstart

This guide will walk you through generating your first PDF with Pdflet.

## Prerequisites

- A Pdflet account ([sign up free](https://pdflet.dev/signup))
- An API key (created in your [dashboard](https://pdflet.dev/dashboard/api-keys))

## Step 1: Get Your API Key

<Steps>
  <Step title="Sign Up">
    Create a free account at [pdflet.dev/signup](https://pdflet.dev/signup)
  </Step>
  <Step title="Go to API Keys">
    Navigate to **Dashboard → API Keys**
  </Step>
  <Step title="Create a Key">
    Click **Create API Key**, give it a name, and copy the key
  </Step>
</Steps>

<Warning>
  Your API key is only shown once. Store it securely - you'll need it for all API requests.
</Warning>

## Step 2: Make Your First Request

Convert a simple HTML string to PDF:

<CodeGroup>
```bash cURL
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "html": "<html><body><h1>My First PDF</h1><p>Generated with Pdflet!</p></body></html>"
  }'
```

```python Python
import requests

response = requests.post(
    "https://api.pdflet.dev/api/v1/pdf/",
    headers={"X-API-Key": "pk_live_your_api_key"},
    json={"html": "<h1>My First PDF</h1><p>Generated with Pdflet!</p>"}
)

data = response.json()
print(f"Conversion ID: {data['id']}")
```

```javascript JavaScript
const response = await fetch('https://api.pdflet.dev/api/v1/pdf/', {
  method: 'POST',
  headers: {
    'X-API-Key': 'pk_live_your_api_key',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    html: '<h1>My First PDF</h1><p>Generated with Pdflet!</p>'
  })
});

const data = await response.json();
console.log(`Conversion ID: ${data.id}`);
```
</CodeGroup>

## Step 3: Check Conversion Status

PDF generation is asynchronous. Poll the conversion endpoint to check status:

<CodeGroup>
```bash cURL
curl https://api.pdflet.dev/api/v1/conversions/conv_abc123/ \
  -H "X-API-Key: pk_live_your_api_key"
```

```python Python
import time

conversion_id = data['id']

while True:
    status_response = requests.get(
        f"https://api.pdflet.dev/api/v1/conversions/{conversion_id}/",
        headers={"X-API-Key": "pk_live_your_api_key"}
    )
    status_data = status_response.json()

    if status_data['status'] == 'completed':
        print(f"PDF ready: {status_data['file_url']}")
        break
    elif status_data['status'] == 'failed':
        print(f"Error: {status_data['error_message']}")
        break

    time.sleep(1)
```

```javascript JavaScript
const conversionId = data.id;

const checkStatus = async () => {
  const response = await fetch(
    `https://api.pdflet.dev/api/v1/conversions/${conversionId}/`,
    { headers: { 'X-API-Key': 'pk_live_your_api_key' } }
  );
  return response.json();
};

// Poll until complete
let result;
do {
  result = await checkStatus();
  if (result.status === 'pending') {
    await new Promise(r => setTimeout(r, 1000));
  }
} while (result.status === 'pending');

console.log(`PDF URL: ${result.file_url}`);
```
</CodeGroup>

## Step 4: Download Your PDF

Once the status is `completed`, the response includes a `file_url`. Download your PDF:

```bash
curl -O "https://api.pdflet.dev/media/pdfs/conv_abc123.pdf"
```

## Next Steps

<CardGroup cols={2}>
  <Card title="Authentication" icon="key" href="/authentication">
    Learn about API keys and JWT authentication
  </Card>
  <Card title="PDF Options" icon="sliders" href="/api-reference/html-to-pdf">
    Customize page size, margins, headers, and more
  </Card>
  <Card title="Examples" icon="code" href="/examples/invoices">
    See real-world examples for invoices, reports, and more
  </Card>
  <Card title="SDKs" icon="cube" href="/sdks/python">
    Use our official SDKs for easier integration
  </Card>
</CardGroup>
```

---

## 4. `authentication.mdx`

```mdx
---
title: 'Authentication'
description: 'Secure your API requests with API keys or JWT tokens'
---

# Authentication

Pdflet supports two authentication methods: **API Keys** (recommended) and **JWT Tokens**.

## API Keys (Recommended)

API keys are the simplest way to authenticate. Include your key in the `X-API-Key` header:

```bash
curl https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{"html": "<h1>Hello</h1>"}'
```

### Creating API Keys

1. Log in to your [Pdflet Dashboard](https://pdflet.dev/dashboard)
2. Navigate to **API Keys**
3. Click **Create API Key**
4. Enter a descriptive name (e.g., "Production Server")
5. Copy and securely store your key

<Warning>
  API keys are shown only once. If you lose a key, revoke it and create a new one.
</Warning>

### API Key Format

API keys follow this format:
- **Live keys**: `pk_live_` prefix (32 characters total)
- Example: `pk_live_a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`

### Best Practices

<AccordionGroup>
  <Accordion title="Use environment variables">
    Never hardcode API keys in your source code:
    ```python
    import os
    api_key = os.environ.get('PDFLET_API_KEY')
    ```
  </Accordion>
  <Accordion title="Use separate keys per environment">
    Create different keys for development, staging, and production
  </Accordion>
  <Accordion title="Rotate keys periodically">
    Revoke and replace keys every 90 days for security
  </Accordion>
  <Accordion title="Limit key permissions">
    Create keys with only the permissions you need
  </Accordion>
</AccordionGroup>

## JWT Authentication

For web applications where users interact directly, use JWT (JSON Web Token) authentication.

### Obtaining Tokens

```bash
curl -X POST https://api.pdflet.dev/api/v1/auth/jwt/create/ \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "your_password"}'
```

Response:

```json
{
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}
```

### Using Access Tokens

Include the access token in the `Authorization` header:

```bash
curl https://api.pdflet.dev/api/v1/pdf/ \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..." \
  -H "Content-Type: application/json" \
  -d '{"html": "<h1>Hello</h1>"}'
```

### Refreshing Tokens

Access tokens expire after 5 minutes. Use the refresh token to get a new access token:

```bash
curl -X POST https://api.pdflet.dev/api/v1/auth/jwt/refresh/ \
  -H "Content-Type: application/json" \
  -d '{"refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."}'
```

### Token Lifetimes

| Token Type | Lifetime |
|------------|----------|
| Access Token | 5 minutes |
| Refresh Token | 1 day |

## Which Should I Use?

| Use Case | Recommended Method |
|----------|-------------------|
| Backend server-to-server | API Key |
| CLI tools or scripts | API Key |
| Web application (frontend) | JWT |
| Mobile application | JWT |
| Microservices | API Key |

<Info>
  API keys are simpler but cannot be revoked per-session. JWT tokens offer more granular control for user-facing applications.
</Info>
```

---

## 5. `api-reference/overview.mdx`

```mdx
---
title: 'API Overview'
description: 'RESTful API conventions and base URL'
---

# API Overview

The Pdflet API is a RESTful JSON API for generating PDFs from HTML content.

## Base URL

All API requests should be made to:

```
https://api.pdflet.dev/api/v1
```

## Request Format

- All requests must include a `Content-Type: application/json` header
- Request bodies must be valid JSON
- Authentication is required for all endpoints

## Response Format

All responses return JSON with consistent structure:

### Success Response

```json
{
  "id": "conv_abc123",
  "status": "completed",
  "file_url": "https://api.pdflet.dev/media/pdfs/conv_abc123.pdf",
  "created_at": "2024-01-15T10:30:00Z"
}
```

### Error Response

```json
{
  "error": "validation_error",
  "message": "Invalid page size",
  "details": {
    "page_size": ["Must be one of: A4, Letter, Legal, A3, A5"]
  }
}
```

## HTTP Status Codes

| Code | Description |
|------|-------------|
| `200` | Success |
| `201` | Created |
| `202` | Accepted (async processing started) |
| `400` | Bad Request - Invalid parameters |
| `401` | Unauthorized - Invalid or missing authentication |
| `402` | Payment Required - No credits remaining |
| `404` | Not Found - Resource doesn't exist |
| `429` | Too Many Requests - Rate limit exceeded |
| `500` | Internal Server Error |

## Rate Limits

Rate limits vary by plan:

| Plan | Requests per Minute |
|------|---------------------|
| Free | 10 |
| Starter | 30 |
| Pro | 100 |

Rate limit headers are included in every response:

```
X-RateLimit-Limit: 30
X-RateLimit-Remaining: 29
X-RateLimit-Reset: 1705320000
```

## Pagination

List endpoints support pagination via query parameters:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `page` | 1 | Page number |
| `page_size` | 20 | Items per page (max 100) |

```bash
GET /api/v1/api-keys/?page=2&page_size=10
```

## Idempotency

For safe retries, include an `Idempotency-Key` header:

```bash
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Idempotency-Key: unique-request-id-123" \
  -H "Content-Type: application/json" \
  -d '{"html": "<h1>Hello</h1>"}'
```

Requests with the same idempotency key within 24 hours return the cached response.
```

---

## 6. `api-reference/html-to-pdf.mdx`

```mdx
---
title: 'Convert HTML to PDF'
description: 'Create a PDF from HTML content'
api: 'POST /pdf/'
---

# Convert HTML to PDF

Convert HTML content to a PDF document.

<Note>
  This endpoint returns immediately with a `202 Accepted` status. The PDF is generated asynchronously. Use the [Get Conversion](/api-reference/get-conversion) endpoint to check status and retrieve the PDF URL.
</Note>

## Request

<ParamField body="html" type="string" required>
  HTML content to convert. Must be valid HTML.
</ParamField>

<ParamField body="url" type="string">
  URL to render instead of HTML content. Cannot be used with `html`.
</ParamField>

<ParamField body="page_size" type="string" default="A4">
  Page size. Options: `A4`, `Letter`, `Legal`, `A3`, `A5`
</ParamField>

<ParamField body="landscape" type="boolean" default="false">
  Render in landscape orientation
</ParamField>

<ParamField body="margin_top" type="string" default="1cm">
  Top margin (CSS units: `px`, `cm`, `in`, `mm`)
</ParamField>

<ParamField body="margin_bottom" type="string" default="1cm">
  Bottom margin
</ParamField>

<ParamField body="margin_left" type="string" default="1cm">
  Left margin
</ParamField>

<ParamField body="margin_right" type="string" default="1cm">
  Right margin
</ParamField>

<ParamField body="print_background" type="boolean" default="true">
  Include background colors and images
</ParamField>

<ParamField body="scale" type="number" default="1.0">
  Scale factor (0.1 to 2.0)
</ParamField>

## Response

<ResponseField name="id" type="string">
  Unique conversion identifier
</ResponseField>

<ResponseField name="status" type="string">
  Conversion status: `pending`, `processing`, `completed`, `failed`
</ResponseField>

<ResponseField name="created_at" type="string">
  ISO 8601 timestamp
</ResponseField>

## Examples

### Basic HTML Conversion

<CodeGroup>
```bash cURL
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "html": "<html><body><h1>Hello World</h1></body></html>"
  }'
```

```python Python
import requests

response = requests.post(
    "https://api.pdflet.dev/api/v1/pdf/",
    headers={"X-API-Key": "pk_live_your_api_key"},
    json={"html": "<html><body><h1>Hello World</h1></body></html>"}
)

print(response.json())
```

```javascript JavaScript
const response = await fetch('https://api.pdflet.dev/api/v1/pdf/', {
  method: 'POST',
  headers: {
    'X-API-Key': 'pk_live_your_api_key',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    html: '<html><body><h1>Hello World</h1></body></html>'
  })
});

const data = await response.json();
```
</CodeGroup>

### With Custom Options

```bash
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: pk_live_your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "html": "<html><body><h1>Report</h1></body></html>",
    "page_size": "Letter",
    "landscape": true,
    "margin_top": "2cm",
    "margin_bottom": "2cm",
    "print_background": true
  }'
```

### Response

```json
{
  "id": "conv_abc123def456",
  "status": "pending",
  "created_at": "2024-01-15T10:30:00Z"
}
```

## Error Responses

### Invalid HTML

```json
{
  "error": "validation_error",
  "message": "Either 'html' or 'url' is required"
}
```

### No Credits

```json
{
  "error": "insufficient_credits",
  "message": "You have no credits remaining. Please upgrade your plan."
}
```
```

---

## 7. `api-reference/get-conversion.mdx`

```mdx
---
title: 'Get Conversion'
description: 'Check conversion status and get the PDF URL'
api: 'GET /conversions/{id}/'
---

# Get Conversion Status

Retrieve the status and result of a PDF conversion.

## Request

<ParamField path="id" type="string" required>
  The conversion ID returned from the create PDF endpoint
</ParamField>

## Response

<ResponseField name="id" type="string">
  Unique conversion identifier
</ResponseField>

<ResponseField name="status" type="string">
  Conversion status:
  - `pending` - Queued for processing
  - `processing` - Currently rendering
  - `completed` - PDF ready for download
  - `failed` - Conversion failed
</ResponseField>

<ResponseField name="file_url" type="string">
  URL to download the PDF (only present when `status` is `completed`)
</ResponseField>

<ResponseField name="error_message" type="string">
  Error details (only present when `status` is `failed`)
</ResponseField>

<ResponseField name="created_at" type="string">
  ISO 8601 timestamp of when the conversion was created
</ResponseField>

<ResponseField name="completed_at" type="string">
  ISO 8601 timestamp of when the conversion completed
</ResponseField>

## Examples

<CodeGroup>
```bash cURL
curl https://api.pdflet.dev/api/v1/conversions/conv_abc123/ \
  -H "X-API-Key: pk_live_your_api_key"
```

```python Python
import requests

response = requests.get(
    "https://api.pdflet.dev/api/v1/conversions/conv_abc123/",
    headers={"X-API-Key": "pk_live_your_api_key"}
)

data = response.json()
if data['status'] == 'completed':
    print(f"PDF URL: {data['file_url']}")
```

```javascript JavaScript
const response = await fetch(
  'https://api.pdflet.dev/api/v1/conversions/conv_abc123/',
  { headers: { 'X-API-Key': 'pk_live_your_api_key' } }
);

const data = await response.json();
if (data.status === 'completed') {
  console.log(`PDF URL: ${data.file_url}`);
}
```
</CodeGroup>

### Pending Response

```json
{
  "id": "conv_abc123",
  "status": "pending",
  "created_at": "2024-01-15T10:30:00Z"
}
```

### Completed Response

```json
{
  "id": "conv_abc123",
  "status": "completed",
  "file_url": "https://api.pdflet.dev/media/pdfs/conv_abc123.pdf",
  "created_at": "2024-01-15T10:30:00Z",
  "completed_at": "2024-01-15T10:30:02Z"
}
```

### Failed Response

```json
{
  "id": "conv_abc123",
  "status": "failed",
  "error_message": "Failed to render HTML: Invalid CSS syntax",
  "created_at": "2024-01-15T10:30:00Z"
}
```

## Polling Pattern

Since conversions are asynchronous, implement polling to wait for completion:

```python
import time
import requests

def wait_for_pdf(conversion_id, api_key, timeout=30):
    """Poll until PDF is ready or timeout."""
    start = time.time()

    while time.time() - start < timeout:
        response = requests.get(
            f"https://api.pdflet.dev/api/v1/conversions/{conversion_id}/",
            headers={"X-API-Key": api_key}
        )
        data = response.json()

        if data['status'] == 'completed':
            return data['file_url']
        elif data['status'] == 'failed':
            raise Exception(data['error_message'])

        time.sleep(1)  # Poll every second

    raise TimeoutError("PDF generation timed out")
```

<Tip>
  Most conversions complete within 2-5 seconds. Start with a 1-second polling interval.
</Tip>
```

---

## 8. `api-reference/api-keys.mdx`

```mdx
---
title: 'API Keys'
description: 'Manage your API keys programmatically'
---

# API Keys

Create, list, and revoke API keys for authentication.

## List API Keys

<api method="GET" path="/api-keys/" />

Returns all API keys for the authenticated user.

### Response

```json
[
  {
    "id": "key_abc123",
    "name": "Production Server",
    "prefix": "pk_live_a1b2c3",
    "created_at": "2024-01-15T10:30:00Z",
    "last_used_at": "2024-01-16T14:22:00Z"
  }
]
```

<Note>
  For security, only the key prefix is returned. The full key is only shown once when created.
</Note>

---

## Create API Key

<api method="POST" path="/api-keys/" />

Create a new API key.

### Request

<ParamField body="name" type="string" required>
  A descriptive name for the key (e.g., "Production Server")
</ParamField>

### Response

```json
{
  "id": "key_abc123",
  "name": "Production Server",
  "key": "pk_live_a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6",
  "created_at": "2024-01-15T10:30:00Z"
}
```

<Warning>
  The full `key` value is only returned once. Store it securely immediately.
</Warning>

### Example

<CodeGroup>
```bash cURL
curl -X POST https://api.pdflet.dev/api/v1/api-keys/ \
  -H "Authorization: Bearer your_jwt_token" \
  -H "Content-Type: application/json" \
  -d '{"name": "Production Server"}'
```

```python Python
import requests

response = requests.post(
    "https://api.pdflet.dev/api/v1/api-keys/",
    headers={"Authorization": "Bearer your_jwt_token"},
    json={"name": "Production Server"}
)

key_data = response.json()
print(f"Save this key: {key_data['key']}")
```
</CodeGroup>

---

## Delete API Key

<api method="DELETE" path="/api-keys/{id}/" />

Revoke an API key. This action cannot be undone.

### Parameters

<ParamField path="id" type="string" required>
  The API key ID to delete
</ParamField>

### Response

Returns `204 No Content` on success.

### Example

```bash
curl -X DELETE https://api.pdflet.dev/api/v1/api-keys/key_abc123/ \
  -H "Authorization: Bearer your_jwt_token"
```

<Warning>
  Revoking a key immediately invalidates it. Any requests using this key will fail with `401 Unauthorized`.
</Warning>
```

---

## 9. `examples/invoices.mdx`

```mdx
---
title: 'Invoice Generation'
description: 'Generate professional invoices with Pdflet'
---

# Invoice Generation

Generate professional, branded invoices from your application data.

## Invoice Template

Here's a complete HTML invoice template:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      color: #1a1a1a;
      padding: 40px;
    }
    .header {
      display: flex;
      justify-content: space-between;
      margin-bottom: 40px;
    }
    .logo { font-size: 24px; font-weight: bold; color: #f05335; }
    .invoice-title { font-size: 32px; color: #666; }
    .info-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 40px;
      margin-bottom: 40px;
    }
    .info-block h3 {
      font-size: 12px;
      text-transform: uppercase;
      color: #666;
      margin-bottom: 8px;
    }
    table { width: 100%; border-collapse: collapse; margin-bottom: 40px; }
    th {
      text-align: left;
      padding: 12px;
      border-bottom: 2px solid #1a1a1a;
      font-size: 12px;
      text-transform: uppercase;
    }
    td { padding: 12px; border-bottom: 1px solid #eee; }
    .amount { text-align: right; }
    .totals {
      width: 300px;
      margin-left: auto;
    }
    .totals tr td { border: none; padding: 8px 12px; }
    .totals .total {
      font-size: 18px;
      font-weight: bold;
      border-top: 2px solid #1a1a1a;
    }
    .footer {
      margin-top: 60px;
      padding-top: 20px;
      border-top: 1px solid #eee;
      font-size: 12px;
      color: #666;
    }
  </style>
</head>
<body>
  <div class="header">
    <div class="logo">Your Company</div>
    <div class="invoice-title">INVOICE</div>
  </div>

  <div class="info-grid">
    <div class="info-block">
      <h3>Bill To</h3>
      <p><strong>{{customer_name}}</strong></p>
      <p>{{customer_address}}</p>
      <p>{{customer_email}}</p>
    </div>
    <div class="info-block" style="text-align: right;">
      <h3>Invoice Details</h3>
      <p><strong>Invoice #:</strong> {{invoice_number}}</p>
      <p><strong>Date:</strong> {{invoice_date}}</p>
      <p><strong>Due Date:</strong> {{due_date}}</p>
    </div>
  </div>

  <table>
    <thead>
      <tr>
        <th>Description</th>
        <th>Qty</th>
        <th class="amount">Unit Price</th>
        <th class="amount">Amount</th>
      </tr>
    </thead>
    <tbody>
      {{#each items}}
      <tr>
        <td>{{description}}</td>
        <td>{{quantity}}</td>
        <td class="amount">${{unit_price}}</td>
        <td class="amount">${{amount}}</td>
      </tr>
      {{/each}}
    </tbody>
  </table>

  <table class="totals">
    <tr>
      <td>Subtotal</td>
      <td class="amount">${{subtotal}}</td>
    </tr>
    <tr>
      <td>Tax (10%)</td>
      <td class="amount">${{tax}}</td>
    </tr>
    <tr class="total">
      <td>Total</td>
      <td class="amount">${{total}}</td>
    </tr>
  </table>

  <div class="footer">
    <p>Thank you for your business!</p>
    <p>Payment is due within 30 days. Please include invoice number with payment.</p>
  </div>
</body>
</html>
```

## Python Example

```python
import requests
from jinja2 import Template

# Your invoice data
invoice_data = {
    "customer_name": "Acme Corp",
    "customer_address": "123 Business St, Suite 100",
    "customer_email": "billing@acme.com",
    "invoice_number": "INV-2024-001",
    "invoice_date": "January 15, 2024",
    "due_date": "February 14, 2024",
    "items": [
        {"description": "API Access - Pro Plan", "quantity": 1, "unit_price": "29.00", "amount": "29.00"},
        {"description": "Additional Credits (1000)", "quantity": 2, "unit_price": "10.00", "amount": "20.00"},
    ],
    "subtotal": "49.00",
    "tax": "4.90",
    "total": "53.90"
}

# Load and render template
with open("invoice_template.html") as f:
    template = Template(f.read())

html = template.render(**invoice_data)

# Generate PDF
response = requests.post(
    "https://api.pdflet.dev/api/v1/pdf/",
    headers={"X-API-Key": "pk_live_your_api_key"},
    json={
        "html": html,
        "page_size": "Letter",
        "margin_top": "0.5in",
        "margin_bottom": "0.5in"
    }
)

conversion_id = response.json()["id"]
print(f"Invoice PDF queued: {conversion_id}")
```

## JavaScript Example

```javascript
import Handlebars from 'handlebars';
import fs from 'fs';

const invoiceData = {
  customer_name: "Acme Corp",
  customer_address: "123 Business St, Suite 100",
  customer_email: "billing@acme.com",
  invoice_number: "INV-2024-001",
  invoice_date: "January 15, 2024",
  due_date: "February 14, 2024",
  items: [
    { description: "API Access - Pro Plan", quantity: 1, unit_price: "29.00", amount: "29.00" },
    { description: "Additional Credits (1000)", quantity: 2, unit_price: "10.00", amount: "20.00" },
  ],
  subtotal: "49.00",
  tax: "4.90",
  total: "53.90"
};

const templateSource = fs.readFileSync('invoice_template.html', 'utf8');
const template = Handlebars.compile(templateSource);
const html = template(invoiceData);

const response = await fetch('https://api.pdflet.dev/api/v1/pdf/', {
  method: 'POST',
  headers: {
    'X-API-Key': 'pk_live_your_api_key',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    html,
    page_size: 'Letter',
    margin_top: '0.5in',
    margin_bottom: '0.5in'
  })
});

const { id } = await response.json();
console.log(`Invoice PDF queued: ${id}`);
```

## Tips for Better Invoices

<CardGroup cols={2}>
  <Card title="Use web fonts" icon="font">
    Include Google Fonts via `@import` for professional typography
  </Card>
  <Card title="Print-friendly CSS" icon="print">
    Use `@media print` for PDF-specific styles
  </Card>
  <Card title="Fixed dimensions" icon="ruler">
    Use absolute units (px, cm, in) for consistent layout
  </Card>
  <Card title="Embed images as base64" icon="image">
    Inline images with data URIs for reliable rendering
  </Card>
</CardGroup>
```

---

## 10. `examples/reports.mdx`

```mdx
---
title: 'Report Generation'
description: 'Create data-driven PDF reports'
---

# Report Generation

Generate PDF reports with charts, tables, and dynamic data.

## Report Template

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, sans-serif;
      padding: 40px;
      color: #1a1a1a;
    }
    .header {
      border-bottom: 3px solid #f05335;
      padding-bottom: 20px;
      margin-bottom: 30px;
    }
    h1 { margin: 0; color: #1a1a1a; }
    .date { color: #666; font-size: 14px; }
    .metrics {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
      margin-bottom: 40px;
    }
    .metric {
      background: #f8f9fa;
      padding: 20px;
      border-radius: 8px;
    }
    .metric-value { font-size: 32px; font-weight: bold; }
    .metric-label { font-size: 12px; color: #666; text-transform: uppercase; }
    .chart-container {
      height: 300px;
      margin-bottom: 40px;
    }
    table { width: 100%; border-collapse: collapse; }
    th, td {
      padding: 12px;
      text-align: left;
      border-bottom: 1px solid #eee;
    }
    th {
      background: #f8f9fa;
      font-weight: 600;
    }
  </style>
</head>
<body>
  <div class="header">
    <h1>Monthly Performance Report</h1>
    <p class="date">Generated on {{report_date}}</p>
  </div>

  <div class="metrics">
    <div class="metric">
      <div class="metric-value">{{total_conversions}}</div>
      <div class="metric-label">Total Conversions</div>
    </div>
    <div class="metric">
      <div class="metric-value">{{success_rate}}%</div>
      <div class="metric-label">Success Rate</div>
    </div>
    <div class="metric">
      <div class="metric-value">{{avg_time}}s</div>
      <div class="metric-label">Avg Response Time</div>
    </div>
    <div class="metric">
      <div class="metric-value">{{active_users}}</div>
      <div class="metric-label">Active Users</div>
    </div>
  </div>

  <h2>Usage Over Time</h2>
  <div class="chart-container">
    <canvas id="usageChart"></canvas>
  </div>

  <h2>Top Endpoints</h2>
  <table>
    <thead>
      <tr>
        <th>Endpoint</th>
        <th>Requests</th>
        <th>Avg Latency</th>
        <th>Error Rate</th>
      </tr>
    </thead>
    <tbody>
      {{#each endpoints}}
      <tr>
        <td>{{name}}</td>
        <td>{{requests}}</td>
        <td>{{latency}}ms</td>
        <td>{{error_rate}}%</td>
      </tr>
      {{/each}}
    </tbody>
  </table>

  <script>
    const ctx = document.getElementById('usageChart').getContext('2d');
    new Chart(ctx, {
      type: 'line',
      data: {
        labels: {{chart_labels}},
        datasets: [{
          label: 'API Requests',
          data: {{chart_data}},
          borderColor: '#f05335',
          tension: 0.3
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        animation: false // Important for PDF rendering
      }
    });
  </script>
</body>
</html>
```

## Python Example with Charts

```python
import requests
import json
from datetime import datetime, timedelta

# Generate report data
report_data = {
    "report_date": datetime.now().strftime("%B %d, %Y"),
    "total_conversions": "12,847",
    "success_rate": "99.2",
    "avg_time": "2.3",
    "active_users": "1,234",
    "endpoints": [
        {"name": "/pdf/", "requests": "8,234", "latency": "2100", "error_rate": "0.5"},
        {"name": "/conversions/", "requests": "4,613", "latency": "45", "error_rate": "0.1"},
    ],
    "chart_labels": json.dumps(["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]),
    "chart_data": json.dumps([1200, 1900, 1700, 2100, 2400, 800, 600])
}

# Render template with data
from jinja2 import Template
with open("report_template.html") as f:
    template = Template(f.read())
html = template.render(**report_data)

# Generate PDF
response = requests.post(
    "https://api.pdflet.dev/api/v1/pdf/",
    headers={"X-API-Key": "pk_live_your_api_key"},
    json={
        "html": html,
        "page_size": "A4",
        "landscape": True,
        "print_background": True
    }
)

print(response.json())
```

## Tips for Reports

<Tip>
  Set `animation: false` in Chart.js options to ensure charts render correctly in PDFs.
</Tip>

- **Use CDN scripts** - External scripts are loaded before rendering
- **Landscape for dashboards** - Wide reports work better in landscape
- **Print backgrounds** - Enable `print_background` for colored elements
- **Page breaks** - Use `page-break-before: always` for multi-page reports
```

---

## 11. `sdks/python.mdx`

```mdx
---
title: 'Python'
description: 'Python code examples for Pdflet API'
---

# Python Examples

Python code examples using the `requests` library.

## Installation

```bash
pip install requests
```

## Configuration

```python
import requests
import os

PDFLET_API_KEY = os.environ.get("PDFLET_API_KEY")
BASE_URL = "https://api.pdflet.dev/api/v1"

headers = {
    "X-API-Key": PDFLET_API_KEY,
    "Content-Type": "application/json"
}
```

## Generate PDF

```python
def create_pdf(html: str, **options) -> dict:
    """Create a PDF from HTML content."""
    response = requests.post(
        f"{BASE_URL}/pdf/",
        headers=headers,
        json={"html": html, **options}
    )
    response.raise_for_status()
    return response.json()

# Usage
result = create_pdf(
    html="<h1>Hello World</h1>",
    page_size="A4",
    margin_top="2cm"
)
print(f"Conversion ID: {result['id']}")
```

## Wait for Completion

```python
import time

def wait_for_pdf(conversion_id: str, timeout: int = 60) -> str:
    """Poll until PDF is ready and return the download URL."""
    start = time.time()

    while time.time() - start < timeout:
        response = requests.get(
            f"{BASE_URL}/conversions/{conversion_id}/",
            headers=headers
        )
        response.raise_for_status()
        data = response.json()

        if data["status"] == "completed":
            return data["file_url"]
        elif data["status"] == "failed":
            raise Exception(f"Conversion failed: {data.get('error_message')}")

        time.sleep(1)

    raise TimeoutError("PDF generation timed out")

# Usage
pdf_url = wait_for_pdf(result["id"])
print(f"PDF ready: {pdf_url}")
```

## Download PDF

```python
def download_pdf(url: str, filename: str) -> None:
    """Download a PDF to a local file."""
    response = requests.get(url, headers=headers)
    response.raise_for_status()

    with open(filename, "wb") as f:
        f.write(response.content)

    print(f"Downloaded: {filename}")

# Usage
download_pdf(pdf_url, "output.pdf")
```

## Complete Example

```python
import requests
import time
import os

class PdfletClient:
    def __init__(self, api_key: str):
        self.api_key = api_key
        self.base_url = "https://api.pdflet.dev/api/v1"
        self.headers = {
            "X-API-Key": api_key,
            "Content-Type": "application/json"
        }

    def html_to_pdf(self, html: str, **options) -> bytes:
        """Convert HTML to PDF and return the PDF bytes."""
        # Start conversion
        response = requests.post(
            f"{self.base_url}/pdf/",
            headers=self.headers,
            json={"html": html, **options}
        )
        response.raise_for_status()
        conversion_id = response.json()["id"]

        # Wait for completion
        for _ in range(60):
            status_response = requests.get(
                f"{self.base_url}/conversions/{conversion_id}/",
                headers=self.headers
            )
            status_response.raise_for_status()
            data = status_response.json()

            if data["status"] == "completed":
                # Download PDF
                pdf_response = requests.get(data["file_url"])
                return pdf_response.content
            elif data["status"] == "failed":
                raise Exception(data.get("error_message", "Unknown error"))

            time.sleep(1)

        raise TimeoutError("Conversion timed out")

# Usage
client = PdfletClient(os.environ["PDFLET_API_KEY"])

pdf_bytes = client.html_to_pdf(
    html="<h1>Invoice #123</h1><p>Total: $99.00</p>",
    page_size="Letter"
)

with open("invoice.pdf", "wb") as f:
    f.write(pdf_bytes)
```

## Error Handling

```python
from requests.exceptions import HTTPError

try:
    result = create_pdf("<h1>Test</h1>")
except HTTPError as e:
    if e.response.status_code == 401:
        print("Invalid API key")
    elif e.response.status_code == 402:
        print("No credits remaining")
    elif e.response.status_code == 429:
        print("Rate limit exceeded")
    else:
        print(f"Error: {e.response.json()}")
```
```

---

## 12. `sdks/javascript.mdx`

```mdx
---
title: 'JavaScript'
description: 'JavaScript/Node.js code examples for Pdflet API'
---

# JavaScript Examples

JavaScript examples for Node.js and browser environments.

## Node.js Setup

```javascript
const PDFLET_API_KEY = process.env.PDFLET_API_KEY;
const BASE_URL = 'https://api.pdflet.dev/api/v1';

const headers = {
  'X-API-Key': PDFLET_API_KEY,
  'Content-Type': 'application/json'
};
```

## Generate PDF

```javascript
async function createPdf(html, options = {}) {
  const response = await fetch(`${BASE_URL}/pdf/`, {
    method: 'POST',
    headers,
    body: JSON.stringify({ html, ...options })
  });

  if (!response.ok) {
    throw new Error(`API error: ${response.status}`);
  }

  return response.json();
}

// Usage
const result = await createPdf('<h1>Hello World</h1>', {
  page_size: 'A4',
  margin_top: '2cm'
});
console.log(`Conversion ID: ${result.id}`);
```

## Wait for Completion

```javascript
async function waitForPdf(conversionId, timeout = 60000) {
  const start = Date.now();

  while (Date.now() - start < timeout) {
    const response = await fetch(
      `${BASE_URL}/conversions/${conversionId}/`,
      { headers }
    );

    const data = await response.json();

    if (data.status === 'completed') {
      return data.file_url;
    } else if (data.status === 'failed') {
      throw new Error(data.error_message || 'Conversion failed');
    }

    await new Promise(r => setTimeout(r, 1000));
  }

  throw new Error('Conversion timed out');
}

// Usage
const pdfUrl = await waitForPdf(result.id);
console.log(`PDF ready: ${pdfUrl}`);
```

## Complete Client Class

```javascript
class PdfletClient {
  constructor(apiKey) {
    this.apiKey = apiKey;
    this.baseUrl = 'https://api.pdflet.dev/api/v1';
  }

  get headers() {
    return {
      'X-API-Key': this.apiKey,
      'Content-Type': 'application/json'
    };
  }

  async htmlToPdf(html, options = {}) {
    // Start conversion
    const createResponse = await fetch(`${this.baseUrl}/pdf/`, {
      method: 'POST',
      headers: this.headers,
      body: JSON.stringify({ html, ...options })
    });

    if (!createResponse.ok) {
      const error = await createResponse.json();
      throw new Error(error.message || 'Failed to create conversion');
    }

    const { id } = await createResponse.json();

    // Poll for completion
    for (let i = 0; i < 60; i++) {
      const statusResponse = await fetch(
        `${this.baseUrl}/conversions/${id}/`,
        { headers: this.headers }
      );

      const data = await statusResponse.json();

      if (data.status === 'completed') {
        return data.file_url;
      } else if (data.status === 'failed') {
        throw new Error(data.error_message);
      }

      await new Promise(r => setTimeout(r, 1000));
    }

    throw new Error('Conversion timed out');
  }
}

// Usage
const client = new PdfletClient(process.env.PDFLET_API_KEY);

const pdfUrl = await client.htmlToPdf(
  '<h1>Invoice #123</h1><p>Total: $99.00</p>',
  { page_size: 'Letter' }
);

console.log(`PDF URL: ${pdfUrl}`);
```

## Download to File (Node.js)

```javascript
import fs from 'fs';
import { pipeline } from 'stream/promises';

async function downloadPdf(url, filename) {
  const response = await fetch(url);
  const fileStream = fs.createWriteStream(filename);
  await pipeline(response.body, fileStream);
  console.log(`Downloaded: ${filename}`);
}

// Usage
await downloadPdf(pdfUrl, 'invoice.pdf');
```

## Browser Usage

```javascript
// In browser, download to user's device
async function downloadPdfInBrowser(url, filename) {
  const response = await fetch(url);
  const blob = await response.blob();

  const link = document.createElement('a');
  link.href = URL.createObjectURL(blob);
  link.download = filename;
  link.click();

  URL.revokeObjectURL(link.href);
}
```

## Error Handling

```javascript
try {
  const url = await client.htmlToPdf('<h1>Test</h1>');
} catch (error) {
  if (error.message.includes('401')) {
    console.error('Invalid API key');
  } else if (error.message.includes('402')) {
    console.error('No credits remaining');
  } else if (error.message.includes('429')) {
    console.error('Rate limit exceeded - please slow down');
  } else {
    console.error('Error:', error.message);
  }
}
```
```

---

## 13. `sdks/curl.mdx`

```mdx
---
title: 'cURL'
description: 'cURL examples for testing the Pdflet API'
---

# cURL Examples

Test the Pdflet API directly from your terminal.

## Set Your API Key

```bash
export PDFLET_API_KEY="pk_live_your_api_key"
```

## Create PDF from HTML

```bash
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: $PDFLET_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "html": "<html><body><h1>Hello World</h1><p>This is a test PDF.</p></body></html>"
  }'
```

Response:

```json
{
  "id": "conv_abc123",
  "status": "pending",
  "created_at": "2024-01-15T10:30:00Z"
}
```

## Create PDF with Options

```bash
curl -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: $PDFLET_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "html": "<h1>Report</h1>",
    "page_size": "Letter",
    "landscape": true,
    "margin_top": "1in",
    "margin_bottom": "1in",
    "margin_left": "0.5in",
    "margin_right": "0.5in",
    "print_background": true
  }'
```

## Check Conversion Status

```bash
curl https://api.pdflet.dev/api/v1/conversions/conv_abc123/ \
  -H "X-API-Key: $PDFLET_API_KEY"
```

Response (completed):

```json
{
  "id": "conv_abc123",
  "status": "completed",
  "file_url": "https://api.pdflet.dev/media/pdfs/conv_abc123.pdf",
  "created_at": "2024-01-15T10:30:00Z",
  "completed_at": "2024-01-15T10:30:02Z"
}
```

## Download PDF

```bash
curl -o output.pdf "https://api.pdflet.dev/media/pdfs/conv_abc123.pdf"
```

## Complete Workflow Script

```bash
#!/bin/bash

# Create PDF
RESPONSE=$(curl -s -X POST https://api.pdflet.dev/api/v1/pdf/ \
  -H "X-API-Key: $PDFLET_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"html": "<h1>Hello World</h1>"}')

CONVERSION_ID=$(echo $RESPONSE | jq -r '.id')
echo "Conversion started: $CONVERSION_ID"

# Poll for completion
while true; do
  STATUS_RESPONSE=$(curl -s \
    "https://api.pdflet.dev/api/v1/conversions/$CONVERSION_ID/" \
    -H "X-API-Key: $PDFLET_API_KEY")

  STATUS=$(echo $STATUS_RESPONSE | jq -r '.status')

  if [ "$STATUS" = "completed" ]; then
    FILE_URL=$(echo $STATUS_RESPONSE | jq -r '.file_url')
    echo "PDF ready: $FILE_URL"
    curl -o output.pdf "$FILE_URL"
    echo "Downloaded: output.pdf"
    break
  elif [ "$STATUS" = "failed" ]; then
    echo "Conversion failed"
    exit 1
  fi

  echo "Status: $STATUS - waiting..."
  sleep 1
done
```

## API Key Management

### List API Keys

```bash
curl https://api.pdflet.dev/api/v1/api-keys/ \
  -H "Authorization: Bearer $JWT_TOKEN"
```

### Create API Key

```bash
curl -X POST https://api.pdflet.dev/api/v1/api-keys/ \
  -H "Authorization: Bearer $JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "Production Server"}'
```

### Delete API Key

```bash
curl -X DELETE https://api.pdflet.dev/api/v1/api-keys/key_abc123/ \
  -H "Authorization: Bearer $JWT_TOKEN"
```

## Authentication

### Get JWT Token

```bash
curl -X POST https://api.pdflet.dev/api/v1/auth/jwt/create/ \
  -H "Content-Type: application/json" \
  -d '{
    "email": "your@email.com",
    "password": "your_password"
  }'
```

### Refresh Token

```bash
curl -X POST https://api.pdflet.dev/api/v1/auth/jwt/refresh/ \
  -H "Content-Type: application/json" \
  -d '{"refresh": "your_refresh_token"}'
```
```

---

## 14. `pricing.mdx`

```mdx
---
title: 'Pricing'
description: 'Plans and pricing for Pdflet'
---

# Pricing

Simple, transparent pricing based on your usage.

## Plans

<CardGroup cols={3}>
  <Card title="Free" icon="gift">
    **$0/month**

    - 100 credits/month
    - 10 requests/minute
    - Community support
    - Perfect for testing
  </Card>

  <Card title="Starter" icon="rocket">
    **$9/month**

    - 1,000 credits/month
    - 30 requests/minute
    - Email support
    - Great for side projects
  </Card>

  <Card title="Pro" icon="bolt">
    **$29/month**

    - 5,000 credits/month
    - 100 requests/minute
    - Priority support
    - Built for production
  </Card>
</CardGroup>

## What's a Credit?

One credit = one PDF conversion. Simple as that.

| Action | Credits |
|--------|---------|
| Convert HTML to PDF | 1 |
| Convert URL to PDF | 1 |

## Rate Limits

Rate limits are per minute and reset every 60 seconds.

| Plan | Requests/Minute |
|------|-----------------|
| Free | 10 |
| Starter | 30 |
| Pro | 100 |

If you exceed your rate limit, you'll receive a `429 Too Many Requests` response. Wait for the limit to reset and retry.

## Credit Rollover

Credits do **not** roll over to the next month. Unused credits expire at the end of each billing period.

## Upgrading

Upgrade anytime from your [dashboard settings](https://pdflet.dev/dashboard?settings=billing). You'll be prorated for the current billing period.

## Downgrading

Downgrade takes effect at the end of your current billing period. You'll keep your current plan's limits until then.

## Enterprise

Need more than 5,000 credits/month or custom rate limits?

<Card title="Contact Sales" icon="envelope" href="mailto:sales@pdflet.dev">
  We'll create a custom plan for your needs
</Card>

## FAQ

<AccordionGroup>
  <Accordion title="What happens if I run out of credits?">
    API requests will return a `402 Payment Required` error. Upgrade your plan or wait for the next billing cycle.
  </Accordion>

  <Accordion title="Can I buy additional credits?">
    Not currently. If you need more credits, upgrade to a higher plan.
  </Accordion>

  <Accordion title="Is there a free trial for paid plans?">
    The Free plan is essentially a permanent free trial. Try all features with 100 credits/month.
  </Accordion>

  <Accordion title="What payment methods do you accept?">
    We accept all major credit cards via our payment processor.
  </Accordion>
</AccordionGroup>
```

---

## 15. `errors.mdx`

```mdx
---
title: 'Error Handling'
description: 'API error codes and how to handle them'
---

# Error Handling

Learn how to handle errors from the Pdflet API.

## Error Response Format

All errors return a consistent JSON format:

```json
{
  "error": "error_code",
  "message": "Human-readable description",
  "details": {}
}
```

## HTTP Status Codes

| Code | Name | Description |
|------|------|-------------|
| `400` | Bad Request | Invalid request parameters |
| `401` | Unauthorized | Missing or invalid authentication |
| `402` | Payment Required | No credits remaining |
| `404` | Not Found | Resource doesn't exist |
| `429` | Too Many Requests | Rate limit exceeded |
| `500` | Internal Server Error | Something went wrong on our end |

## Common Errors

### Authentication Errors (401)

**Missing API Key**
```json
{
  "error": "authentication_required",
  "message": "Authentication credentials were not provided."
}
```

**Invalid API Key**
```json
{
  "error": "invalid_api_key",
  "message": "Invalid API key provided."
}
```

**Solution:** Verify your API key is correct and included in the `X-API-Key` header.

---

### Validation Errors (400)

**Missing HTML**
```json
{
  "error": "validation_error",
  "message": "Either 'html' or 'url' is required.",
  "details": {
    "html": ["This field is required."]
  }
}
```

**Invalid Page Size**
```json
{
  "error": "validation_error",
  "message": "Invalid page size.",
  "details": {
    "page_size": ["Must be one of: A4, Letter, Legal, A3, A5"]
  }
}
```

**Solution:** Check your request body matches the API specification.

---

### Credit Errors (402)

**No Credits**
```json
{
  "error": "insufficient_credits",
  "message": "You have no credits remaining. Please upgrade your plan."
}
```

**Solution:** [Upgrade your plan](https://pdflet.dev/dashboard?settings=billing) or wait for credits to reset.

---

### Rate Limit Errors (429)

**Rate Limited**
```json
{
  "error": "rate_limit_exceeded",
  "message": "Rate limit exceeded. Please slow down.",
  "details": {
    "retry_after": 45
  }
}
```

**Solution:** Wait for `retry_after` seconds before retrying. Implement exponential backoff.

---

### Not Found Errors (404)

**Conversion Not Found**
```json
{
  "error": "not_found",
  "message": "Conversion not found."
}
```

**Solution:** Verify the conversion ID is correct and belongs to your account.

---

## Handling Errors in Code

### Python

```python
import requests
from requests.exceptions import HTTPError

def create_pdf_safe(html):
    try:
        response = requests.post(
            "https://api.pdflet.dev/api/v1/pdf/",
            headers={"X-API-Key": API_KEY},
            json={"html": html}
        )
        response.raise_for_status()
        return response.json()

    except HTTPError as e:
        error_data = e.response.json()

        if e.response.status_code == 401:
            raise AuthenticationError(error_data["message"])
        elif e.response.status_code == 402:
            raise InsufficientCreditsError(error_data["message"])
        elif e.response.status_code == 429:
            retry_after = error_data.get("details", {}).get("retry_after", 60)
            time.sleep(retry_after)
            return create_pdf_safe(html)  # Retry
        else:
            raise ApiError(error_data["message"])
```

### JavaScript

```javascript
async function createPdfSafe(html) {
  const response = await fetch('https://api.pdflet.dev/api/v1/pdf/', {
    method: 'POST',
    headers: {
      'X-API-Key': API_KEY,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ html })
  });

  if (!response.ok) {
    const error = await response.json();

    switch (response.status) {
      case 401:
        throw new Error(`Authentication failed: ${error.message}`);
      case 402:
        throw new Error('No credits remaining');
      case 429:
        const retryAfter = error.details?.retry_after || 60;
        await new Promise(r => setTimeout(r, retryAfter * 1000));
        return createPdfSafe(html); // Retry
      default:
        throw new Error(error.message);
    }
  }

  return response.json();
}
```

## Retry Strategy

For transient errors (429, 500, 503), implement exponential backoff:

```python
import time
import random

def retry_with_backoff(fn, max_retries=3):
    for attempt in range(max_retries):
        try:
            return fn()
        except (RateLimitError, ServerError) as e:
            if attempt == max_retries - 1:
                raise

            # Exponential backoff with jitter
            delay = (2 ** attempt) + random.uniform(0, 1)
            time.sleep(delay)
```

<Tip>
  Always implement retry logic for rate limits (429) and server errors (5xx). These are often transient and succeed on retry.
</Tip>
```

---

# Setup Checklist

After creating all the files above in your Mintlify docs repository:

1. **Add logo files:**
   - `logo/dark.png` - Logo for dark mode (recommended: 200x50px)
   - `logo/light.png` - Logo for light mode (recommended: 200x50px)

2. **Add favicon:**
   - `favicon.png` - Site favicon (recommended: 32x32px or 64x64px)

3. **Update mint.json:**
   - Replace GitHub/Twitter URLs with your actual social links
   - Update `support@pdflet.dev` with your actual support email

4. **Commit and push:**
   ```bash
   git add .
   git commit -m "Add complete Pdflet documentation"
   git push origin main
   ```

5. **Verify deployment:**
   - Mintlify auto-deploys on push
   - Check `docs.pdflet.dev` after a few minutes

---

# API Reference Summary

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/auth/jwt/create/` | POST | Login (get JWT tokens) |
| `/auth/jwt/refresh/` | POST | Refresh access token |
| `/auth/users/` | POST | Register new user |
| `/auth/users/me/` | GET | Get current user |
| `/api-keys/` | GET | List API keys |
| `/api-keys/` | POST | Create API key |
| `/api-keys/{id}/` | DELETE | Revoke API key |
| `/pdf/` | POST | Create PDF conversion |
| `/conversions/{id}/` | GET | Get conversion status |
| `/subscription/` | GET | Get subscription info |
| `/billing/checkout/` | POST | Create checkout session |
| `/billing/change-plan/` | POST | Change plan |
| `/billing/cancel/` | POST | Cancel subscription |
