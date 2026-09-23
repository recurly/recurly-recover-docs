---
title: Multi-payment method, single gateway
excerpt: >-
  Learn how to submit Recurly Recover invoices with multiple payment methods
  against a single gateway, including token access and NTID requirements.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">This guide covers testing best practices for using multiple payment methods on a single gateway. For streamlined gateway token usage, confirm that the gateway you've enabled has access to those tokens — this is essential for a successful implementation.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#definition"><span class="rp-toc-num">1</span>Definition</a>
    <a class="rp-toc-pill" href="#integration-guide"><span class="rp-toc-num">2</span>Integration guide</a>
  </div>
</div>

### Prerequisites and limitations

<ul class="rp-list">
  <li>You've reviewed the <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api" target="_blank">basic API guide</a> and are familiar with the fields on the Recovery endpoint</li>
  <li>You've enabled a single gateway on your Recurly sandbox site</li>
  <li>You've confirmed that the tokens you're using are accessible through your enabled gateway. For example, if you provide Recurly with Braintree gateway tokens, your enabled Braintree gateway must have access to them</li>
  <li>If your gateway tokens require a Network Transaction ID (NTID), you have the NTIDs available for Recurly to store and send. Stripe, Braintree, and PayPal Complete are exceptions — for any other gateway, send the NTID you provide for normal subscription processing</li>
</ul>

# Definition

<div class="rp-definition">Creating a recovery invoice means generating a new invoice through the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide covers submitting multiple payment methods against a single gateway.</div>

# Integration guide

## Best practices

<ul class="rp-list">
  <li>Add multiple payment methods to the same invoice within the same API request. Don't submit separate invoices for different payment methods</li>
  <li>Specify which method is primary and which is backup based on your customer's preferences in your own environment</li>
</ul>

## Example: multiple payment methods, single gateway

In this example, the singular gateway is Stripe, so gateway token formatting will follow Stripe-style PGR array. If you are not using Stripe, your PGR array will have a single object, and will not contain a reference type.

When using a single gateway, your gateway_code strings will match. It is required that the Stripe Customer IDs also match within a single account to avoid issues in token handling. If you have set up your Stripe token behavior to have a 1:1 relationship with the Customer ID do not send these tokens in a separate invoice to avoid overcharging.

```json
{
    "currency": "USD",
    "po_number": "NNNN",
    "due_at": "YYYY-MM-DDTHH:MM:SS.MSZ", // Date and Time 
    "account": {
      "code": "account-code", // Account code
      "dunning_campaign_id": "{{dunning_campaign_id}}", // Dunning Campaign ID
      "billing_infos": [ 
        {
          "gateway_code": "1234567890", 
          "primary_payment_method": true, // Wallet Primary indicator
          "backup_payment_method": false,
          "payment_gateway_references": [ // Stripe Token Format
            {
              "token": "pm_67890",
              "reference_type": "stripe_payment_method"
            },
            {
              "token": "cus_12345",
              "reference_type": "stripe_customer"
            }
          ],
          "transactions": [
              {
                  "gateway_error_code": "gateway-responsed-code-value", // The actual gateway response code returned in your integration
                  "attempted_collection_date": "YYYY-MM-DDTHH:MM:SS.MSZ",
                  "merchant_advice_code": "NN"
              }
          ]
        },
        {
          "gateway_code": "1234567890",
          "primary_payment_method": false,
          "backup_payment_method": false,
          "payment_gateway_references": [
            {
              "token": "pm_12345",
              "reference_type": "stripe_payment_method"
            },
            {
              "token": "cus_12345",
              "reference_type": "stripe_customer"
            }
          ]
        }
      ],
      "email": "customer@example-domain.com"
    },
    "line_items": [
      {
        "description": "Description of Invoice", // Overwritten when using Vindicia
        "unit_amount": 9.99
      }
    ],
    "external_recovery_eligible": true,
    "transaction_descriptor_suffix": "Descriptor Suffix" // New Descriptor Field (Suffix)
  }
```

***

For next steps and error handling, follow our dedicated integration guide: [Submit Invoices via Recovery API](https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/submit-invoices-via-the-recovery-api)
