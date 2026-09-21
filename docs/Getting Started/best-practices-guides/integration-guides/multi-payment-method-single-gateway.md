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

```json
```

***

📋 TODO before publishing:

- [ ] The multiple payment methods, single gateway example is empty in the source — add the payload before publishing.
- [ ] The source cuts off after a trailing, empty heading following the example. Confirm whether content is missing and supply it if so.
- [ ] No Testing your integration content was in the source — add sandbox/test-card guidance if this guide should include it.
- [ ] No Error handling and troubleshooting content was in the source — add if applicable.
