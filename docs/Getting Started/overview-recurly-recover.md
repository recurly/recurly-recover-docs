---
title: 'Overview: Recurly Recover'
excerpt: >-
  Use Recurly Recover's standalone retry engine to collect on past-due invoices
  from your existing billing platform — without adopting Recurly for
  subscription management.
deprecated: false
hidden: true
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recurly Recover is a standalone retry engine for collecting on past-due invoices without requiring Recurly as your primary billing platform. Submit a failed invoice via the Recovery API, and Recurly automatically creates the account objects, calculates an optimized retry schedule, and manages the entire collection lifecycle until the invoice is paid or the retry window closes.</div>
  <div class="rp-toc">
   
    <a class="rp-toc-pill" href="#key-benefits"><span class="rp-toc-num">2</span>Key benefits</a>
    <a class="rp-toc-pill" href="#key-details"><span class="rp-toc-num">3</span>Key details</a>
    <a class="rp-toc-pill" href="#setup"><span class="rp-toc-num">4</span>Setup</a>
    <a class="rp-toc-pill" href="#roles--permissions"><span class="rp-toc-num">5</span>Roles & permissions</a>
    <a class="rp-toc-pill" href="#faqs"><span class="rp-toc-num">6</span>FAQs</a>
  </div>
</div>

### Onboarding includes

<ul class="rp-list">
  <li>An active  account with an API key generated.</li>
  <li>At least one retry window (dunning campaign) </li>
</ul>

### Limitations

<ul class="rp-list">
  <li>Recurly Recover is designed for merchants who don't use Recurly for subscription management.</li>
  <li>Each successful API call creates one account with one invoice. Calling the API again with the same account code returns an error.</li>
 <li>Accounts can only be created via the API, not through the Admin UI.</li>
</ul>

<li>Existing Recurly Subscriptions can utilize the Retries in RSM.</li>

# Key benefits

<div class="rp-benefits">
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-plug" aria-hidden="true"></i></div>
    <strong>Works with your stack</strong>
    <span>Use Recurly's retry engine without adopting Recurly for subscription management — it integrates with your existing billing system.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-sliders" aria-hidden="true"></i></div>
    <strong>Flexible retry strategies</strong>
    <span>Assign a different dunning campaign per API request, making it easy to A/B test retry windows and strategies across customer segments.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-arrows-rotate" aria-hidden="true"></i></div>
    <strong>Fully managed collection</strong>
    <span>Recurly handles the entire retry lifecycle — calculating optimal retry dates, managing payment attempts, and firing webhooks when the journey ends.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-bolt" aria-hidden="true"></i></div>
    <strong>Minimal setup</strong>
    <span>No need to configure plans, items, or taxes. Setup is limited to payment gateway, retry window, and API integration.</span>
  </div>
</div>

# Key details

## How Recurly Recover works

1. A payment fails on your billing platform.
2. You pause your internal retry logic for that invoice.
3. You call the Recovery API with account details, payment method tokens, prior attempt history, and the retry window you want Recurly to use.
4. Recurly creates an account, a past-due invoice, and a failed transaction.
5. Recurly calculates the first retry date based on your submission and begins retrying per the assigned retry window.
6. When a retry succeeds or the retry window is exhausted, Recurly fires a webhook. You update the invoice state in your system.

<div class="rp-callout rp-callout-warning">
  <div><strong><i class="fa-solid fa-triangle-exclamation" aria-hidden="true"></i> Warning</strong> Pause your internal retry logic before submitting an invoice to Recurly Recover. Running parallel retries on the same payment method risks double-charging your customer.</div>
</div>

# Configuration&#x20;

## Onboarding Flow

The first time you sign-in, you will be prompted through configuration.

<div class="rp-steps">
  <div class="rp-step">
    <div class="rp-step-num">1</div>
    <div><h4>Connect your payment gateway</h4><p>In initial onboarding flow, click <strong>Add Gateway</strong> and follow the prompts to connect your gateway. You may continue to add gateways or click Continue to finish configuration.</p> 
