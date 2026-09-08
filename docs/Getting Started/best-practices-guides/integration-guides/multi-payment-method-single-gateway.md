---
title: Multi-payment method, single gateway
excerpt: >-
  Create recovery invoices via API and learn best practices around testing
  against multiple payment methods, and single gateway setup.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

This guide will cover the testing best practices for using multiple payment methods on a single gateway.

If you are using gateway tokens, ensure the gateway you have enabled has access to those tokens -- this is necessary for a successful implementation.

### Prerequisites & limitations

- Ensure you have reviewed the [basic API Guide](https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/submit-invoices-via-the-recovery-api) and are familiar with the fields in the Recovery endpoint.
- You have enabled a single gateway in your Recurly sandbox site.
- If you are using gateway tokens, you have confirmed that the tokens in use are accessible via your enabled gateway. Example, if you provide Recurly with Braintree gateway tokens, the enabled Braintree gateway must have access to them.
- If your gateway tokens require NTID reference, you have the NTIDs available for Recurly to store and send.

***

# Definition

**Creating Recovery Invoices** refers to the process of generating a new invoice via the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide specifically covers using multiple payment methods with a single gateway.

***

## Best Practices&#x20;

* **Add multiple payment methods** **against the same invoice&#x20;**&#x77;ithin the same API request. Do not add multiple invoices with different payment methods.
* **Specify which method is primary versus backup** based on your customer's preferences in their account within your environment.
* C

## Integration Guide

### Example using Multiple Payment Methods (Tokens) and Single Gateway

```json
```

###
