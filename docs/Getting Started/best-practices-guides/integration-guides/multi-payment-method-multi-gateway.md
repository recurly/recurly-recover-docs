---
title: Multi-payment method, multi-gateway
excerpt: >-
  Learn how to submit Recurly Recover invoices with multiple payment methods
  spread across multiple gateways, including token access, primary/backup logic,
  and NTID requirements.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">This guide covers testing best practices for using multiple payment methods across multiple gateways. For streamlined gateway token usage, confirm that each gateway you've enabled has access to its tokens — this is essential for a successful implementation.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#definition"><span class="rp-toc-num">1</span>Definition</a>
    <a class="rp-toc-pill" href="#integration-guide"><span class="rp-toc-num">2</span>Integration guide</a>
  </div>
</div>

### Prerequisites and limitations

<ul class="rp-list">
  <li>You've reviewed the <a href="https://docs.recurly.com/recurly-recover/docs/submit-invoices-via-the-recovery-api" target="_blank">basic API guide</a> and are familiar with the fields on the Recovery endpoint</li>
  <li>You've enabled multiple gateways on your Recurly sandbox site</li>
  <li>You've confirmed that the tokens you're using are accessible through your enabled gateways. For example, if you provide Recurly with Braintree gateway tokens, your enabled Braintree gateway must have access to them</li>
  <li>If your gateway tokens require a Network Transaction ID (NTID), you have the NTIDs available for Recurly to store and send. Stripe, Braintree, and PayPal Complete are exceptions — for any other gateway, provide the NTID you send during standard subscription processing</li>
</ul>

# Definition

<div class="rp-definition">Creating a recovery invoice means generating a new invoice through the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide covers submitting multiple payment methods across multiple gateways.</div>

# Integration guide

## Best practices

<ul class="rp-list">
  <li>Add multiple payment methods to the same invoice within the same API request. Don't submit separate invoices for different payment methods</li>
  <li>Specify which method is primary and which is backup based on your customer's preferences and your default gateway. For tokens that represent the same payment method on different gateways, make the primary designation match your default gateway — for example, if you have Braintree and Stripe tokens for the same Visa card and Stripe is your default gateway, set the Stripe token as the account's primary payment method</li>
  <li>Make sure your gateway permissions allow token metadata inquiries, so Recurly can identify which tokens share the same payment method and which are unique. This helps target the correct tokens and payment methods</li>
</ul>

## Example: multiple payment methods, multiple gateways

```json
```

***

For next steps and error handling, follow our dedicated integration guide: [Submit Invoices via Recovery API](https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/submit-invoices-via-the-recovery-api)
