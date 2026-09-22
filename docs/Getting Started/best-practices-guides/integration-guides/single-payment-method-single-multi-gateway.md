---
title: Single payment method, single or multiple gateways
excerpt: >-
  Create recovery invoices via API and learn best practices around testing
  against a single payment method, and single or multi-gateway setup.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">This guide covers testing and integration best practices for submitting a single payment method against either a single gateway or multiple gateways. Single method, single gateway is the simplest setup to implement and test. If you're using gateway tokens across multiple gateways, careful token-to-gateway_code hygiene is essential for a successful implementation.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#definition"><span class="rp-toc-num">1</span>Definition</a>
    <a class="rp-toc-pill" href="#integration-guide"><span class="rp-toc-num">2</span>Integration guide</a>
  </div>
</div>

### Prerequisites and limitations

<ul class="rp-list">
  <li>You've reviewed the <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api" target="_blank">basic API guide</a> and are familiar with the fields on the Recovery endpoint</li>
  <li>You've enabled one or more gateways on your Recurly sandbox site</li>
  <li>You know which gateway tokens are accessible through your enabled gateways. For example, if you provide Recurly with Braintree gateway tokens, your enabled Braintree gateway must have access to them</li>
  <li>If your gateway tokens require a Network Transaction ID (NTID), you have the NTIDs available for Recurly to store and send. Stripe, Braintree, and PayPal Complete are exceptions — for any other gateway, provide the NTID you use for normal subscription processing</li>
</ul>

# Definition

<div class="rp-definition">Creating a recovery invoice means generating a new invoice through the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide covers submitting a single payment method against either a single gateway or multiple gateways.</div>

# Integration guide

## Best practices

<ul class="rp-list">
  <li>Use the original gateway and merchant account the customer's subscription was set up on — this gives you the best chance of success</li>
  <li>Confirm the token exists on the target gateway. Tokens are typically tied to the specific gateway account they were created on, so specifying a different account can cause an error</li>
  <li>Pass the NTID on any gateway that requires it and doesn't handle storage on your behalf or Recurly's</li>
  <li>When using tokens across multiple gateways, submit a separate token for each gateway that represents the same payment method. For example, to have Recurly attempt a single Visa card on both Stripe and Braintree, you'll need a token from each gateway, even though they represent the same underlying card. Review <a href="https://docs.recurly.com/recurly-recover/docs/multiple-payment-methods" target="_blank">Multiple payment methods best practices</a> to make sure your testing is complete</li>
</ul>

## Example: single payment method, single gateway

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
            "token": "string" // Single-part Tokens Only
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

## Stripe Formatting

If you are using Stripe, the PGR array is formatted in the following manner as Stripe has two-part tokens. You must provide the Customer ID and the Payment Method ID as below.

```json
 "payment_gateway_references": [
          {
            "token": "string",
            "reference_type": "stripe_payment_method"
          },
          {
            "token": "string",
            "reference_type": "stripe_customer"
          }
        ],
```

***

For next steps, follow our dedicated integration guide:&#x20;

<br />