</div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">2</div>
    <div><h4>Note the gateway code</h4><p>Each gateway connection is assigned a unique <strong>gateway code</strong>. You'll pass this value in API requests to route transactions to the correct gateway. If you need to route different card types or merchant category codes through separate accounts, you can add multiple connections for the same provider — each gets its own gateway code.</p></div>
  </div>
 <div class="rp-step">
    <div class="rp-step-num">3</div>
    <div><h4>Setup webhooks</h4><p>In initial onboarding flow, enter your <strong>Endpoint URL</strong> and select the events you wish to send webhooks.</p> 
</div>
  </div> 
 <div class="rp-step">
    <div class="rp-step-num">4</div>
    <div><h4>Your API Key</h4><p>In initial onboarding flow, copy <strong>Your API key</strong>.</p> 
</div>
  </div>
<div class="rp-step">
    <div class="rp-step-num">5</div>
    <div><h4>Make your API call</h4><p>In initial onboarding flow, see the <strong>API Reference</strong> to make your API call.</p> 
</div>
  </div>
</div>

#

## Submit a failed invoice

Call `POST /invoices/recovery` to submit a failed invoice for collection. A successful request creates a Recurly account, a past-due invoice, and an initial failed transaction — and immediately begins the retry schedule.

### Endpoint

```
POST https://v3.recurly.com/invoices/recovery
```

### Request

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

## Handle the response

A successful `201` response confirms that Recurly has created the account and started the retry process. Save the `invoice_id` from the response — you'll need it to stop retries later.

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> The Recover API response doesn't include a field for the next scheduled retry date. Use webhook notifications to track retry progress — see <a href="#step-4-configure-webhooks">Step 4: Configure webhooks</a>.</div>
</div>

### Response

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

## Stopping retries

You can stop all future retry attempts on an invoice at any time while it's in a `past_due` state.

**Mark as paid** — use when payment was collected outside of Recurly:

```
PUT https://v3.recurly.com/invoices/{invoice_id}/mark_successful
```

**Mark as failed** — use when you want to abandon collection:

```
PUT https://v3.recurly.com/invoices/{invoice_id}/mark_failed
```

Use the `invoice_id` returned in the original API response. Once marked, Recurly won't make any further retry attempts on that invoice.

# Payment method wallet

When the Wallet feature is enabled, you can designate payment methods as primary or backup in your API request. You can submit multiple payment methods, but only one can be marked as primary.

# Payment Gateways

Currently supported gateways are Stripe and Braintree. &#x20;

Stripe:

```json
"payment_gateway_references": [
                   {
                       "token": "cus_TapC8aysC8GRkU",
                       "reference_type": "stripe_customer"
                   },
                   {
                       "token": "pm_1SddYODhxUCUQqaNKCscliir",
                       "reference_type": "stripe_payment_method"
                   }
               ]
```

Braintree:

```json
"payment_gateway_references": [
    {
        "token": "BT-0427-79"
    }
]
```

# Roles & permissions

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> This section describes Recurly Recover's current (stop-gap) roles and permissions model. A full custom-role system is planned; until then, access is managed through the four permission categories below.</div>
</div>

## How admin access is provisioned

<div class="rp-steps">
  <div class="rp-step">
    <div class="rp-step-num">1</div>
    <div><h4>Your site is provisioned on a Recover plan</h4><p>Recurly configures your merchant account on either the <strong>Recurly Recover Annual Monthly</strong> or <strong>Recurly Recover Monthly</strong> plan.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">2</div>
    <div><h4>The Admin user logs in</h4><p>Because the account is subscribed to a Recover plan, this user sees the Recover UI and navigation. Until roles are created, they see only the <strong>Admin</strong> navigation link and page.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">3</div>
    <div><h4>The Admin creates roles</h4><p>Using <strong>Admin → Roles</strong>, the Admin user builds one or more roles from the permission categories in the table below.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">4</div>
    <div><h4>The Admin invites users and assigns roles</h4><p>Each invited user is assigned one of the roles created in the previous step.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">5</div>
    <div><h4>Users get access based on their role</h4><p>Newly added users can access only the pages granted by the permission categories on their assigned role. Every user — regardless of role — has access to the Recover dashboard.</p></div>
  </div>
