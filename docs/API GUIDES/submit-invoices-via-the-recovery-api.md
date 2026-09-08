---
title: Submit invoices via the Recovery API
excerpt: >-
  Submit a failed invoice to Recurly Recover for automated retry collection,
  read the response, and stop retries when a payment is collected or abandoned.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">The Recovery API is the entry point to Recurly Recover. A single authenticated request submits a failed invoice for collection — Recurly creates the account, opens a past-due invoice, records the failed transaction, and starts retrying on the retry window you assign. This guide covers submitting an invoice, reading the response, and stopping retries when collection finishes elsewhere.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#submit-a-failed-invoice"><span class="rp-toc-num">1</span>Submit a failed invoice</a>
    <a class="rp-toc-pill" href="#handle-the-response"><span class="rp-toc-num">2</span>Handle the response</a>
    <a class="rp-toc-pill" href="#stop-retries"><span class="rp-toc-num">3</span>Stop retries</a>
    <a class="rp-toc-pill" href="#payment-method-wallet"><span class="rp-toc-num">4</span>Payment method wallet</a>
    <a class="rp-toc-pill" href="#supported-gateways"><span class="rp-toc-num">5</span>Supported gateways</a>
    <a class="rp-toc-pill" href="#error-handling"><span class="rp-toc-num">6</span>Error handling</a>
    <a class="rp-toc-pill" href="#whats-next"><span class="rp-toc-num">7</span>What's next</a>
  </div>
</div>

### Prerequisites

<ul class="rp-list">
  <li>An active Recurly Recover account with an API key generated — see <a href="/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a>.</li>
  <li>At least one retry window (dunning campaign) configured.</li>
  <li>A reusable gateway token for each customer's payment method from Stripe or Braintree.</li>
</ul>

<div class="rp-callout rp-callout-warning">
  <div><strong><i class="fa-solid fa-triangle-exclamation" aria-hidden="true"></i> Warning</strong> Pause your own retry logic before submitting an invoice. Running parallel retries on the same payment method risks double-charging your customer.</div>
</div>

# Submit a failed invoice

Send a `POST` request to `/invoices/recovery`. A successful call creates a Recurly `Account`, a past-due charge invoice, and an initial failed transaction — and immediately begins the retry schedule.

Recover authenticates with HTTP Basic Auth: pass your API key as the username with an empty password.

```bash curl
curl -u YOUR_RECOVER_API_KEY: \
  -X POST https://v3.recurly.com/invoices/recovery \
  -H "Content-Type: application/json" \
  --data @recovery-request.json
```

## Request body

```json
{
  "currency": "str",
  "due_at": "2019-08-24T14:15:22Z",
  "po_number": "string",
  "external_recovery_eligible": true,
  "account": {
    "address": {
      "phone": "string",
      "street1": "string",
      "street2": "string",
      "city": "string",
      "region": "string",
      "postal_code": "string",
      "country": "string"
    },
    "billing_infos": [
      {
        "first_name": "string",
        "last_name": "string",
        "company": "string",
        "address": {
          "phone": "string",
          "street1": "string",
          "street2": "string",
          "city": "string",
          "region": "string",
          "postal_code": "string",
          "country": "string"
        },
        "ip_address": "string",
        "gateway_code": "string",
        "primary_payment_method": true,
        "backup_payment_method": true,
        "payment_gateway_references": [
          {
            "token": "string",
            "reference_type": "stripe_confirmation_token"
          }
        ],
        "network_transaction_id": "string",
        "transactions": [
          {
            "gateway_error_code": "string",
            "merchant_advice_code": "st",
            "attempted_collection_date": "2019-08-24T14:15:22Z"
          }
        ]
      }
    ],
    "code": "string",
    "email": "user@example.com",
    "custom_fields": [
      {
        "name": "string",
        "value": "string"
      }
    ],
    "dunning_campaign_id": "string"
  },
  "line_items": [
    {
      "tax": 0,
      "custom_fields": [
        {
          "name": "string",
          "value": "string"
        }
      ],
      "harmonized_system_code": "string",
      "product_code": "string",
      "quantity": 1,
      "description": "string",
      "unit_amount": 0
    }
  ]
}
```

## Fields that drive retry behavior

The full schema is documented in the API reference. These are the fields that determine how Recover collects:

