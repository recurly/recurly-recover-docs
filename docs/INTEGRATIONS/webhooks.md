---
title: Webhooks
excerpt: >-
  Track Recurly Recover retry progress and confirm each invoice's final outcome
  with the four webhook events, and handle delivery securely and idempotently.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">The Recovery API response doesn't tell you when the next retry will run or how collection ends — webhooks do. Recover sends four events across an invoice's retry lifecycle so your system can follow progress and record the final outcome. This guide covers what each event means, the order they arrive in, how to tie them back to an invoice, and how to handle delivery securely.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#the-four-events"><span class="rp-toc-num">1</span>The four events</a>
    <a class="rp-toc-pill" href="#event-sequences"><span class="rp-toc-num">2</span>Event sequences</a>
    <a class="rp-toc-pill" href="#correlate-events-with-an-invoice"><span class="rp-toc-num">3</span>Correlate events</a>
    <a class="rp-toc-pill" href="#handle-webhooks-safely"><span class="rp-toc-num">4</span>Handle safely</a>
    <a class="rp-toc-pill" href="#test-in-the-sandbox"><span class="rp-toc-num">5</span>Testing</a>
    <a class="rp-toc-pill" href="#whats-next"><span class="rp-toc-num">6</span>What's next</a>
  </div>
</div>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> Set your endpoint URL and choose which events to receive in the onboarding flow — see <a href="https://docs.recurly.com/recurly-recover/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a>.</div>
</div>

# The four events

Recover fires these four events as an invoice moves through its retry schedule:

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Event</td><td>When it fires</td><td>How often</td></tr>
  <tr><td><code>new_dunning_event</code></td><td>An invoice enters or reaches a milestone in the dunning retry schedule.</td><td>Once per configured schedule milestone</td></tr>
  <tr><td><code>successful_payment</code></td><td>A retry transaction is created and collected by the gateway.</td><td>Once per invoice</td></tr>
  <tr><td><code>failed_payment</code></td><td>A retry transaction is created and declined by the gateway.</td><td>Can fire multiple times per invoice, depending on the retry window</td></tr>
  <tr><td><code>closed_invoice</code></td><td>A past-due invoice reaches a final state — either paid or the retry window is exhausted.</td><td>Once per invoice</td></tr>
</table>

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong> Treat <code>closed_invoice</code> as the authoritative final outcome. Its <code>state</code> value reflects either <code>collected</code>/<code>paid</code> or <code>failed</code>/<code>unpaid</code>, and confirms that no further collection attempts will occur.</div>
</div>

# Event sequences

Every invoice follows one of two paths. A `new_dunning_event` marks the schedule milestone, a payment event reports the outcome of that attempt, and `closed_invoice` records the final state.

### Successful recovery

`new_dunning_event` → `successful_payment` → `closed_invoice` (`state`: `collected`/`paid`)

### Exhausted retry window

`new_dunning_event` → `failed_payment` (one or more) → `closed_invoice` (`state`: `failed`/`unpaid`)

# Correlate events with an invoice

Every event carries an `invoice_id` — a shared identifier that links all related invoices and their transactions across object types. Key your local records on `invoice_id` to match incoming events back to the invoice you submitted.

# Handle webhooks safely

<div class="rp-callout rp-callout-important">
  <div><strong><i class="fa-solid fa-circle-exclamation" aria-hidden="true"></i> Important</strong> Treat webhooks as triggers, not the source of truth: verify they're genuine, ignore repeats, and confirm state through an API query before acting.</div>
</div>

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Concern</td><td>How to handle it</td></tr>
  <tr><td>Authenticity</td><td>Verify the <code>recurly-signature</code> header (HMAC-SHA256) on every JSON webhook using your endpoint's secret key. You can optionally add HTTP Basic Auth and IP allowlisting.</td></tr>
  <tr><td>Duplicate deliveries</td><td>Recurly resends on delivery failure, so expect repeats. Dedupe on the <code>recurly-notification-id</code> header, which stays identical across retries of the same notification, and reply with a 2XX within 5 seconds so Recurly doesn't retry unnecessarily.</td></tr>
  <tr><td>Out-of-order events</td><td>Never act on the payload alone. Use the event as a signal to call the API, compare the result against your local record, and update only when the API confirms a change.</td></tr>
</table>

## Verify the signature

Compute an HMAC-SHA256 of the raw request body with your endpoint's secret key and compare it, in constant time, to the `recurly-signature` header.

```javascript Node.js
const crypto = require("crypto");

function verifyRecurlySignature(rawBody, signatureHeader, secret) {
  const expected = crypto
    .createHmac("sha256", secret)
    .update(rawBody)
    .digest("hex");
  return crypto.timingSafeEqual(
    Buffer.from(expected),
    Buffer.from(signatureHeader)
  );
}
```

# Test in the sandbox

Use Stripe test cards configured to trigger declines and successes. Testing both in your sandbox delivers the corresponding events to your configured endpoint.

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Stripe test card</td><td>Events delivered</td></tr>
  <tr><td>Successful</td><td><code>new_dunning_event</code>, <code>successful_payment</code>, <code>closed_invoice</code></td></tr>
  <tr><td>Declining</td><td><code>new_dunning_event</code>, <code>failed_payment</code> — and <code>closed_invoice</code> once a shortened retry window reaches its final milestone and the invoice moves to a failed state</td></tr>
</table>

# What's next

- <a href="https://docs.recurly.com/recurly-recover/docs/recovery-api-reference" target="_blank">Recovery API reference</a> — the complete endpoint and field schema
- <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api" target="_blank">Submit invoices via the Recovery API</a> — submit an invoice, read the response, and stop retries
- <a href="https://docs.recurly.com/recurly-recover/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a> — configure your endpoint and select events