</div>

## Permission categories

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Category</td><td>Grants access to</td></tr>
  <tr>
    <td>Analytics & Insights</td>
    <td>
      <ul class="rp-list">
        <li><a href="https://prototypes.recurly.net/analytics/recovered-revenue/" target="_blank">Recovered revenue</a></li>
        <li><a href="https://prototypes.recurly.net/analytics/payment-processing/" target="_blank">Payment processing</a></li>
        <li><a href="https://prototypes.recurly.net/analytics/retry-recovery/" target="_blank">Retry & recovery</a></li>
        <li> <a href ="https://prototypes.recurly.net/analytics/campaign-performance/" target="_blank">Campaign Performance</a></li>
        <li><a href="https://prototypes.recurly.net/payments/invoices/" target="_blank">Invoices</a></li>
        <li><a href="https://prototypes.recurly.net/payments/transactions/" target="_blank">Transactions</a></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Configuration</td>
    <td>
      <ul class="rp-list">
        <li><a href="https://prototypes.recurly.net/payments/gateways/" target="_blank">Payment gateway settings</a> — view and edit</li>
        <li><a href="https://prototypes.recurly.net/retention/retry-windows/" target="_blank">Retention (retry window) settings</a> — view and edit</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Integrations</td>
    <td>
      <ul class="rp-list">
        <li><a href="https://prototypes.recurly.net/developer/api-credentials/" target="_blank">API credentials</a> — view and edit</li>
        <li><a href="https://prototypes.recurly.net/developer/webhooks/" target="_blank">Webhooks</a> — view and edit</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Admin</td>
    <td>
      <ul class="rp-list">
        <li>Users</li>
        <li>Roles</li>
      </ul>
    </td>
  </tr>
</table>

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong> A role can combine any number of these categories. For example, a role for a finance teammate might combine Analytics & Insights with Configuration, while a role for a developer might combine Integrations with Analytics & Insights.</div>
</div>

#

# FAQs

<Accordion title="Do I need Recurly Subscriptions to use Recurly Recover?" icon="fa-solid fa-link-slash">
  No. Recurly Recover is designed as a standalone retry engine for merchants using other billing platforms. Combining Recurly Recover with Recurly Subscriptions is not recommended.
</Accordion>

<Accordion title="What happens when I submit a past-due invoice via the API?" icon="fa-solid fa-file-invoice">
  Recurly creates an account (without a subscription), a charge invoice, and one or more failed transactions. Billing information is stored and Recurly automatically calculates the next collection attempt date based on your submission.
</Accordion>

<Accordion title="Can I stop retries on a past-due invoice?" icon="fa-solid fa-hand">
  Yes. While an invoice is in a past-due state, you can cancel all future collection attempts by marking the invoice as failed or paid using the Recurly Invoice API.
</Accordion>

<Accordion title="What happens when the retry window closes without a successful payment?" icon="fa-solid fa-hourglass-end">
  The invoice is marked as failed and a webhook event fires. No further retries are made. You can then handle the outcome in your system — for example, suspending access or triggering a win-back campaign.
</Accordion>

<Accordion title="What if a customer provides a new payment method outside of Recurly?" icon="fa-solid fa-credit-card">
  Mark the in-flight Recurly invoice as successful (if payment was collected) or as failed (to stop the current attempt), then submit a new recovery request with the updated payment method token.
</Accordion>

<Accordion title="Can I use Recurly Recover with existing Recurly Subscriptions customers?" icon="fa-solid fa-ban">
  Recurly Recover is not intended to work alongside Recurly Subscriptions — payment recovery is already included in your Recurly Subscriptions plan. For questions about which solution fits your needs, contact Recurly Sales or email <a href="mailto:support@recurly.com">[support@recurly.com](mailto:support@recurly.com)</a>.
</Accordion>

<Accordion title="Does the API response tell me when the next retry attempt will happen?" icon="fa-solid fa-clock">
  No. The Recover API response doesn't include a next-retry date or time. Track retry progress through webhook notifications instead — a <code>new_dunning_event</code> notification is delivered each time an invoice enters or hits a milestone in the retry schedule.
