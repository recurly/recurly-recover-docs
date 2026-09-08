---
title: API Reference
excerpt: >-
  Interim reference for the Recurly Recover Recovery API — base URL,
  authentication, and endpoints — pending the full ReadMe API reference section.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">This is the interim reference for the Recurly Recover Recovery API. It lists the base URL, authentication, and the available endpoints. Full field-level request and response schemas will live in a dedicated API reference section in ReadMe.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#base-url-and-authentication"><span class="rp-toc-num">1</span>Base URL & auth</a>
    <a class="rp-toc-pill" href="#endpoints"><span class="rp-toc-num">2</span>Endpoints</a>
    <a class="rp-toc-pill" href="#request-and-response"><span class="rp-toc-num">3</span>Request & response</a>
  </div>
</div>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> This is a temporary reference page. A full, interactive API reference for Recover is coming to ReadMe and will replace it.</div>
</div>

# Base URL and authentication

All Recovery API requests go to the Recurly API v3 base URL:

```bash Base URL
https://v3.recurly.com
```

Recover authenticates with HTTP Basic Auth — pass your API key as the username with an empty password:

```bash curl
curl -u YOUR_RECOVER_API_KEY: https://v3.recurly.com/invoices/recovery
```

# Endpoints

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Method</td><td>Endpoint</td><td>Purpose</td></tr>
  <tr><td><code>POST</code></td><td><code>/invoices/recovery</code></td><td>Submit a failed invoice for collection</td></tr>
  <tr><td><code>PUT</code></td><td><code>/invoices/{invoice_id}/mark_successful</code></td><td>Stop retries — mark the invoice paid</td></tr>
  <tr><td><code>PUT</code></td><td><code>/invoices/{invoice_id}/mark_failed</code></td><td>Stop retries — abandon collection</td></tr>
</table>

# Request and response

Until the full schema lands here, the <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api" target="_blank">Submit invoices via the Recovery API</a> guide carries the complete example bodies:

- <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api#request-body" target="_blank">Request body</a> — the full `POST /invoices/recovery` payload
- <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api#handle-the-response" target="_blank">Response</a> — the `201` response with the returned `charge_invoice`

{/*
📋 TODO before publishing:
- [ ] Temporary page — replace this with the dedicated ReadMe API reference section for Recover once it exists, then repoint the "What's next" links on the Recovery API and Webhooks pages.
- [ ] Field-level schema — add per-field tables (name, type, required, description) for the request and response, or let the generated API reference cover them.
*/}
