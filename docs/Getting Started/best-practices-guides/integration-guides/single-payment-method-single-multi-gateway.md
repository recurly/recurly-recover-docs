---
title: Single payment method, single or multiple gateways
excerpt: >-
  Create recovery invoices via API and learn best practices around testing
  against a single payment method, and single or multi-gateway setup.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

This guide will cover the testing best practices for both the single/single and single/multiple (payment method&#x20;

Generally, the Single method / Single gateway is the easiest to implement and test in your recovery suite. If you are using gateway tokens, multiple gateways and token to gateway_code hygiene is necessary for a successful implementation.

### Prerequisites & limitations

- Ensure you have reviewed the basic API Guide and are familiar with the fields in the Recovery endpoint.
- You have enabled one or more gateways in your Recurly sandbox site.
- If you are using gateway tokens, you have awareness of which tokens are accessible via your enabled gateways. Example, if you provide Recurly with Braintree gateway tokens, the enabled Braintree gateway must have access to them.
- If your gateway tokens require NTID reference, you have the NTIDs available for Recurly to store and send.

***

# Definition

**Creating Recovery Invoices** refers to the process of generating a new invoice via the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide specifically covers using a single payment method with a single or multi-gateway setup.

***

## Best Practices&#x20;

* **Use the original gateway** **and merchant account&#x20;**&#x74;hat the customer's subscription was set up on. This gives you the best opportunity for success.
* **Ensure the token exists&#x20;**&#x6F;n the target gateway. Since tokens are typically tied to the specific gateway account they were created on, specifying a different account may result in an error.
* **Pass the NTID** on gateways that require the value and do not handle storage on yours or Recurly's behalf.
* **When using raw card details**, ensure you have the full card data (number and expiration date), and the original CIT NTID. Recurly retry transactions are merchant initiated.
* **Enable Account Updater** if you are using raw card data.
* **If using tokens with multiple gateways** you will need to submit multiple tokens that represent the same payment method. For example, if you want Recurly to attempt a single Visa on Stripe and Braintree, we will need the tokens for Stripe and Braintree even if they are the same underlying card number. You should review Multiple Payment Methods with Multiple Gateways best practices to ensure your testing is complete.

## Integration Guide

### Example using Single Payment Method (Token) and Single Gateway

```json
```

### Example using Single Payment Method (Token) and Multi Gateway

```json
```

###