</Accordion>

<Accordion title="When do successful_payment, failed_payment, new_dunning_event, and closed_invoice fire?" icon="fa-solid fa-bolt">
  <ul class="rp-list">
    <li><strong>successful_payment</strong> — delivered after a retry transaction is created and successfully collected by the gateway. Expected once per invoice.</li>
    <li><strong>failed_payment</strong> — delivered after a retry transaction is created and declined by the gateway. Multiple notifications can fire per invoice depending on the retry window.</li>
    <li><strong>new_dunning_event</strong> — delivered when an invoice enters or hits a milestone in the dunning retry schedule, per the schedule's configured event count.</li>
    <li><strong>closed_invoice</strong> — delivered when a previously past-due invoice moves to a final state, either by being paid or by exhausting the retry schedule.</li>
  </ul>
</Accordion>

<Accordion title="What event sequence should I expect for a successful recovery versus an exhausted retry window?" icon="fa-solid fa-list-ol">
  You'll receive a <code>new_dunning_event</code> notification marking the schedule milestone, followed by a <code>successful_payment</code> or <code>failed_payment</code> notification confirming the outcome of that retry attempt. A <code>closed_invoice</code> notification is delivered for the invoice's final state, confirming that no further collection attempts will occur.
</Accordion>

<Accordion title="Which webhook event represents the authoritative final outcome?" icon="fa-solid fa-flag-checkered">
  <code>closed_invoice</code>. It includes a <code>state</code> parameter reflecting either <code>collected</code>/<code>paid</code> or <code>failed</code>/<code>unpaid</code>, and confirms that no other collection attempts will occur.
</Accordion>

<Accordion title="How do I correlate payment webhook events with the Recover invoice?" icon="fa-solid fa-link">
  Use the <code>invoice_id</code> parameter — it's a shared identifier that links all related invoices and their transactions across both object types.
</Accordion>

<Accordion title="How should I handle webhook authenticity, duplicate deliveries, and out-of-order events?" icon="fa-solid fa-shield-halved">
  Treat webhooks as triggers, not as the source of truth: verify they're genuine, ignore repeats, and always confirm state through an API query before acting.

  <ul class="rp-list">
    <li><strong>Authenticity</strong> — verify the <code>recurly-signature</code> header (HMAC-SHA256) on every JSON webhook using your endpoint's secret key. You can optionally add HTTP Basic Auth and IP allowlisting.</li>
    <li><strong>Duplicates</strong> — Recurly resends on delivery failure, so expect repeats. Use the <code>recurly-notification-id</code> header, which stays identical across retries of the same notification, to detect and skip ones you've already processed. Reply with a 2XX within 5 seconds so Recurly doesn't retry unnecessarily.</li>
    <li><strong>Out-of-order events</strong> — never act on the payload alone. Use the webhook as a signal to call the Recurly API, compare the result to your local record, and update only if the API confirms a change. This handles delayed retries arriving after the resource has already changed.</li>
  </ul>
</Accordion>

<Accordion title="How can I trigger and test all four webhook events in a sandbox?" icon="fa-solid fa-flask">
  Use Stripe test cards configured to trigger declines and successes. Testing both types in your sandbox triggers and delivers the corresponding notifications to your configured endpoint.

  <ul class="rp-list">
    <li>A successful Stripe test card triggers <code>new_dunning_event</code>, <code>successful_payment</code>, and <code>closed_invoice</code>.</li>
    <li>A declining Stripe test card triggers <code>new_dunning_event</code> and <code>failed_payment</code>. If tested with a shortened retry window, <code>closed_invoice</code> also fires once the schedule reaches its final milestone and the invoice automatically updates to a failed state.</li>
  </ul>
</Accordion>

<Accordion title="Who can create and assign roles in Recurly Recover?" icon="fa-solid fa-user-shield">
  Only a user with the Admin permission category can create roles and invite or assign users. Every user granted access — regardless of role — automatically has access to the Recover dashboard.
</Accordion>

<br />

<br />