<table class="rp-params">
  <tr class="rp-thead-row"><td>Field</td><td>What it does</td></tr>
  <tr><td><code>account.code</code></td><td>Your unique identifier for the account. Reusing a code that already exists returns an error — each call creates one account with one invoice.</td></tr>
  <tr><td><code>account.dunning_campaign_id</code></td><td>The retry window Recover follows for this invoice. Assign a different campaign per request to test strategies across segments.</td></tr>
  <tr><td><code>gateway_code</code></td><td>Routes the transaction to the correct gateway connection.</td></tr>
  <tr><td><code>payment_gateway_references</code></td><td>The reusable gateway <code>token</code> and its <code>reference_type</code> (for example, <code>stripe_confirmation_token</code>).</td></tr>
  <tr><td><code>transactions</code></td><td>Prior failed attempt history — <code>gateway_error_code</code>, <code>merchant_advice_code</code>, and <code>attempted_collection_date</code> — used to calculate the first retry date.</td></tr>
</table>

# Handle the response

A `201` response confirms that Recurly created the account and started the retry process. Save the `id` of the returned `charge_invoice` — you'll need it to stop retries later.

```json
{
  "object": "string",
  "charge_invoice": {
    "id": "string",
    "uuid": "string",
    "object": "string",
    "type": "charge",
    "origin": "carryforward_credit",
    "state": "open",
    "account": {
      "id": "string",
      "object": "string",
      "code": "string",
      "email": "user@example.com",
      "first_name": "string",
      "last_name": "string",
      "company": "string",
      "parent_account_id": "string",
      "bill_to": "parent",
      "dunning_campaign_id": "string"
    },
    "billing_info_id": "string",
    "subscription_ids": ["string"],
    "previous_invoice_id": "string",
    "number": "string",
    "collection_method": "automatic",
    "po_number": "string",
    "net_terms": 0,
    "net_terms_type": "net",
    "currency": "str",
    "discount": 0,
    "subtotal": 0,
    "subtotal_after_discount": 0,
    "tax": 0,
    "total": 0,
    "refundable_amount": 0,
    "paid": 0,
    "balance": 0,
    "dunning_campaign_id": "string",
    "due_at": "2019-08-24T14:15:22Z",
    "closed_at": "2019-08-24T14:15:22Z",
    "created_at": "2019-08-24T14:15:22Z",
    "updated_at": "2019-08-24T14:15:22Z"
  }
}
```

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> The response doesn't include the next scheduled retry date. Track retry progress through <a href="/docs/recurly-recover-webhooks" target="_blank">webhook notifications</a> instead.</div>
</div>

# Stop retries

While an invoice is in a `past_due` state, you can cancel all future retry attempts at any time. Use the invoice `id` returned in the original response. Once marked, Recover makes no further attempts on that invoice.

## Mark as paid

Use when the payment was collected outside of Recurly.

```bash curl
curl -u YOUR_RECOVER_API_KEY: \
  -X PUT https://v3.recurly.com/invoices/YOUR_INVOICE_ID/mark_successful
```

## Mark as failed

Use when you want to abandon collection.

```bash curl
curl -u YOUR_RECOVER_API_KEY: \
  -X PUT https://v3.recurly.com/invoices/YOUR_INVOICE_ID/mark_failed
```

# Payment method wallet

When the Wallet feature is enabled, you can designate payment methods as primary or backup in the same request. Set `primary_payment_method` or `backup_payment_method` to `true` on each entry in `billing_infos`. You can submit multiple payment methods, but only one can be marked as primary.

# Supported gateways

Recover currently supports the following gateways with reusable gateway tokens:

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Gateway</td><td>Token support</td></tr>
  <tr><td>Stripe</td><td>Reusable gateway tokens (for example, <code>stripe_confirmation_token</code>)</td></tr>
  <tr><td>Braintree</td><td>Reusable gateway tokens</td></tr>
</table>

# Error handling

Every call creates exactly one account with one invoice. Submitting a request with an `account.code` that already exists returns an error rather than creating a duplicate — generate a unique code per invoice, or mark the existing invoice as paid or failed before resubmitting.

# What's next

- <a href="/docs/recurly-recover-recovery-api-reference" target="_blank">Recovery API reference</a> — the complete endpoint and field schema
- <a href="/docs/recurly-recover-webhooks" target="_blank">Webhooks</a> — track retry progress and confirm the final outcome of each invoice
- <a href="/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a> — connect a gateway, set up webhooks, and generate your API key
